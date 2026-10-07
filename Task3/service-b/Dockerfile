FROM golang:1.25-alpine AS build
WORKDIR /src
COPY go.mod go.sum ./
RUN go mod download
COPY main.go ./
RUN CGO_ENABLED=0 GOOS=linux go build -trimpath -ldflags="-s -w" -o /service-b .

FROM gcr.io/distroless/static-debian12:nonroot
COPY --from=build /service-b /service-b
EXPOSE 8080
ENTRYPOINT ["/service-b"]
