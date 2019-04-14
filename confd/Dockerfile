FROM alpine:latest

ENV ENVIRONMENT=dev
ENV AWS_DEFAULT_REGION=us-east-1
ENV AWS_REGION=us-east-1

RUN apk --update --no-cache add ca-certificates

ARG VERSION=0.16.0
RUN wget https://github.com/kelseyhightower/confd/releases/download/v${VERSION}/confd-${VERSION}-linux-amd64 -O /usr/local/bin/confd \
  && chmod +x /usr/local/bin/confd

VOLUME [ "/config-output" ]

COPY manifest /

ENTRYPOINT [ "/usr/local/bin/entrypoint.sh" ]
