# Using official nodejs image based on alpine
FROM node:21-alpine3.18

# Setting the working directory inside the container
WORKDIR /app

#Copy all file locally to the container
COPY . .

# Install application dependencies
RUN npm install

# Exposing port application running on
EXPOSE 3000

# Define command to run application
CMD node app.js