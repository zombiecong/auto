# 多站点服务器自动化部署lv1

## Requirment
> * ubuntu trusty
> * git

## Achievement

> * lv1实现主机部署
> * apt-get 默认自动化安装 python3.4-dev, nginx , gcc , python3-setuptools ,  python3-pip   
> * pip3 默认自动化安装 uwsgi, virtualenv 

## Usage

可在配置文件cfg.ini中,自定义额外的apt-get 和pip 需要安装的包,格式为:

	add_apt="x1 x2"
	add_pip="x1 x2"


 
```bash
$ git clone http://learning-tech.com:8901/lt/auto.git
$ cd auto/host
$bash auto
```
安装完后,输入 y 重启系统

# 多站点服务器自动化部署lv2

## Requirment
> * python3.4
> * pip
> * uwsgi
> * nginx
> * virutalenv



## Achievement

> * lv2实现服务器部署
> * 创建虚拟环境
> *  添加本地配置文件settings_local.py
> * 安装requirement.txt
> * 集合静态文件 (可选)
> * 创建uwsgi 配置文件 
> * 创建nginx 配置文件



## Usage

自动化配置 server
```bash
$ source autoserver path-to-project
```

**删除uwsgi和nginx相关配置文件**(/etc/nginx/site-enabled和/etc/uwsgi/site-enabled里的配置文件)

```bash
$ source autoserver rmconfig
```



# 多站点服务器自动化部署lv3


## Requirment
> * api 接口


**完成静态页面部署**


## Rule

> * project/app/settings.py ,保证 project 和 app的文件夹名相同
> * django的服务端的配置放在settings_loca.py (自动创建)
> * django的settings.py 增加  **STATIC_ROOT = os.path.join(BASE_DIR,  'static')** 和 **MEDIA_ROOT = os.path.join(BASE_DIR,  'upload') **
> * uwsgi 总的 log 放在 /var/log/uwsgi.log
> * uwsgi 子项目的 log 放在 /var/log/uwsgi/ xx.log









