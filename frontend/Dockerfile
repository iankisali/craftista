# Using official Node.js image based on Alpine Linux
FROM node:22-alpine3.19 as build

# Setting working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the container  
COPY package*.json ./

# Installing application dependencies
RUN npm install

# Copy rest of application to container
COPY . .

# ----------------------------------------------
# Second Stage: Create a smaller image for production
# ----------------------------------------------


# U sing small base image
FROM node:alpine

# Setting non-root user
RUN adduser -D appuser
USER appuser

# Setting working directory in the container
WORKDIR /app

# Copy necessary files from previous build stage
COPY --from=build /app .

# Exposing port app will run in the container
EXPOSE 3000

# Set default environment variables (if needed)
# ENV NODE_ENV=production

# Add a health check (modify as per your app's needs)
# HEALTHCHECK --interval=30s --timeout=30s CMD curl -f http://localhost:3000 || exit 1

# Command to run the application
CMD node app.js