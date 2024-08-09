1.日志里面没有15672

A：没有开启Rabbit MQ管理插件，15672这个端口是这个插件开启监听的，logs里没有的话可以手动开启

```shell
docker exec -it mq rabbitmq-plugins enable rabbitmq_management
```

2.ubuntu关闭防火墙

- 启用防火墙: `sudo ufw enable`
- 禁用防火墙: `sudo ufw disable`

防火墙的状态查询 `sudo ufw status`



centos关闭防火墙

### **‌[CentOS](https://www.baidu.com/s?wd=CentOS&tn=84053098_3_dg&usm=2&ie=utf-8&rsv_pq=da55b086001b96e5&oq=虚拟机防火墙关闭命令&rsv_t=b141KqEN%2FkkF70Kp%2B92dkdMEb%2FvYSRVqT0G8SY8HDPW4IkeC%2BzTvdnW5yUP8L%2BxeqZTMrw&sa=re_dqa_generate)/Red Hat 系统**

- **firewalld**

  :

  - 启用防火墙: `sudo systemctl start firewalld`
  - 禁用防火墙: `sudo systemctl stop firewalld`
  - 永久关闭防火墙: `sudo systemctl disable firewalld`





```
docker run \
 -e RABBITMQ_DEFAULT_USER=itheima \
 -e RABBITMQ_DEFAULT_PASS=123321 \
 -v mq-plugins:/plugins \
 --name mq \
 --hostname mq \
 -p 15672:15672 \
 -p 5672:5672 \
 --network hm-net\
 -d \
 rabbitmq:3.8-management
```

