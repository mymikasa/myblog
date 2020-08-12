---
title: ssh 快捷登陆
date: 2020-08-12 21:09:18
tags: ssh
---


### ssh-copy-id命令
ssh-copy-id命令可以把本地主机的公钥复制到远程主机的authorized_keys文件上，ssh-copy-id命令也会给远程主机的用户主目录（home）和~/.ssh, 和~/.ssh/authorized_keys设置合适的权限。

### 语法

```
ssh-copy-id [-i [identity_file]] [user@]machine

# eg:
ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```


### ssh 别名登录

通常我们在 Termianl 下用 ssh 链接远程主机的时候，每次都需要输入一长串的用户名加主机地址，是不是觉得很麻烦？那么好吧，这个 Tips 也需能帮你解决这一烦恼。

我们知道在 /etc/ssh/ 目录下通常都会有 ssh_config 和 sshd_config 这两个文件，前面一个是 ssh 客户端配置文件，后面一个则是服务器端配置文件，而这两个都是应用到系统全局的。而我们要做的就是在 ssh_config 中通过 Host 参数来配置远程 ssh 主机的别名，这样就可以方便快速的进行远程登录了。

当然也可以只应用于当前用户，那么这个配置项应该写在 ~/.ssh/config 文件中，如果这个文件中没有的话就自已创建一个。

现在就开始设置主机别名，在 /etc/ssh/ssh_config 或 ~/.ssh/config 中输出以下行

注：config文件同样需要是600权限，用chmod 600 config修改

```shell
Host www
    HostName www.ttlsa.com
    Port 22
    User root
    IdentityFile  ~/.ssh/id_rsa.pub
    IdentitiesOnly yes

Host bbs
    HostName 115.28.45.104
    User anotheruser
    PubkeyAuthentication no
```

+ 选项注释：
  + HostName 指定登录的主机名或IP地址
  + Port 指定登录的端口号
  + User 登录用户名
  + IdentityFile 登录的公钥文件
  + IdentitiesOnly 只接受SSH key 登录
  + PubkeyAuthentication 公钥认证


参考文章： https://blog.csdn.net/zhanlanmg/article/details/48708255
