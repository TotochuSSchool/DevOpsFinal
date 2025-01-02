FROM golang:1.20 AS build
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . ./
RUN go build -o /app/vote-api && ls -l /app/vote-api

FROM debian:bullseye-slim
WORKDIR /app
COPY --from=build /app/vote-api /app/vote-api
RUN chmod +x /app/vote-api && ls -l /app/vote-api
RUN useradd -m nonroot
USER nonroot
EXPOSE 8080
CMD ["./vote-api"]
