# agricultural_bot
Steps:

1. Launch EC2 instance and install docker inside and start docker Service:
Use following Commands:
       sudo su - root               
        yum install docker -y
        systemctl enable  docker --now
        systemctl status docker

   ![Screenshot 2023-08-30 181908](https://github.com/pratikshashinde55/agricultural_bot/assets/61465971/c919913b-aa92-448a-97f3-7a61165a0451)

2.create own net name as "psnet"
        subnet range 10.0.0.1/16 in CIDR format
        
  ![Screenshot 2023-08-30 185447](https://github.com/pratikshashinde55/agricultural_bot/assets/61465971/bc2e8ddd-5f80-42f6-90a4-0f44bc5607be)
      

#docker network ls
#docker network create --driver bridge --subnet 10.0.0.1/16  psnet
#docker network ls



3. Create database with own driver (database- container name)...also provide required enviromental variable

 ![Screenshot 2023-08-30 185342](https://github.com/pratikshashinde55/agricultural_bot/assets/61465971/2e1f0892-4059-4b02-b876-f91907d4bd7b)

#docker run -dit --name database --network psnet -v /mydata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=pratik55  -e MYSQL_DATABASE=mydatabase  -e MYSQL_USER=jack  -e MYSQL_PASSWORD=jack11 mysql

#docker inspect database   <--- here we show our subnet range(10.0.0.1/16) to our given database container

![Screenshot 2023-08-30 185033](https://github.com/pratikshashinde55/agricultural_bot/assets/61465971/0188840f-d021-4d93-b3dc-acb4f5951ddd)
![Screenshot 2023-08-30 185149](https://github.com/pratikshashinde55/agricultural_bot/assets/61465971/491672f9-612e-4480-9fef-48cfd2c61920)

Here,check provided subnet range.

4.Launch wordpress and uase PATTING to make outside world connection 
 As port number of container is 80 also check by #netstat -tnlp
 
 ![Screenshot 2023-08-30 185418](https://github.com/pratikshashinde55/agricultural_bot/assets/61465971/67b0ad62-3774-4f05-baf9-d3c8ad45305a)

  
  #docker run -dit --name mywordpress --network psnet -p 1234:80 wordpress

we can also check MYWORDPRESS has our subnet range by command on above screenshots.( step no.3)
#docker inspect mywordpress

5.EC2 intance has Firewall which cannot be connected by outside world, so we can modify inbound rules(All traffic allowed)

![Screenshot 2023-08-30 182129](https://github.com/pratikshashinde55/agricultural_bot/assets/61465971/f5cb4732-1715-4a23-89da-92f825f1ec81)

Substeps
     1. : EC2 Dashboard 
     2. select securtity option 
     3. go inside Security groups
     4. select "edit inbound rule"
     5. delete defult rule and new rule
     5. custom TCP ->> "ALL TRAFIC" ,ANYWHERE IPv4
     6. save rule


     we use instance public + our port number that provide in wordpress contanierb 
  http://65.2.146.158:1234  <<---- on google or browser

we get wordprss interface on google , we provide details that we provide  in the for of enviromental variable during lauching "database" caintainer 

http://65.2.146.158:1234 <<------- show our blog



 
