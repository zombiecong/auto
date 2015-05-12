# 多站点服务器自动化部署

## 目的

本程序通过自动化脚本和相应的配置文件，实现Ubuntu系统上各类Python/Django站点的快速部署。

使用上，首先需要在Ubuntu服务器上*一次性*下载和初始化本程序，完成一次第一层部署。随后可参考第二层和第三层，对每个独立的子站点进行配置。

## 第一层：服务器初始化

### 依赖环境
> * Ubuntu 14.04 Server LTS (Trusty)
> * Git

### 使用方法

可在配置文件config.ini中，修改以下两行配置，以添加需要通过 apt-get 和 pip 额外安装的软件包，

	add_apt="x1 x2"
	add_pip="x3 x4"

通过以下命令安装本程序，并进行服务器初始化，
 
```bash
$ git clone http://learning-tech.com:8901/lt/auto.git
$ cd auto/host
$ bash auto
```
安装完后,输入 y 重启系统。

### 实现结果

> * 实现本系统进行多站点自动配置所需的服务器环境部署，包括Python服务器，包管理器，以及反向代理
> * 默认通过 apt-get 自动安装 python3.4-dev, python3-setuptools, python3-pip, nginx 和 gcc
> * 默认通过 pip3 自动安装 uwsgi, virtualenv


## 第二层：子站点部署

### 依赖环境

* 以下依赖环境可通过执行第一层自动完成 *
> * python3.4
> * pip
> * uwsgi
> * nginx
> * virutalenv

### 部署方法

1. 将欲部署的Django项目复制到名为[project-dir]的目录

2. 使用本程序，初始化名称为[project-name]的子站点于给定的[project-dir]目录

```bash
$ cp auto/server/* [project-dir]
$ cd [project-dir]
$ source auto create [project-name]
```

3. 自动配置完成后，删除本程序自身文件

```bash
$ source auto rmself
```

### 实现结果

> * 总体上，实现Django程序的一键部署到服务器。具体包括：
> * 创建Python虚拟环境到 [project-dir/project-name.virtualenv]
> * 自动添加Django服务器端的本地配置文件settings_local.py
> * 安装pip包文件requirement.txt
> * 收集静态文件
> * 创建uwsgi服务配置文件 
> * 创建Nginx站点配置文件
> * 自动启动以上配置


## 第三层：静态文件配置


### 依赖环境
> * API 接口


**完成静态页面部署**



## 自动部署的项目文件和目录规范

> * project/app/settings.py ,保证 project 和 app的文件夹名相同
> * django的服务端的配置放在settings_local.py (自动创建)
> * django的settings.py 增加  **STATIC_ROOT = os.path.join(BASE_DIR,  'static')** 和 **MEDIA_ROOT = os.path.join(BASE_DIR,  'upload') **
> * uwsgi 总的 log 放在 /var/log/uwsgi.log
> * uwsgi 子项目的 log 放在 /var/log/uwsgi/ xx.log


1. 对于欲部署的Django项目，
	
	1.1 在项目[project-name]/[project-name]/settings.py中，添加以下语句引用本地配置文件
	
	```Python
	from .settings_local import *
	```






