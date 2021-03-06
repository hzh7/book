# Git 

## [git 无法添加文件夹下的文件](https://blog.csdn.net/m0_37315653/article/details/83064810)

无论使用啥命令，都无法将文件夹下的某些文件添加进 Git 进行版本控制  
原来是子文件夹下面含有 .git 文件夹，因此导致该子文件夹无法被 Git 跟踪，可以通过以下方法解决：
```bash
git rm --cached folder
git add folder
```
其中 folder 为子文件夹。

## 新仓库
简易的命令行入门教程:
```bash
Git 全局设置:
git config --global user.name "lab1008"
git config --global user.email "lab1008@163.com"

创建 git 仓库:
mkdir lab_1008
cd lab_1008
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin git@gitee.com:lab_1008/lab_1008.git
git push -u origin master

已有仓库?
cd existing_git_repo
git remote add origin git@gitee.com:lab_1008/lab_1008.git
git push -u origin master
```

## git 撤销commit  
```bash
撤回最近一次的commit(撤销commit，不撤销git add)  
git reset --soft HEAD~1 

撤回最近一次的commit(撤销commit，撤销git add)  
git reset --mixed HEAD~1 

撤回最近一次的commit(撤销commit，撤销git add,还原改动的代码)  
git reset --hard HEAD~1 
```

## git 删除
```bash
# use --cached to keep the file
$ git rm --cached xxx.pdf
# -f to force removal
$ git rm -f xxx.pdf
```