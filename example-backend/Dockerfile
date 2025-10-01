FROM golang:1.16-alpine AS build-env

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN go build


# production
FROM alpine

RUN apk update && apk add ca-certificates && rm -rf /var/cache/apk/*

WORKDIR /usr/src/app

COPY --from=build-env /usr/src/app/server .

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

USER appuser

ENTRYPOINT ["./server"]