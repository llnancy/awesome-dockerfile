FROM rabbitmq:management-alpine

ARG URL=https://api.github.com/repos/rabbitmq/rabbitmq-delayed-message-exchange/releases/latest
RUN apk add --update --no-cache curl jq wget && \
  VERSION=`curl $URL | jq -r ".tag_name"` && \
  wget -P /plugins https://github.com/rabbitmq/rabbitmq-delayed-message-exchange/releases/download/${VERSION}/rabbitmq_delayed_message_exchange-${VERSION}.ez && \
  rabbitmq-plugins enable --offline rabbitmq_delayed_message_exchange

LABEL maintainer=admin@lilu.org.cn
