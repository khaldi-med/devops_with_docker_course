FROM golang:1.16

EXPOSE 8080

WORKDIR /app

COPY go.mod go.sum ./

COPY . . 

RUN go build -o server .

RUN go test ./...

CMD ["./server"]

