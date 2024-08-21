# Use the official Go image based on Alpine Linux
FROM golang:1.20.10-alpine3.18 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the Go application code into the container
COPY go.mod go.sum ./

# Build the Go application
RUN go mod download

# Copy rest of application code
COPY . .

# Build the Go application with optimizations
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o app


# ----------------------------------------------
# Second Stage: Create a smaller image for production
# ----------------------------------------------

# Alpine base image
FROM alpine:3.18

# Setting the working directory inside the container
WORKDIR /app

# Copy only compiles Go binary from build stage
COPY --from=builder /app/app .

# Copy the templates directory
COPY --from=builder /app/templates ./templates

# Setting app to production mode
ENV GIN_MODE=release

# Expose port 8080 for the application
EXPOSE 8080

# Define the command to run the Go application
CMD ["./app"]