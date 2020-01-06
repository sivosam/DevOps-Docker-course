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
