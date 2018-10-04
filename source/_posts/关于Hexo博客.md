---
Ntitle: 关于Hexo博客
date: 2018-10-04 16:01:17
tags:
	- Hexo
	- Hexo主题
	- Hexo备份
---

![just a pic](http://oumh6gonh.bkt.clouddn.com/18-10-4/16476369.jpg)



### 本文:

- [Hexo博客的搭建](#hexo)
- [Hexo博客主题Yilia的安装配置](#theme)
- [Hexo推送到Github的配置](#github)
- [Hexo源文件的备份](#bak)
- [遇到的一些问题](#question)

<h3 id="hexo">Hexo博客的搭建</h3>

1.Install Hexo  

```shell
$ brew install npm 
$ sudo npm install -g hexo-cli
$ hexo -v
 ....
```

2.Create a project

```shell 
$ hexo init btainleer.github.io
  ......
$ cd btainleer.github.io
$ npm install
```

3.Run a test.

```shell
$ hexo server
  Info Hexo is running at http://0.0.0.0:4000/
```

4.此时，浏览器访问 http://localhost:4000 就能看到 Hello,world 文章了吧。

<h3 id="theme">Hexo博客主题Yilia的安装配置</h3>  

1.Download hexo theme yilia  

```shell 
$ pwd
 xxxx/btainlee.github.io  #在博客根目录
$ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
$ cd themes/yilia
$ git pull
```

2.Active themes yilia  

```shell
btainleer.github.io:_config.yml  
	theme: yilia
```

3.Modify themes config file：btainleer.github.io/themes/yilia/_config.yml  

4.Preview new Blog  

```shell 
$ pwd
btainleer.github.io
$ hexo clean
...
$hexo deploy
...
$hexo sever
...
```

5.此时，浏览器访问 http://localhost:4000 就能看到 新的主题了吧。  

<h3 id="github">Hexo推送到Github的配置</h3>  

1.在Github创建一个Repository。命名方式为 username.github.io。如我的用户名是btainleeR,则我的Repository名称为 btainleeR.github.io。

2.配置Hexo的配置文件（非主题的配置文件）。 

```shell 
deploy:
	type: git
	repo: git@github.com:UserName/UserName.github.io.git
	branch: master
```

3.安装自动同步插件 

```shell
$pwd
btainlee.github.io
$ npm install --save hexo-deployer-git
```

4.生成Git秘钥公钥。 

```
$ ssh_keygen
...
$ cd ~/.ssh
$ vim id_rsa.pub
#复制该文件所有内容，转第五步
```

5.将复制的公钥添加到Github账户的SSH keys中。

​	点击头像>setting>SSH and GPG keys>New SSH key>粘贴   

6.推动到github  

```shell
$ pwd 
btainleer.github.io
$ hexo clean
...
$ hexo deploy
...
```

7.此时，浏览器访问 https://Username.github.io就能看到 网站了吧。【Username为github用户名】  



<h3 id="bak">Hexo源文件的备份</h3>  











  





 