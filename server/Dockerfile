FROM alpine:3.9

RUN apk --update --no-cache add ca-certificates \
  && apk add curl

ARG BIN_DIR=/usr/local/bin
ARG CONFD_VERSION=0.16.0
ARG URL=https://github.com/kelseyhightower/confd/releases/download/v${CONFD_VERSION}/confd-${CONFD_VERSION}-linux-amd64
WORKDIR ${BIN_DIR}
RUN curl -L ${URL} -o confd && chmod u+x confd

# copy empty confd dir tree and entrypoint.sh
COPY manifest /

# implementing client should map an output volume and execute entrypoint.sh
# VOLUME [ "/output" ]
# ENTRYPOINT [ "./entrypoint.sh" ]
