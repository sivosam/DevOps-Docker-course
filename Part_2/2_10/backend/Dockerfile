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
