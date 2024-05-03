FROM golang:1.22.2-alpine3.18 as builder
WORKDIR /build
COPY . . 
RUN go build -o app


FROM alpine:3.18
WORKDIR /run
COPY --from=builder /build/app .
COPY --from=builder /build/static .
COPY --from=builder /build/templates .
EXPOSE 8080
CMD ["./app"]