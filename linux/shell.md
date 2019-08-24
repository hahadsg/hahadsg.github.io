## difference between \`sh\` and \`source\`

[https://stackoverflow.com/questions/13786499/what-is-the-difference-between-sh-and-source](https://stackoverflow.com/questions/13786499/what-is-the-difference-between-sh-and-source)

When you call `source` \(or its alias `.`\), you _insert_ the script in the **current** bash process. So you could read variables set by the script.

When you call `sh`, you initiate a _fork_ \(sub-process\) that runs a new session of `/bin/sh`, which is usually a symbolic link to `bash`. In this case, environment variables set by the sub-script would be dropped when the sub-script finishes.

## run script

```bash
nohup python -u myscript.py > myout.file 2>&1 &
```

## stderr stdout

* stderr/stdout分别输出到文件

  ```bash
  python test.py 2>stderr.log 1>stdout.log
  ```

* stderr/stdout分别输出到文件，也打印到屏幕

  ```bash
  # -a 代表append
  python test.py 2> >(tee -a stderr.log) 1> >(tee -a stdout.log)
  ```

## 进程

* 获取上一个进程号

  ```bash
  echo $!
  ```
  
* 获取上一个command的退出码

  ```bash
  # 经测试，获得的是当前session的上一个命令的退出码，如果开两个窗口，之间互不干扰
  # cmd1 | cmd2 会返回cmd2的退出码
  # cmd & 总是会返回0
  echo $?
  ```
  
* 后台执行获取退出码

  ```bash
  python -c 'import time; time.sleep(10); a = b'
  wait $!
  echo $?
  # 这时就会返回这个python命令的退出码，exit_code=1
  ```
  
## 调试shell

https://www.ibm.com/developerworks/cn/linux/l-cn-shell-debug/index.html

## Syntax

* sh file head

```bash
#!bin/sh
set -e -u -x
export LANG=en_US.UTF-8

# -e Exit immediately if a command exits with a non-zero status.
# -u Treat unset variables as an error when substituting.
# -x Print commands and their arguments as they are executed.
```

* for

```bash
# for int range
for i in {1..100}
do
    echo $i
done

# for int range use seq
for i in $(seq $start $end); do echo $i; done
```

* xagrs

```
# -I
seq 1 30 | xargs -I {} date -d "2018/11/{}" "+%Y-%m-%d"
```

* strip

```
${string#substring}Strip shortest match of $substring from front of $string
${string%substring}Strip shortest match of $substring from back of $string
#代表删除从前往后最小匹配的内容
%代表删除从后往前最小匹配的内容

s="abc"
${s#a} # -> bc
${s%c} # -> ab

s="a/b/c"
${s#*/} # -> b/c
${s%/*} # -> a/b
```

* path parse

```
p="./foo/bar/f.txt"
echo `dirname $p` # -> ./foo/bar
echo `basename $p` # -> f.txt
```