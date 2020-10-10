# Git-common-docs
## 1、Git切换分支报错问题

```tex
第一种方式：
git add .
git stash 缓存
git stash pop 弹出缓存
第二种方式：
git add .
git commit -m 'msg'
第三种方式：清除未跟踪的文件
git clean -n 预览要清除的文件
git clean -f 强制清除文件
第四种：强制切换分支(粗暴的方式)
git checkout -f <branch>
```

## 2、Git撤销add文件

```tex
git status 查看当前工作去的状态情况
git reset HEAD 撤销上一下全的add的文件
git reset HEAD test.java 撤销某个文件
git reset HEAD file 撤销某个文件夹中的所有文件
```

