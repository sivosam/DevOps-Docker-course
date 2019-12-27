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
