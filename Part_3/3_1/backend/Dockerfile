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
