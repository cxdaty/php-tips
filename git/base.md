<h1 align="center">git基础</h1>

分支说明

 名称 | 说明 | 命名规范 | 命名示例 | 合并目标 | 合并操作
---|---|---|---|---|---
master | 线上稳定版本 | master | master | -- | --
release | 待发布分支，下个版本需上线的版本 | release/xxx | release/v1.0.0 | master | merge request
develop | 当前正在开发的分支 | develop | develop | master | merge request
feature | 功能分支，每个功能需分别建立自己的子分支 | feature/版本号-功能名 | feature/v1.0.0-Login | develop | merge request
hotfix  | 紧急修复分支 | hotfix/xxx | hotfix/v1.0.1 | master/develop | merge request

其中主分支 master、develop 为受保护分支


操作指导

一. 拉取项目代码，使用 ssh 方式
```
1. 打开本地git brash，在其中输入指令，生成ssh公钥和私钥对
ssh-keygen -t rsa -C 'xxx@xxx.com'
//其中xxx@xxx.com即为你的邮箱地址
//点击回车，会让你选择存储路径，此时不用理会直接回车，其会保存到默认路径
//可能有人此目录下已有该文件，他会提示是否覆盖，输入yes回车即可
//接下来就是输入密码，不用输入，再次回车，其会让你再次确认输入密码，再回车，即生成完毕

2. 在cmd中复制到公钥，打开电脑的cmd，在其中输入命令并回车
type %userprofile%\.ssh\id_rsa.pub | clip
//此时已复制

3. GitLab上添加SSH-Keys
Settings->SSH Keys
//将公钥复制到 Key 中，下方title可自己命名，点击addkey。

4. 拉取代码，例
git clone git@192.168.2.186:mowork/moplat.git
```

二、配置信息（必须）
```
//用户名邮箱配置
//此处必须填写你在 GitLab 的名字和邮箱
git config user.name “Name”
git config user.email "gitlab@xx.com"

//查看配置
git config --list
```

三、以远程 develop 分支为基础创建本地 develop 分支
```
git checkout -b develop origin/develop
```
git clone -b 分支名称

四、功能开发
```
1. 以 develop 分支为基础创建功能分支，这里以 登录 功能为例
git checkout -b feature/v1.0.0-Login develop
//注意：这里的版本号为下阶段将要发布的版本

2. 开发调试完成，将 feature分支 推送到远程仓库
git push origin feature/v1.0.0-Login
//注意：这里的远程分支名与本地分支名一致

3. 提交 merge request 请求合并到 develop 分支；
此操作在 GitLab 上完成
//注意：
//Source branch为 feature 分支，此处为 feature/v1.0.0-Login
//Target branch 为develop分支

4. merge request 结果操作
//相关负责人 code review 后且同意合并
//跳回 develop，pull代码，并删除对应 feature 分支
git checkout develop
git pull 
git branch -d feature/v1.0.0-Login
//不同意合并
重新修改后再上传 feature 分支，请求 merge request
```

五、紧急bug修复
```
1. 以 master 分支为基础创建 hotfix 分支，这里以 1.0.0 版本为例
git checkout -b hotfix/v1.0.0 master
//注意：这里的版本号为当前版本

2. 修改调试完成，将 hotfix分支 推送到远程仓库
git push origin hotfix/v1.0.0

3. 提交 merge request 请求合并到 master 分支；
此操作在 GitLab 上完成
//注意：
//Source branch为 hotfix 分支，此处为 hotfix/v1.0.0
//Target branch 为master分支

4. merge request 结果操作
//相关负责人 code review 后且同意合并
//跳回 master，pull代码，并删除对应 hotfix 分支
git checkout master
git pull 
git branch -d hotfix/v1.0.0
//不同意合并
重新修改后再上传 hotfix 分支，请求 merge request
```

六、发布新的版本
```
//当develop分支上的代码已经包含了所有即将发布的版本中所计划包含的软件功能，并且已通过所有测试时，我们就可以考虑准备创建release分支了
1. 以 develop分支 为基础创建 release分支，此处以版本1.0.0为例
git checkout -b release/v1.0.0 develop

2. 修改完成，将 release分支 推送到远程仓库
git push origin release/v1.0.0
//在这个分支上的代码允许做小的缺陷修正、准备发布版本所需的各项说明信息（版本号、发布时间、编译时间等）
//- 修改 README 版本信息  - 修改 config/version 版本信息  - 将数据库更改record整理成version

3. 推送gitlab触发自动部署
git push origin release/v1.0.0

4. 开发环境服务端更新 composer 和 数据库

3. 提交 merge request 请求合并到 master 分支；
此操作在 GitLab 上完成
//注意：
//Source branch为 release 分支，此处为 release/v1.0.0
//Target branch 为master分支

release分支提交 merge request 请求合并到 develop 分支；

4. merge request 结果操作
//相关负责人 code review 后且同意合并
//跳回 master，pull代码，并删除对应 release 分支
git checkout master
git pull 
git branch -d release/v1.0.0
//不同意合并
重新修改后再上传 release 分支，请求 merge request

5. 在 master分支 打tag，并推送到远程仓库，此时新版本发布完毕
git tag -a 1.0.0 -m 'version 1.0.0'
git push origin 1.0.0
```


测试环境完成测试后，发布正式版本

一. 平台
```
1. release 合并到 master
2. 新建tag，推送到仓库
3. 拉取对应版本
4. 确认数据库配置
5. 部署
```

二. oem
```
1. release 合并到 master
2. 新建tag，推送到仓库
3. 拉取对应版本
4. 确认数据库配置、环境变量
5. composer安装依赖
6. 部署
```

三、单体 - 更新包形式
```
1. release 合并到 master
2. 新建tag，推送到仓库
3. 拉取对应版本
4. 确认配置文件（system.php、database.php、redis.php）、环境变量
5. composer安装依赖
6. 打包上传平台对应BU
```

环境变量
```
- 生产 prod
- 测试 test
- 开发 dev
```

克隆分支
```
git clone --branch 1.3.0 git@192.168.2.186
```