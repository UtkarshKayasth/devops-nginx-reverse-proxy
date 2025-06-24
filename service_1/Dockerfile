# Use official Golang image
FROM golang:1.22

# Set working directory
WORKDIR /app

# Copy source code
COPY . .

# Build the Go binary
RUN go build -o main .

# Expose port used by the app
EXPOSE 8001

# Command to run the app
CMD ["./main"]
