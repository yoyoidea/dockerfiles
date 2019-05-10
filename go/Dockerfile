FROM golang:1.12-alpine
RUN mkdir /website
WORKDIR /websitw
ENV GO111MODULE=on
COPY . .
RUN go mod download
RUN go build main.go
CMD ["./main"]
