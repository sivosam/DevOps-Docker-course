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

### [Exercise 2.2](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_2/2_2)
docker-compose.yml:
```
version: '3.5'

services:
  ports_exercise:
    image: devopsdockeruh/ports_exercise
    ports:
      - 3000:80
```

### [Exercise 2.3](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_2/2_3)
docker-compose.yml:
```
version: '3.5'

services:
  front:
    build: './frontend'
    ports:
      - 5000:5000
    container_name: front
  back:
    build: './backend'
    ports:
      - 8000:8000
    volumes:
      - ./logs.txt:/usr/src/app/logs.txt
    container_name: back
```

### [Exercise 2.4](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_2/2_4)
commands:
```
➜ docker-compose up -d --scale compute=10
```

### [Exercise 2.5](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_2/2_5)
docker-compose.yml:
```
version: '3.5'

services:
  backend:
    image: back
    build: .
    ports:
      - 8000:8000
    environment:
      - REDIS=redis
    container_name: back
  frontend:
    image: front
    build: .
    ports:
      - 5000:5000
    container_name: front
  redis:
    image: redis
    build: .
    ports:
      - 6379:6379
    container_name: redis-backend
```
### [Exercise 2.6](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_2/2_6)
docker-compose.yml:
```
version: '3.5'

services:
  backend:
    image: back
    build: .
    ports:
      - 8000:8000
    environment:
      - REDIS=redis
      - DB_USERNAME=postgres
      - DB_PASSWORD=pass
      - DB_HOST=db
    container_name: back
  frontend:
    image: front
    build: .
    ports:
      - 5000:5000
    container_name: front
  redis:
    image: redis
    build: .
    ports:
      - 6379:6379
    container_name: redis-backend
  db:
    image: postgres
    build: .
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=pass
    container_name: db_postgres
```

### [Exercise 2.7](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_2/2_7)
docker-compose.yml:
```
version: '3.5'

services:
  backend:
    image: ml_backend
    build: .
    ports:
      - 5000:5000
    depends_on:
      - training
    volumes:
      - model:/src/model
    container_name: backend

  frontend: 
    image: ml_frontend
    build: .
    ports:
      - 3000:3000
    container_name: frontend

  training:
    image: ml_training
    build: .
    volumes:
      - model:/src/model
      - imgs:/src/imgs
      - data:/src/data
    container_name: training

volumes:
  model:
  imgs:
  data:
```

### [Exercise 2.8](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_2/2_8)
docker-compose.yml:
```
version: '3.5'

services:
  backend:
    image: back
    build: .
    ports:
      - 8000:8000
    environment:
      - REDIS=redis
      - DB_USERNAME=postgres
      - DB_PASSWORD=pass
      - DB_HOST=db
    container_name: back
  frontend:
    image: front
    build: .
    ports:
      - 5000:5000
    container_name: front
    environment:
      - API_URL=/api
  redis:
    image: redis
    build: .
    ports:
      - 6379:6379
    container_name: redis-backend
  db:
    image: postgres
    build: .
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=pass
    container_name: db_postgres
  proxy:
    image: nginx
    ports:
      - 80:80
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
 ```
nginx.conf:
```
events { worker_connections 1024; }

http {
  server {
    listen 80;

    location / {
      proxy_pass http://front:5000/;
    }

    location /api/ {
      proxy_pass http://back:8000/;
    }
  }
}
```

### [Exercise 2.9](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_2/2_9)
docker-compose.yml:
```
version: '3.5'

services:
  backend:
    image: back
    build: .
    ports:
      - 8000:8000
    environment:
      - REDIS=redis
      - DB_USERNAME=postgres
      - DB_PASSWORD=pass
      - DB_HOST=db
    container_name: back
  frontend:
    image: front
    build: .
    ports:
      - 5000:5000
    container_name: front
    environment:
      - API_URL=/api
  redis:
    image: redis
    build: .
    command: ["redis-server", "--appendonly", "yes"]
    ports:
      - 6379:6379
    volumes:
      - ./data:/data
    
    container_name: redis-backend
  db:
    image: postgres
    build: .
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=pass
    volumes:
      - ./database:/var/lib/postgresql/data
    container_name: db_postgres
  proxy:
    image: nginx
    ports:
      - 80:80
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf

volumes:
 database:
 data:
 ```

