FROM alpine:3.10

LABEL "com.github.actions.name"="Label Deleter"
LABEL "com.github.actions.description"="Deletes labels from Pull Requests"
LABEL "com.github.actions.icon"="delete"
LABEL "com.github.actions.color"="red"

RUN apk add --no-cache \
    curl jq bash

ADD entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]