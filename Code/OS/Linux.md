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