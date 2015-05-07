#多站点服务器自动化部署lv1

##Requirment
> * ubuntu trusty
> * git

**完成python3,virtualenv,uwsgi,nginx,pip3**

##Usage

 
```bash
$ source autohost
```

#多站点服务器自动化部署lv2

##Requirment
> * python3.4
> * pip
> * uwsgi
> * nginx
> * virutalenv

**完成django服务器环境**

##Usage

**lv2** 
```bash
$ source autoserver project
```
**删除autoserver**

```bash
$ source autoserver rmself
```
**删除uwsgi和nginx相关配置文件**

```bash
$ source autoserver rmconfig
```



#多站点服务器自动化部署lv3


##Requirment
> * api 接口


**完成静态页面部署**




#Rule

> * django的服务端的配置放在settings_loca.py (自动创建)
> * django的settings.py 增加  **STATIC_ROOT = os.path.join(BASE_DIR,  'static')** 和 **MEDIA_ROOT = os.path.join(BASE_DIR,  'upload') **
> * uwsgi 总的 log 放在 /var/log/uwsgi.log
> * uwsgi 子项目的 log 放在 /var/log/uwsgi/ xx.log



#Future

> * autohost 增加自定义apt-get包 





