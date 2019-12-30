# DevOps-Docker-course
 Avo_Kousa_AYTKT21025en_lv2019

## Part 1
### [Exercise 1.1](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_1/1_1.txt)
```
➜ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
7f8f7bdc0440        nginx               "nginx -g 'daemon of…"   2 minutes ago       Up 2 minutes                80/tcp              nervous_rosalind
1b9e15388384        nginx               "nginx -g 'daemon of…"   2 minutes ago       Exited (0) 12 seconds ago                       brave_elion
e48d6ecb7374        nginx               "nginx -g 'daemon of…"   2 minutes ago       Exited (0) 31 seconds ago                       eager_driscoll
```

### [Exercise 1.2](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_1/1_2.txt)
```
DevOps-Docker-course on  master [?] 
➜ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
DevOps-Docker-course on  master [?] 
➜ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

### [Exercise 1.3](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_1/1_3.txt)
```
➜ docker run -it devopsdockeruh/pull_exercise
Unable to find image 'devopsdockeruh/pull_exercise:latest' locally
latest: Pulling from devopsdockeruh/pull_exercise
8e402f1a9c57: Pull complete 
5e2195587d10: Pull complete 
6f595b2fc66d: Pull complete 
165f32bf4e94: Pull complete 
67c4f504c224: Pull complete 
Digest: sha256:7c0635934049afb9ca0481fb6a58b16100f990a0d62c8665b9cfb5c9ada8a99f
Status: Downloaded newer image for devopsdockeruh/pull_exercise:latest
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

### [Exercise 1.4](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_1/1_4.txt)
```
➜ docker run devopsdockeruh/exec_bash_exercise
Unable to find image 'devopsdockeruh/exec_bash_exercise:latest' locally
latest: Pulling from devopsdockeruh/exec_bash_exercise
...

➜ docker exec -it recursing_jepsen bash
root@f20ddc63764c:/usr/app# tail -f ./logs.txt
Thu, 19 Sep 2019 10:24:03 GMT
Thu, 19 Sep 2019 10:24:06 GMT
Thu, 19 Sep 2019 10:24:09 GMT
Thu, 19 Sep 2019 10:24:12 GMT
Secret message is:
"Docker is easy"
```

### [Exercise 1.5](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_1/1_5.txt)
```
➜ docker run -d -it --name hki ubuntu:16.04

➜ docker exec -it hki bash

root@88e74c473135:/# apt-get update; apt-get install curl 

root@88e74c473135:/# sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body></html>
```

### [Exercise 1.6](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_1/1_6)
Dockerfile:
```
FROM devopsdockeruh/overwrite_cmd_exercise

CMD ["--clock"]
```
Commands:
```
➜ docker build -t docker-clock .

...

➜ docker run docker-clock
```

### [Exercise 1.7](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_1/1_7)
Dockerfile:
```
FROM ubuntu:16.04 

RUN apt-get update && apt-get install -y curl 
COPY script.sh .
RUN chmod +x script.sh

ENTRYPOINT ["./script.sh"]
```
Commands:
```
➜ docker build -t curler .

...

➜ docker run -it curler
```
Output:
```
Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body></html>
```
Script:
```
#!/bin/bash
echo "Input website:";
read website;
echo "Searching..";
sleep 1;
curl http://$website;
```

### [Exercise 1.8](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_1/1_8)
Commands and output:
```
➜ touch logs.txt
...

➜ docker run --name bind -v $(pwd)/logs.txt:/usr/app/logs.txt devopsdockeruh/first_volume_exercise                                                    
(node:1) ExperimentalWarning: The fs.promises API is experimental
Wrote to file /usr/app/logs.txt
Wrote to file /usr/app/logs.txt
Wrote to file /usr/app/logs.txt
Wrote to file /usr/app/logs.txt
```
Logs:
```
Thu, 26 Dec 2019 11:42:46 GMT
Thu, 26 Dec 2019 11:42:49 GMT
Thu, 26 Dec 2019 11:42:52 GMT
Thu, 26 Dec 2019 11:42:55 GMT
Secret message is:
"Volume bind mount is easy"
Thu, 26 Dec 2019 11:43:01 GMT
```

