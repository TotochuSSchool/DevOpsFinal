FROM golang:1.23 AS build
WORKDIR /app
COPY go.mod go.sum ./ 
RUN go mod download
COPY . . 
RUN go build -o vote-api

FROM debian:bullseye-slim
WORKDIR /app
COPY --from=build /app/vote-api .
ENV PG_URL="${PG_URL}"
EXPOSE 8080
RUN useradd -m nonroot
USER nonroot
CMD ["./vote-api"]
