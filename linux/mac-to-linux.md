## 在Mac上执行bash（Linux下的脚本）

1. 安装coreutils

 ```
 brew install coreutils
 ```

2. 加入gnubin路径

 由于装完coreutils后，所有gnu的命令需要带前缀g，所以加入gnubin路径

 ```
 PATH="/usr/local/opt/coreutils/libexec/gnubin:$PATH"
 ```


