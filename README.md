# agricultural_bot

Use following Commands:
       sudo su - root               
        yum install docker -y
        systemctl enable  docker --now
        systemctl status docker
create own net name as "psnet"
        subnet range 10.0.0.1/16 in CIDR format
        

#docker network ls
#docker network create --driver bridge --subnet 10.0.0.1/16  psnet
#docker network ls

 Create database with own driver (database- container name)...also provide required enviromental variable
 
#  docker run -dit --name database --network psnet -v /mydata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=pratik55  -e MYSQL_DATABASE=mydatabase  -e MYSQL_USER=jack  -e MYSQL_PASSWORD=jack11 mysql

#docker inspect database   <--- here we show our subnet range(10.0.0.1/16) to our given database container
