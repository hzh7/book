# Git 

## [git 无法添加文件夹下的文件](https://blog.csdn.net/m0_37315653/article/details/83064810)

无论使用啥命令，都无法将文件夹下的某些文件添加进 Git 进行版本控制  
原来是子文件夹下面含有 .git 文件夹，因此导致该子文件夹无法被 Git 跟踪，可以通过以下方法解决：
```bash
git rm --cached folder
git add folder
```
其中 folder 为子文件夹。