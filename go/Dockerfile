FROM golang:alpine as builder

WORKDIR /cmd/main
COPY go.mod ./

RUN go mod download

COPY . .

RUN cd cmd && CGO_ENABLED=0 GOOS=linux go build -o api main.go


FROM scratch
COPY . .
WORKDIR /app
COPY --from=builder /cmd/main/cmd/api .

CMD ["./api"]
