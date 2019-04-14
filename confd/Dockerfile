FROM alpine:latest

ENV ENVIRONMENT=dev
ENV AWS_DEFAULT_REGION=us-east-1
ENV AWS_REGION=us-east-1

RUN apk --update --no-cache add ca-certificates \
  && apk add curl

ARG TARGET_DIR=/usr/local/bin
ARG VERSION=0.16.0
ARG URL=https://github.com/kelseyhightower/confd/releases/download/v${VERSION}/confd-${VERSION}-linux-amd64
WORKDIR ${TARGET_DIR}

RUN curl -L ${URL} -o confd && chmod u+x confd

COPY manifest /

VOLUME [ "/config-output" ]

ENTRYPOINT [ "./entrypoint.sh" ]
