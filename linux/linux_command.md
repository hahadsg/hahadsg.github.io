# Linux Info

* `cat /etc/os-release`

```
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```

# Linux Command

* find

```bash
$ find [path] -name [name]
```

* !

```bash
$ !! # 上一条命令
$ !-x # 上x条命令
$ !!:s/p1/p2/ # 将上条命令的p1替换成p2
$ ^p1^p2^ # 等同于上条命令
```

* {}

```bash
$ echo {a,b}{a,b} # 会生成全排列的aa ab ba bb
$ cp filename{,.bak} # 备份文件
```

* &gt;

```bash
$ > file.txx # 清空或创建文件
```

* ssh

```bash
$ ssh-keygen # 生成公钥
$ ssh-copy-id remote-machine # 直接把本机的公钥写到远程主机的~/.ssh/authorized_keys内
```

* Keyboard

```
command <CTRL-xe># 用编辑器敲命令（打开的编辑器通过环境变量$EDITOR指定）
```



