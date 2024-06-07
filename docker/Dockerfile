# Build container
FROM golang:1.21 AS build

ARG VERSION

COPY . /home/src
WORKDIR /home/src

RUN CGO_ENABLED=0 go build -v -o . -ldflags="-w -s" ./...

# Runtime container
FROM alpine as base-publisher

RUN apk add --update --no-cache \
    ca-certificates \
    bash

WORKDIR /home/app
COPY --from=build /home/src/base-publisher .
RUN chmod +x /home/app/base-publisher

CMD ["./base-publisher", "start"]
