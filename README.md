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

### [Exercise 1.3]

### [Exercise 1.3]

### [Exercise 1.3]

### [Exercise 1.3]

### [Exercise 1.3]

### [Exercise 1.3]

### [Exercise 1.3]

### [Exercise 1.3]
### [Exercise 1.3]
### [Exercise 1.3]

### [Exercise 1.3]
### [Exercise 1.3]
### [Exercise 1.3]
