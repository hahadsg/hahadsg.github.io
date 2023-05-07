## supervisord

```bash
supervisord -c /path/to/supervisord.conf
```

## supervisorctl

``` bash
# 帮助
supervisorctl -h
supervisorctl help
# 查看状态
supervisorctl status
# 启动tornado
supervisorctl start <group>:<program>
supervisorctl start tornado:*
# 重启tornado
supervisorctl restart tornado:*
# 重载supervisor配置并重启
supervisorctl update
# 重载supervisor配置不重启
supervisorctl reread tornado
```