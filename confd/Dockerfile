FROM alpine:latest

ENV ENVIRONMENT=dev
ENV AWS_DEFAULT_REGION=us-east-1
ENV AWS_REGION=us-east-1

RUN apk --update --no-cache add ca-certificates \
  && apk add curl

ARG VERSION=0.16.0
ARG URL=https://github.com/kelseyhightower/confd/releases/download/v${VERSION}/confd-${VERSION}-linux-amd64
ARG TARGET_DIR=/usr/local/bin
RUN curl -L ${URL} -o ${TARGET_DIR}/confd && chmod u+x ${TARGET_DIR}/confd

VOLUME [ "/config-output" ]

COPY manifest /

WORKDIR ${TARGET_DIR}
ENTRYPOINT [ "./entrypoint.sh" ]
