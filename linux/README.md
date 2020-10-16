# Linux常用命令

## 1、模糊搜索历史命令

```tex
a、Ctrl+ r 组合键进入历史记录搜寻状态，然后，键盘每按一个字母，当前命令行就会搜索出命令历史记录．
b、history
用法：
history [n]  n为数字，列出最近的n条命令
-c  将目前shell中的所有history命令消除
history [-raw] histfiles
-a 将目前新增的命令写入histfiles, 默认写入~/.bash_history
-r  将histfiles内容读入到目前shell的history记忆中
-w 将目前history记忆的内容写入到histfiles
```

## 2、防火墙开启重启

```properties
开启:firewall-cmd --zone=public --add-port=10880/tcp --permanent
重启:firewall-cmd --reload
```

