FROM golang:alpine as builder

RUN apk update && apk add curl git
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

COPY . src/github.com/johananl/simple-cm
WORKDIR src/github.com/johananl/simple-cm/cmd/master

RUN dep ensure
RUN go build -o /tmp/master

FROM alpine

COPY --from=builder /tmp/master /master
COPY docker/wait-for.sh /wait-for.sh
CMD /master