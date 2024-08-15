# Using official Node.js image based on Alpine
FROM node:22-alpine3.19

# 
WORKDIR /app

COPY . .

RUN npm install

EXPOSE 3000

CMD node app.js