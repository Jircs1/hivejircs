FROM golang:1-alpine AS builder
RUN apk --no-cache add gcc musl-dev linux-headers cmake make clang build-base clang-static clang-dev

# Prepare workspace.
# Note: the build context of this simulator image is the parent directory!
ADD . /source

# Build within simulator folder
WORKDIR /source/testnet
RUN go build -o ./sim .

# Build the runner container.
FROM alpine:3.20.3
ADD . /
COPY --from=builder /source/testnet/sim /
ENTRYPOINT ["./sim"]
