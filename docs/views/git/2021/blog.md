---
title: git添加一个ed25519的key
date: 2021-07-11
tags:
- git
  
categories:
- git
---
直接看官方文档:
[generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent](https://docs.github.com/cn/github-ae@latest/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
### &emsp;&emsp; 困扰了很久,我自己生成的ed25519的key不能用来拉去代码,就会报权限错误
#### &emsp;&emsp;有一次看到同事还在用密码去拉取代码,就想着帮他生成一个ed25519的key去拉取代码,生成key的时候还是很顺利的.
#### &emsp;&emsp;就是key在.ssh文件里躺着,gitlab的设置里也是添加了这个key的公钥但是拉去代码就是权限不足
#### &emsp;&emsp;我一直以为sshkey只要生成了就自动会作为拉取代码时候的验证,其实不是,还要添加到ssh-agent.


#### &emsp;&emsp;git的默认生成key的方式会在.ssh文件夹下生成两个 id_ras id_ras.pub

#### &emsp;&emsp;就可以用这两个key去完成验证

#### &emsp;&emsp;现在用更高性能而且更简短的ed25519算法生成密钥然后添加到ssh-agent

```shell
1. 生成密钥 直接全部默认,就是无密码的,也可以根据提示设置密码,生成的位置使用默认位置
ssh-keygen -t ed25519 -C "your_email@example.com"
2. 启动ssh-agent,这样才能使用ssh-add命令把ed25519添加到验证里
$ eval "$(ssh-agent -s)"
3. 添加ssh key  这里就是一个路径,文件名看自己设置的什么
ssh-add ~/.ssh/id_ed25519
```
