
FROM golang:1.26.4-alpine AS builder

WORKDIR /app

COPY go.mod ./
COPY . .

RUN go build -o http-server-projeto-korp .


FROM alpine:latest

WORKDIR /root/

COPY --from=builder /app/http-server-projeto-korp .

EXPOSE 8080

CMD ["./http-server-projeto-korp"]