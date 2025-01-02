FROM golang:1.23 AS build
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN go build -o /app/vote-api

FROM debian:bullseye-slim
WORKDIR /app
COPY --from=build /app/vote-api /app/vote-api
ENV PG_URL="${PG_URL}"
EXPOSE 8080
RUN chmod +x /app/vote-api
RUN useradd -m nonroot
USER nonroot
CMD ["/app/vote-api"]
