# Linux

> [Wiki](https://en.wikipedia.org/wiki/Linux)
> Linux is a family of free and open-source software operating systems built around the Linux kernel.

## Tutorials

- [UNIX Tutorial for Beginners](http://www.ee.surrey.ac.uk/Teaching/Unix/)

## Tips

- & && | ||
    - &  表示任务在后台执行，如要在后台运行redis-server,则有  redis-server &

    - && 表示前一条命令执行成功时，才执行后一条命令 ，如 echo '1‘ && echo '2'    

    - | 表示管道，上一条命令的输出，作为下一条命令参数，如 echo 'yes' | wc -l

    - || 表示上一条命令执行失败后，才执行下一条命令，如 cat nofile || echo "fail"2 
- grep（global search regular expression(RE) and print out the line，全面搜索正则表达式并把行打印出来）

## Notes

- linux 任务执行ssh脚本需在.sh文件添加执行命令中的路径，比如执行java就需添加
```bash
export JAVA_HOME=/home/ubuntu/java/jdk1.8.0_181
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export LANG=zh_CN.gbk
```

