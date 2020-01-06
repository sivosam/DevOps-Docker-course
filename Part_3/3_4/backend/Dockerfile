FROM node:alpine
EXPOSE 8000
ENV FRONT_URL="http://localhost:5000"
WORKDIR /app
COPY . .
RUN npm install && \
	adduser -S -D app && chown -R app /app
USER app
CMD ["npm", "start"]
