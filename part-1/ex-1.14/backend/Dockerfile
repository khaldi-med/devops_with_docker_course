FROM golang:1.16

EXPOSE 8080

WORKDIR /app

COPY go.mod go.sum ./

COPY . . 

ENV PORT=8080 \
    REQUEST_ORIGIN=http://localhost:5000

RUN go build -o server .

RUN go test ./...

CMD ["./server"]
