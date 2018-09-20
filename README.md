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

