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