### [Exercise 2.10](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_2/2_10)
To get all the buttons to work, docker-compose.yml file needed a frontend environment variable:

environment:
  - API_URL=/api

Since without that, the buttons still pointed to localhost:8000 and not to localhost/api, 
as was needed for nginx to route correctly.

This was actually already done for exercise 2.8 (to get the first button working), 
so no additional changes were needed.


docker-compose.yml:
```
version: '3.5'

services:
  backend:
    image: back
    build: .
    ports:
      - 8000:8000
    environment:
      - REDIS=redis
      - DB_USERNAME=postgres
      - DB_PASSWORD=pass
      - DB_HOST=db
    container_name: back
  frontend:
    image: front
    build: .
    ports:
      - 5000:5000
    environment:
      - API_URL=/api
    container_name: front
  redis:
    image: redis
    build: .
    ports:
      - 6379:6379
    container_name: redis-backend
  db:
    image: postgres
    build: .
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=pass
    container_name: db_postgres
  proxy:
    image: nginx
    ports:
      - 80:80
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
```
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

## Part 3

### [Exercise 3.1](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_3/3_1)
BEFORE OPTIMIZATION:
Frontend image: 532MB
Backend image: 515MB
TOTAL: 1050MB

AFTER OPTIMIZATION:
Frontend image: 487MB
Backend image: 486MB
TOTAL: 973MB

Both include a clone from the respective examples, which might explain the greater file size.

Backend dockerfile:
```
FROM ubuntu:16.04
EXPOSE 8000
ENV FRONT_URL="http://localhost:5000"
RUN apt-get update && apt-get install -y \
	curl git npm && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \
    git init . && \
    git remote add origin https://github.com/docker-hy/backend-example-docker && \
    git pull origin master && \
    npm install npm@latest -g && \
    apt-get purge -y --auto-remove curl git && \ 
    rm -rf /var/lib/apt/lists/*
CMD ["npm", "start"]
```

Frontend dockerfile:
```
FROM ubuntu:16.04
EXPOSE 5000
ENV API_URL="http://localhost:8000"
RUN apt-get update && apt-get install -y \
    curl git npm && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \
    git init . && \
    git remote add origin https://github.com/docker-hy/frontend-example-docker && \
    git pull origin master && \
    npm install npm@latest -g && \
    apt-get purge -y --auto-remove curl git && \
    rm -rf /var/lib/apt/lists/*
CMD ["npm", "start"]
```

### [Exercise 3.2](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_3/3_2)
Commands used:
```
➜ docker build -t yle-dl .

➜ docker run -v "$(pwd)":/videos yle-dl https://areena.yle.fi/1-50288906

yle-dl 20191231: Download media files from Yle Areena and Elävä Arkisto
...
```
Dockerfile:
```
FROM ubuntu:16.04

ENV LC_ALL=C.UTF-8

RUN apt-get update && apt-get install -y \
	python ffmpeg python-pip wget && \
	pip install yle-dl && \
	rm -rf /var/lib/apt/lists/*
	
WORKDIR /videos	
ENTRYPOINT ["yle-dl"]
```

Or....
Alternative, much simpler dockerfile (which feels a bit like cheating, but is half the size of the previous one. Then again, doing it this way does go against the spirit of the exercise):
```
FROM taskinen/yle-dl
WORKDIR /videos
ENTRYPOINT ["yle-dl"]
```
### [Exercise 3.3](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_3/3_3)
Backend dockerfile:
```
FROM ubuntu:16.04
EXPOSE 8000
ENV FRONT_URL="http://localhost:5000"
WORKDIR /app
COPY . .
RUN apt-get update && apt-get install -y \
    curl && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \
    apt-get install -y nodejs && \
    npm install && \
    apt-get purge -y --auto-remove curl && \ 
    rm -rf /var/lib/apt/lists/* && \
    useradd -m app && chown -R app /app
USER app
CMD ["npm", "start"]
```
Frontend dockerfile:
```
FROM ubuntu:16.04
EXPOSE 5000
ENV API_URL="http://localhost:8000"
WORKDIR /app
COPY . .
RUN apt-get update && apt-get install -y \
	curl && \
	curl -sL https://deb.nodesource.com/setup_10.x | bash && \
	apt-get install -y nodejs && \
	npm install && \
	apt-get purge -y --auto-remove curl && \
	rm -rf /var/lib/apt/lists/* && \
	useradd -m app && chown -R app /app
USER app
CMD ["npm", "start"]
```

