FROM golang:1.22.5-bullseye AS builder

WORKDIR /app

COPY . .

RUN go mod download && go mod verify && CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags "-s -w" -o /main .

FROM alpine:3.19.3 AS main

COPY --from=builder /main .

EXPOSE 8080 

USER nobody:nobody

ENTRYPOINT ["./main"]