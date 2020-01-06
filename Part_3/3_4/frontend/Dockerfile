FROM node:alpine
EXPOSE 5000
ENV API_URL="http://localhost:8000"
WORKDIR /app
COPY . .
RUN npm install && \
	adduser -D -S app && chown -R app /app
USER app
CMD ["npm", "start"]