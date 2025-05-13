# Use the official Go image based on Alpine Linux
FROM golang:1.20.10-alpine3.18 as builder

# Set the working directory inside the container
WORKDIR /build

# Copy the Go application code into the container
COPY . .

# Build the Go application
RUN go build -o app

# Multi-stage dockerfile
FROM alpine:3.20
WORKDIR /build

# Setting non-root user
RUN adduser -D appuser
USER appuser

# Copy the built application
COPY --from=builder /build .

# Copy the templates directory
COPY --from=builder /build/templates ./templates

EXPOSE 8080

ENV GIN_MODE=debug

# Define the command to run the Go application
CMD ["./app"]