### [Exercise 3.4](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_3/3_4)
BEFORE OPTIMIZATION: 
Frontend image: 430MB 
Backend image: 332MB 
TOTAL: 762MB

AFTER OPTIMIZATION: 
Frontend image: 266MB 
Backend image: 170MB 
TOTAL: 436MB

Backend dockerfile:
```
FROM node:alpine
EXPOSE 8000
ENV FRONT_URL="http://localhost:5000"
WORKDIR /app
COPY . .
RUN npm install && \
    adduser -S -D app && chown -R app /app
USER app
CMD ["npm", "start"]
```
Frontend dockerfile:
```
FROM node:alpine
EXPOSE 5000
ENV API_URL="http://localhost:8000"
WORKDIR /app
COPY . .
RUN npm install && \
    adduser -D -S app && chown -R app /app
USER app
CMD ["npm", "start"]
```
### [Exercise 3.5](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_3/3_5/frontend)
Dockerfile:
```
FROM node:alpine as build-stage
WORKDIR /app
COPY . .
RUN npm install && \
    npm run build

FROM node:alpine
EXPOSE 5000
ENV API_URL="http://localhost:8000"
WORKDIR /app
COPY --from=build-stage /app/dist/ /app/dist/

RUN npm install -g serve && \
    adduser -D app && chown -R app /app
USER app
CMD ["serve", "-s", "-l", "5000", "dist"]
```
### [Exercise 3.6](https://github.com/sivosam/DevOps-Docker-course/tree/master/Part_3/3_6/feedback)
Optimization reduced size from 394MB to 242MB

Old dockerfile:
```
FROM node:lts-slim
WORKDIR /usr/src/app
RUN apt-get update && apt-get install -y git
RUN git clone https://github.com/sivosam/feedback.git .
EXPOSE 3000
RUN npm install
CMD ["npm", "start"]
```
New dockerfile:
```
FROM node:alpine as build
WORKDIR /usr/src/app
RUN apk add --no-cache git && \
	git init . && \
	git remote add origin https://github.com/sivosam/feedback && \
	git pull origin master && \
	npm install && npm run build

FROM node:alpine
WORKDIR /app
EXPOSE 3000
COPY --from=build /usr/src/app /app

RUN npm install -g serve && \
	adduser -D app && \
	chown -R app /app
USER app

CMD ["serve", "-s", "-l", "3000", "build"]
```
### [Exercise 3.7b](https://github.com/sivosam/DevOps-Docker-course/blob/master/Part_3/3_7.md)

#### When to use Docker
A common problem in software development is an app that works on one machine (the developers own, for example), but not on colleague’s, or certain user’s machine. Since the issue could be due to an unlimited number of reasons, solving it machine by machine can be almost impossible and certainly wasteful. Docker is one attempt at reducing the problem, by having an app and all its dependencies installed within an isolated image and then run in an isolated container (or containers). Thus the problem should no longer arise due to a missing dependency, incompatible versions or some conflict with other installed applications.

Docker is a good tool to use when, for example, you want to quickly try out a piece of software. You can download an image from Docker hub, run it and delete it without much of a hassle. Additionally, no configuration is necessary, since everything can be packaged right into the image. Docker is also extremely useful for projects where more than one dev is required, as highlighted above. When development is done with multiple machines and by multiple people, having all the dependencies and such in a (relatively) small image, ready to be downloaded and ran in a container, certainly reduces problems.

Docker is not a be-all end-all solution though. Running containers means sacrificing performance, for example. In small projects this may not even be noticeable, but does certainly compound with bigger ones. Secondly, while Docker does provide a measure of security due to isolated containers, the containers still have access to the host operating system. Thus a mistake with setting up privileges, or simply a malicious container, can pose a great risk.
