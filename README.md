# notes
# GFW
> tracert
# port

> netstat -na | findstr "port"

>> -n或--numeric 直接使用IP地址，而不通过域名服务器。

>> -a或--all 显示所有连线中的Socket。
# stat all port-states
> [netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'](http://blog.51cto.com/stephenzhao/658587)


# goroot
> mklink \d <DIR_UNDER_$GOPATH>  <REAL_DIR>

# how to install fucking-mysql-on-docker

## Pull the image
    > docker pull mysql-server
    
## Install the fucking-mysql-server
    > docker run -p <LOCAL_ADDRESS_PORT>:3306 --name <C_NAME> -e MYSQL_ROOT_PASSWORD=<PASSWORD> -d mysql/mysql-server:<VERSION>
    
### example
    > docker run -p 3306:3306 --name sasql -e MYSQL_ROOT_PASSWORD=000000  -d mysql/mysql-server

### Start as service
    > docker ... --restart=always

### MARKDOWN
     -e <ENV_KEY=ENV_VALUE>
     
## Enter mysql cmd mode
    > docker exec -it <C_NAME> mysql -u root -p
    
### example
    > docker exec -it sasql mysql -u root -p

## Allow remote connection
    > show databases;
    > use mysql;
    > show tables;
    > SELECT * FROM user;
    > UPDATE user SET host = '%' WHERE user = 'root';
    > FLUSH PRIVILEGES;

## if 1251 occurs...
    > ALTER USER '<USER>'@'<HOST>' IDENTIFIED WITH mysql_native_password BY '<PASSWORD>';




# some fucking-docker-tips
## Orders does matter!!!!!!!!
    > docker run <IMAGE> --link <CONTAINER_NAME>:<ALIAS>
    
*`--link <CONTAINER_NAME>:<ALIAS>` is useless!* please do
    
    > docker run --link <CONTAINER_NAME>:<ALIAS> <IMAGE> 
    
## Run in background
    > docker run -d
        
## docker volume
    > docker volume create --name <VOLUME_NAME>
    
## Listing only stopped containers
    > docker ps --filter "status=exited"
    > docker ps -a

## Stop the container
    > docker stop <CONTAINER_ID>

## Start the exited container
    > docker start <CONTAINER_ID>

## Remove docker containers
    > docker rm <container_id>
    
## Remove all stopped containers
    > docker rm $(docker ps --filter "status=exited" -q)
    
## Get ip address of one container
    > docker inspect <CONTAINER_ID> | grep "IPAddress"
    
## Get all ports that are being listened on
    > netstat -an | find "<YOUR_PORT>"
    
## Remove image by id
    > docker rmi <IMAGE_ID>
    
## Remove all images
    > docker rmi $(docker images -q)
    
# docker compose
    > volumes: 
        -[HOST:CONTAINER] 
        
# docker mongo
    >  docker run --name ch-mongo -v /my/own/datadir:/data/db -d -p 1994:27017 -e MONGO_INITDB_ROOT_USERNAME=sunao -e MONGO_INITDB_ROOT_PASSWORD=root mongo 
    
# linkers
[好文章](http://blog.jobbole.com/96225/)

# ./configure make & make install
[ref](https://robots.thoughtbot.com/the-magic-behind-configure-make-make-install)

# tips4virtualbox
1. change MAC address when use some copied-vdi

# tips4golang
1. `fmt.Println(t.Format("20060102150405"))` where `20060102150405` is when golang was created

# killALL
1. ps -ef | grep "sunao.*\-bash" | awk '{print $2}' | xargs kill -9

# VNC-server 黑屏
use -localhost=no

# port forwarding(tcp)
1. 开启forwading
    > sysctl net.ipv4.ip_forward=1
2. 转发
    > iptables -t nat -A PREROUTING -p tcp -d IP --dport PORT -j DNAT --to-destination THOST:TPORT
3. 开启
    > iptables -t nat -A POSTROUTING -j MASQUERADE

*-d省略是localhost

# 改变table的编码(docker-mysql的坑)
    > ALTER TABLE table-name CONVERT TO CHARACTER SET utf8;
# celery的坑
```
OSError: Socket closed in celery worker 
```
```python
app = Celery(
    'myapp',
    broker='amqp://guest@localhost//',
)
app.conf.broker_heartbeat = 0
```
works like a charm

# 大便的meteor
速度太慢,加hosts
> 54.192.225.217 warehouse.meteor.com

# 内外网的沟通
默认走外网
> route add -net 0.0.0.0/0  <外网的Ifacey> 

> route add -net 0.0.0.0/0 gw <外网的GateWay>

特殊的走内网
> route add -net 192.168.203.0/24  <内网的Ifacey> 

> route add -net 192.168.203.0/24 gw <内网的GateWay>

查看route table确认
> route table


