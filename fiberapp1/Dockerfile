#first stage - builder
FROM golang:1.14 as builder
RUN mkdir -p /build
WORKDIR /build

ENV GO111MODULE=on \
CGO_ENABLED=0 \
GOOS=linux \
GOARCH=amd64

# Copy and download dependency using go mod
COPY go.mod .
COPY go.sum .
RUN go mod download

# Copy the code into the container
COPY . /build

RUN go build /build/main.go

#second stage
FROM golang:1.14-alpine
RUN mkdir -p /app
WORKDIR /app
COPY --from=builder /build/main .
ENTRYPOINT ["./main"]