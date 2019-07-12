<h1 align="center">git状态和撤销提交</h1>


一. Git的几种状态
```
未修改
       原始内容
已修改    ↓   
       工 作 区
已暂存    ↓    git add
       暂 存 区
已提交    ↓    git commit
       本地仓库
已推送    ↓    git push
       远程仓库
```

二、已修改 未暂存(使用以下任意命令)
    
```
已经修改了文件，还未进行git add.即工作区的内容不想要了
1.git checkout .
2.git checkout -- <FILENAME>
3.git reset --hard
```

三、已暂存 未提交(git add.)
```
已经进行了git add，还未进行git commit.即暂存区的内容不想要了
1.git reset,git checkout .
2.git reset --hard
3.git reset HEAD
4.git reset HEAD -- <FILENAME>
```

四、已提交 未推送(git commit)
```
已经进行了git commit，还未进行git push;使用远程仓库覆盖本地仓库
1.git reset --hard origin/master
```

五、已推送(git push)
```
回滚本地仓库，强制推送覆盖远程仓库
git reset --hard HEAD^
git push -f
```



