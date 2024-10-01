FROM golang:1.23-alpine AS builder

# Set the working directory
WORKDIR /app

# Copy the source code to the container
COPY sample-app .

RUN go mod download

# Build the application
RUN go build -o main .

# Create a distroless image
FROM gcr.io/distroless/base-debian11

# Copy the binary from the builder stage
COPY --from=builder /app/main /app/main

# Set the entrypoint
ENTRYPOINT ["/app/main"]