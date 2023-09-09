FROM golang:alpine as builder

# Install git.
# Git is required for fetching the dependencies.
RUN apk update && apk add --no-cache git

RUN mkdir /build

ADD . /build/

WORKDIR /build

# Using go get.
RUN go get -d -v

RUN GOOS=linux GOARCH=amd64 go build -ldflags="-w -s" -o short-url .

#stage 2

FROM scratch 

# Copy our static executable.
COPY --from=builder /build/short-url /go/bin/short-url

# Run the hello binary.
ENTRYPOINT ["/go/bin/short-url"]