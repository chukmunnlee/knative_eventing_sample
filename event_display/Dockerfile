ARG GOLANG_TAG=1.18-alpine3.16
ARG ALPINE_TAG=3.16

FROM golang:${GOLANG_TAG} AS builder

WORKDIR /app

ADD go.mod .
ADD go.sum .
ADD main.go .

RUN go build -o event_display main.go

FROM alpine:${ALPINE_TAG}

LABEL org.opencontainers.image.source=https://github.com/chukmunnlee/knative-eventing-sample/event_display

WORKDIR /app

COPY --from=builder /app/event_display event_display

RUN apk update && apk add curl

ENV PORT=3000

EXPOSE ${PORT}

ENTRYPOINT [ "./event_display" ]
