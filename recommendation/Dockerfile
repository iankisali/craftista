# Using official Golang image based on Alpine
FROM golang:1.22.6-alpine3.20 AS builder
WORKDIR /build
COPY . .
RUN go build -o app


FROM alpine:3.20
WORKDIR /run
COPY --from=builder /build/app .
COPY --from=builder /build/static .
COPY --from=builder /build/templates .
COPY --from=builder /build/api .
COPY --from=builder /build/data .
EXPOSE 8080
CMD ./app