# Stage 1
FROM golang:1.21-alpine AS builder

WORKDIR /app

# Install tzdata di build stage
RUN apk add --no-cache tzdata

COPY go.mod ./
COPY go.sum ./
RUN go mod download

COPY . .

RUN go build -o /api-contact-form

# Stage 2
FROM alpine

# Install tzdata di runtime stage juga
RUN apk add --no-cache tzdata

WORKDIR /root/

COPY --from=builder /api-contact-form .

# Set timezone
ENV TZ=Asia/Jakarta

CMD ["./api-contact-form"]
