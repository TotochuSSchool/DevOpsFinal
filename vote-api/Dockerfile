FROM golang:1.23-alpine AS build
RUN apk add --no-cache gcc musl-dev bash
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN go build -o vote-api

FROM alpine:3.18
RUN apk add --no-cache bash \
    && wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
    && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.35-r0/glibc-2.35-r0.apk \
    && apk add --force-overwrite glibc-2.35-r0.apk \
    && rm glibc-2.35-r0.apk
WORKDIR /app
COPY --from=build /app/vote-api .
RUN adduser -D -h /app nonroot
USER nonroot
EXPOSE 8080
CMD ["./vote-api"]
