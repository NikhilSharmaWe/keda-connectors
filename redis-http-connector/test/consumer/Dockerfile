FROM golang:1.18-alpine as builder

RUN apk add bash ca-certificates git gcc g++ libc-dev

RUN mkdir /consumer
WORKDIR /consumer
COPY go.mod . 
COPY go.sum .

RUN go mod download

# Copy source code to image
COPY . .

RUN go build -a -o /go/bin/main
FROM alpine:3.16 as base
RUN apk add --update ca-certificates
COPY --from=builder /go/bin/main /

ENTRYPOINT ["/main"]