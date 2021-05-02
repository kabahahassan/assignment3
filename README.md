### Assignment3 - AWS EC2 & VPC

##first creating our network: 
####Creating VPC: 

![](https://github.com/kabahahassan/assignment3/blob/main/screenshot/vpc.png?raw=true)

####Creating subnets:
![](https://github.com/kabahahassan/assignment3/blob/main/screenshot/subnets.png?raw=true)

####Internet Gateway:
![](https://github.com/kabahahassan/assignment3/blob/main/screenshot/internet-gateway.png?raw=true)


####NAT Gateway:
![](https://github.com/kabahahassan/assignment3/blob/main/screenshot/NAT.png?raw=true)

####Route Tables:
**public route table:**
![](https://github.com/kabahahassan/assignment3/blob/main/screenshot/public-route-table.png?raw=true)

**private route table:** 

![](https://github.com/kabahahassan/assignment3/blob/main/screenshot/private-route-table.png?raw=true)


**after we created VPC network, we created 2 EC2 instaces as described: **

![](https://github.com/kabahahassan/assignment3/blob/main/screenshot/instances.png?raw=true)

| instance  | word2  | data2 |
| :------------ |:---------------:| -----:|
| for:     | wordpress | mysql |
| files      | docker-compose-wordpress.yml        |   docker-compose-mySQL.yml |
|  |      |   | |

** docker-compose-wordpress.yml : **
```
version: '3.7'
services:
    wordpress:

        image: wordpress:latest

        ports:
            - "8080:80"
        restart: always
        environment:
            WORDPRESS_DB_HOST: 10.88.2.117
            WORDPRESS_DB_USER: wordpressuser
            WORDPRESS_DB_PASSWORD: wordpress
            WORDPRESSS_DB_NAME: wordpress
```

** docker-compose-mySQL.yml : **
```
version: '3.7'
volumes:
    mysql_data:

services:
    database:
        image: mysql:5.7
        volumes:
            - mysql_data:/var/lib/mysql
        ports:
            - "3306:3306"
        restart: always
        environment:
            MYSQL_ROOT_PASSWORD: mypassword
            MYSQL_DATABASE: wordpress
            MYSQL_USER: wordpressuser
            MYSQL_PASSWORD: wordpress
```

we run the Docker-compose on both servers :
`$ docker-compose up -d `

after that we browse to : 
http://{wordpress-server-ip}:8080

![](https://github.com/kabahahassan/assignment3/blob/main/screenshot/wordpress.png?raw=true)


