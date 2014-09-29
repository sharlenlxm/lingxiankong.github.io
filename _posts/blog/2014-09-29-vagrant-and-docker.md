---
layout: post
title: 浅析vagrant和docker
description: 浅析vagrant和docker
category: blog
---

声明：  
本博客欢迎转发，但请保留原作者信息!  
新浪微博：[@孔令贤HW](http://weibo.com/lingxiankong)；   
博客地址：<http://lingxiankong.github.io/>  
内容系本人学习、研究和总结，如有雷同，实属荣幸！

---

什么是 vagrant ? Vagrant 是一个跨平台的虚拟机构建工具，能够通过 vagrantfile 描述虚拟机并将其部署到 hypervisor 上（VirtualBox, VMWare, AWS, etc）。

什么是 docker ? Docker 是一个 linux 上的 linux container 构建工具，能够通过 dockerfile 来定义一个 container ，并将其部署到任何运行 docker 的主机上。

Vagrant 和 docker 都能够通过一个配置描述文件来构造一个运行环境。

再来看 vagrant 和 docker 的一些差异：  
![](/images/2014-09-29-vagrant-docker/1.png)

docker其他的优势：

* 轻量级的隔离环境比虚拟机能够更方便和快捷地启动和停止；
* 可以在一个虚拟机中运行多个 container，从而节省开销；
* Docker 的 container 机制更适合一些持续集成/持续发布和微型 PaaS 场景。

正是因为两者相比差异颇多，具体用哪一个需要结合特定的使用场景，不能一概而论。但虚拟化爱好者似乎不愿意看到两个宝贝争的你死我活，于是一些人将两者的优势结合，想了一种同时使用两者的使用场景。一个典型场景如下（摘自[这里](https://medium.com/@_marcos_otero/docker-vs-vagrant-582135beb623)）：

* Install a Vagrant virtual machine in your computer containing the same OS you will have in your server ( normally Ubuntu Linux 12.04 LTS 64 bits). This means that you can program in any OS you want and still expect your program will run in your server.
* Install your Docker packages to create Docker containers inside your virtual machine created for Vagrant. This step is better if you can install them through an script.
* Inside your containers put your applications ( Nginx, Memcached, MongoDB, etc)
* Configure a shell script, Puppet or Chef script to install Docker and run your Docker containers each time Vagrant begins.
* Test your containers in your Vagrant VM inside your computer.
* Thanks to providers now you can take the same file ( your Vagrant file ) and just type vagrant up —provider=“provider” where the provider is your next host and Vagrant will take care of everything. For example, if you choose AWS then Vagrant will: Connect to your AMI in AWS, install the same OS you used in your computer, install Docker, launch your Docker containers and give you a ssh session.
* Test your containers in AWS and look that they behave exactly as you expect.

未完待续。