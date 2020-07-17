# Pull Energi Core Node source from Github and compile on a Golang Alpine container.
FROM golang:1.13.7-alpine as builder

RUN apk add --no-cache make gcc musl-dev linux-headers git go

RUN git clone --depth 1 https://github.com/energicryptocurrency/energi3
RUN cd energi3 && make geth

# Copy Energi3 Binaries to a new deploy Alpine container
FROM alpine:latest

RUN apk add --no-cache ca-certificates
COPY --from=builder /go/energi3/build/bin/energi3 /usr/local/bin/

# Expose the necessary ports for testnet and mainnet.
EXPOSE 39795 39796 39797 39797/udp 49795 49796 49797 49797/udp
ENTRYPOINT ["energi3"]