### [Exercise 1.9](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_1/1_9.txt)
```
➜ docker run -p 3000:80 devopsdockeruh/ports_exercise
```

### [Exercise 1.10](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_1/1_10)
Dockerfile:
```
FROM ubuntu:16.04
WORKDIR /usr/src/app
RUN apt-get update
RUN  apt-get -y install curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs
RUN apt-get install -y git
RUN git clone https://github.com/docker-hy/frontend-example-docker.git .
EXPOSE 5000
RUN npm install
CMD ["npm", "start"]
```
Commands:
```  
➜ docker build -t front .

➜ docker run -p 5000:5000 front 

```

### [Exercise 1.11](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_1/1_11)
Dockerfile:
```
FROM ubuntu:16.04
WORKDIR /usr/src/app
RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y git
RUN apt-get install -y nodejs
RUN git clone https://github.com/docker-hy/backend-example-docker.git .
EXPOSE 8000
RUN npm install
CMD ["npm", "start"]
```
Commands:
```
➜ docker build -t back .    

➜ docker run -p 8000:8000 -v $(pwd)/logs.txt:/usr/src/app/logs.txt back
```
Logs:
```
12/26/2019, 12:34:11 PM: Connection received in root
12/26/2019, 12:34:41 PM: Connection received in root
12/26/2019, 12:34:41 PM: Connection received in root
12/26/2019, 12:34:42 PM: Connection received in root
12/26/2019, 12:40:51 PM: Connection received in root
```

### [Exercise 1.12](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_1/1_12)
Backend dockerfile:
```
FROM ubuntu:16.04
WORKDIR /usr/src/app
RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y git
RUN apt-get install -y nodejs
RUN git clone https://github.com/docker-hy/backend-example-docker.git .
EXPOSE 8000
ENV FRONT_URL="http://localhost:5000"
RUN npm install
CMD ["npm", "start"]
```
Frontend dockerfile:
```
FROM ubuntu:16.04
WORKDIR /usr/src/app
RUN apt-get update
RUN  apt-get -y install curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs
RUN apt-get install -y git
RUN git clone https://github.com/docker-hy/frontend-example-docker.git .
EXPOSE 5000
ENV API_URL="http://localhost:8000"
RUN npm install
CMD ["npm", "start"]
```
Commands:
```
➜ docker run -p 5000:5000 front
...

➜ docker run -p 8000:8000 -v $(pwd)/logs.txt:/usr/src/app/logs.txt back
```

### [Exercise 1.13](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_1/1_13)
Dockerfile:
```
FROM openjdk:8
RUN apt-get update && apt-get install -y git
RUN git clone https://github.com/docker-hy/spring-example-project.git
WORKDIR spring-example-project
EXPOSE 8080
RUN ./mvnw package
CMD java -jar ./target/docker-example-1.1.3.jar
```
Commands:
```  
➜ docker build -t button .   

➜ docker run -p 3000:8080 button
```

### [Exercise 1.14](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_1/1_14)
Dockerfile:
```
FROM ruby:2.6.0
WORKDIR /usr/src/app
RUN apt-get update
RUN apt-get install -y git
RUN apt-get install -y nodejs
RUN git clone https://github.com/docker-hy/rails-example-project.git .
RUN gem install bundler
RUN bundle install
EXPOSE 3000
RUN rails db:migrate
CMD rails s
```
Commands:
```  
➜ docker build -t click .      

➜ docker run -p 3000:3000 click
```

### [Exercise 1.15](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_1/1_15.txt)
Link to dockerhub: https://hub.docker.com/repository/docker/sivosam/feedback

### [Exercise 1.16](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_1/1_16.txt)
Link to herokuapp: https://dockers-example.herokuapp.com/


## Part 2

### [Exercise 2.1](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_2/2_1)
docker-compose-yml: 
```
version: '3.5' 

services: 

  first_volume_exercise: 
    image: devopsdockeruh/first_volume_exercise
    build: . 
    volumes: 
      - ./logs.txt:/usr/app/logs.txt
    container_name: first_compose
```
