## 代理 转发

[http://www.cnblogs.com/wangkangluo1/archive/2011/06/29/2093727.html](http://www.cnblogs.com/wangkangluo1/archive/2011/06/29/2093727.html)

## SSH-key设置

参考[https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

```
ssh-keygen -t rsa -b 4096 -C "809428197@qq.com"
eval "$(ssh-agent -s)"
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa
```

或者

```
ssh-keygen -t dsa -P '' -f ~/.ssh/id_rsa
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa
```

## ssh config

`~/.ssh/config`
`chmod 600 ~/.ssh/config`

```
Host 别名
    HostName 主机名
    Port 端口
    User 用户名
    IdentityFile 密钥文件的路径
    IdentitiesOnly 只接受SSH key 登录
    PreferredAuthentications 强制使用Public Key验证
```

## 关于ssh连接被断开的问题

一般即便设置了`TCPKeepAlive yes`，ssh还是会断开，是因为中间存在防火墙，防火墙会定时关闭闲置的连接，服务器端有可能有防火墙，客户端或者中间的路由器都有可能有

所以要想保持ssh连接，还是需要设置`ClientAliveInterval`和`ClientAliveCountMax`，这两个设置的含义是，服务器会定期\(`ClientAliveInterval`\)向客服端发送消息，等待客户端响应，然后保持连接，如果没有响应超过`ClientAliveCountMax`次，就关闭连接

使用下面其中一种方法即可解决

1. 修改服务器配置

   `/etc/ssh/sshd_config`

   ```
   TCPKeepAlive yes
   ClientAliveInterval 30
   ClientAliveCountMax 3
   ```

   然后重启ssh，`sudo /etc/init.d/ssh restart`

2. 修改客户端配置

   `~/.ssh/config`

   ```
   Host *
    ServerAliveInterval 30
    ServerAliveCountMax 3
   ```

   或者，`ssh -o ServerAliveInterval=30 -o ServerAliveCountMax=3 <host>`



