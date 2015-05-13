# 多站点服务器自动化部署

## 目的

本程序通过自动化脚本和相应的配置文件，实现Ubuntu系统上各类Python/Django站点的快速部署。

使用上，首先需要在Ubuntu服务器上**一次性**下载和初始化本程序，完成一次第一层部署。随后可参考第二层和第三层，对每个独立的子站点进行配置。
针对每一个子站点的配置规范，请查看最后一节：**自动部署的子站点项目文件和目录规范**

## 第一层：服务器初始化

### 依赖环境
> * Ubuntu 14.04 Server LTS (Trusty)
> * Git

通过以下命令安装本程序，并进行服务器初始化，
 
```bash
$ git clone http://learning-tech.com:8901/lt/django_auto_deploy.git
$ cd django_auto_deploy/host
$ bash auto
```
安装完后,输入 y 重启系统。

### 实现结果

> * 实现本系统进行多站点自动配置所需的服务器环境部署，包括Python服务器，包管理器，以及反向代理
> * 默认通过 apt-get 自动安装 python3.4-dev, python3-setuptools, python3-pip, nginx 和 gcc
> * 默认通过 pip3 自动安装 uwsgi, virtualenv


## 第二层：部署一个新的子站点

### 依赖环境

* 以下依赖环境可通过执行第一层自动完成 *

> * python3.4
> * pip
> * uwsgi
> * nginx
> * virutalenv

### 部署方法

1. 将欲部署的Django项目复制到名为[project-dir]  (project的父目录名) 的目录

2. 使用本程序，初始化名称为[project-name]的子站点于给定的[project-dir]目录

```bash
$ cp -r django_auto_deploy/server/* [project-dir]
$ cd [project-dir]
$ source auto [project-name]
```

3. 自动配置完成后，执行以下命令，删除本程序自身文件

```bash
$ source auto rmself
```

4. 如果配置错误或需要重新配置子站点，执行以下命令，删除配置文件

```bash
$ source auto rmconfig
```

### 使用方法

如果需要额外增加自定义包,可在配置文件host/config.ini中，修改以下两行配置，以添加需要通过 apt-get 和 pip 额外安装的软件包，
* 注意：等号前后**不可以**添加空格 *

	add_apt="x1 x2"
	add_pip="x3 x4"


### 实现结果

> * 总体上，实现Django程序的一键部署到服务器。具体包括：
> * 创建Python虚拟环境到 [project-dir]/[project-name.virtualenv]
> * 自动添加Django服务器端的本地配置文件settings_local.py
> * 安装pip包文件requirement.txt
> * 收集静态文件
> * 创建uwsgi服务配置文件到[project-dir]/[project-name]_uwsgi.ini
> * 创建Nginx站点配置文件到[project-dir]/[project-name]_nginx.conf
> * 自动启动以上配置


## 第三层：静态文件配置

### 依赖环境
> * API 接口

**完成静态页面部署**


## 自动部署的子站点项目文件和目录规范

> * 对于Django默认的项目结构project/app/settings.py，需要保证 project 和 app 两个父子文件夹名相同
> * Django的settings.py文件中需要增加以下两行，以保证静态文件的正确部署，

    ```python
    STATIC_ROOT = os.path.join(BASE_DIR,  'static') 
    MEDIA_ROOT = os.path.join(BASE_DIR,  'upload')
    ```
    
> * 自动部署子站点后，Django的服务端的配置文件将存储于自动生成的settings_local.py

> * 因此，开发者也可以在Django的[project-name]/[project-name]/settings.py文件的最后一行增加，

    ```python
    from settings_local.py import *
    ```
    
    并在开发者本地的settings_local.py文件中覆盖settings.py中的配置。

> * uwsgi 的总体日志存储在 /var/log/uwsgi.log

> * uwsgi 子项目的日志存储在 /var/log/uwsgi/project-name.log




