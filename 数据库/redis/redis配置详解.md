.conf文件在etc里面





![image-20240809151412548](redis命令.assets/image-20240809151412548.png)

默认是127.0.0.1，即只能本地上访问，学的时候0.0.0.0

![image-20240809150310963](redis命令.assets/image-20240809150310963.png)

yes即可后台运行

![image-20240809150814827](redis命令.assets/image-20240809150814827.png)

requirepass  密码

![image-20240809150948189](redis命令.assets/image-20240809150948189.png)

端口，如果没有冲突占用可以直接用默认的6379

![image-20240809151033631](redis命令.assets/image-20240809151033631.png)

工作目录，即在这个目录下才能使用命令

![image-20240809151150323](redis命令.assets/image-20240809151150323.png)

设置占用的最大内存

![image-20240809151232293](redis命令.assets/image-20240809151232293.png)

生成日志文件 如果不带路径就是在上面dir工作目录里面