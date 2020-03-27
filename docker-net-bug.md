# docker容器映射的端口不能访问

# 场景与现象
vmware虚拟机中运行的系统(centos/ubuntu, nat模式)中安装docker, docker容器1映射的端口，容器2不能访问，外面主机也不能访问。 

ubuntu
=======
1. 需要安装firewalld
```
  apt install firewalld
```
2. 添加路由
```
  # 已验证, 马上就生效了
  firewall-cmd --permanent --zone=trusted --add-interface=docker0
  
  # 未验证
  firewall-cmd --permanent --zone=trusted --add-port=xxxx/tcp  #xxxx改为你希望的端口号
  firewall-cmd --reload  


  #未验证， 开放端口 
  sudo ufw  allow 8321
  ufw allow out on docker0 from 172.17.0.0/16
  ufw allow out on docker0 from 172.17.0.0/16 port 80 proto tcp

```

centos
========

1.  在/etc/firewalld/zones/public.xml添加防火墙规则

>| 已验证 
```
<rule family="ipv4">
  <source address="172.17.0.0/16" />
  <accept />
</rule>
```
 注意这里的 172.17.0.0/16 可以匹配 172.17.xx.xx IP 段的所有 IP.
 之后重启下防火墙
``` 
systemctl restart firewalld
```
之后就可以在 docker 容器内部访问宿主机端口了. 

2. 未验证
```
#1. 开放端口命令： 
iptables -I INPUT -p tcp --dport 9876 -j ACCEPT
iptables -A INPUT -p tcp --dport 2377 -j ACCEPT    
#或者
iptables -t nat -A POSTROUTING -s 172.17.0.0/16 ! -o docker0 -j MASQUERADE

#2. 保存：
/etc/rc.d/init.d/iptables save
              

#3. 重启服务：
/etc/init.d/iptables restart

```
