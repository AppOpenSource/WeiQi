

## 取消Git仓库的版本关联   
在本地仓库的目录下调用命令行删除根目录下的.git文件夹，输入   
find . -name ".git" | xargs rm -Rf     
这样本地仓库就清除了，在GitBash中master就不见了   

## git查看远程仓库地址
git查看远程仓库地址命令：       
$git remote -v        


