FROM golang:1.18.3-alpine
WORKDIR /go/src
COPY . .
ENV GOPROXY https://proxy.golang.org,direct
ENV CGO_ENABLED=0
ENV PATH="/go/bin:${PATH}"
RUN go mod download
RUN apk add --update librdkafka-dev --no-cache
RUN GOOS=linux go build ./main.go
FROM scratch
COPY --from=0 /go/src .
CMD ["./main"]