# Build energi3 in a stock Go builder container
FROM golang:1.13.7-alpine as builder

RUN apk add --no-cache make gcc musl-dev linux-headers git go

RUN git clone --depth 1 https://github.com/energicryptocurrency/energi3
RUN cd energi3 && make geth

# Pull energi3 into a second stage deploy alpine container
FROM alpine:latest

RUN apk add --no-cache ca-certificates
COPY --from=builder /go/energi3/build/bin/energi3 /usr/local/bin/

EXPOSE 49796 49795 49797 49797/udp
ENTRYPOINT ["energi3"]
