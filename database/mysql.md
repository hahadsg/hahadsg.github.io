### unix开启mysql服务
* 开启服务
```bash
sudo /Library/StartupItems/MySQLCOM/MySQLCOM start
```


* 开启守护进程
```bash
cd /usr/local/mysql
sudo ./bin/mysqld_safe
(Enter your password, if necessary)
(Press Control-Z)
```