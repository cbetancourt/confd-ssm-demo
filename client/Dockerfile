FROM confd-alpine:latest

ENV ENVIRONMENT=dev
ENV AWS_DEFAULT_REGION=us-east-1
ENV AWS_REGION=${AWS_DEFAULT_REGION}

COPY manifest /

VOLUME [ "/output" ]
ENTRYPOINT [ "/usr/local/bin/entrypoint.sh" ]
