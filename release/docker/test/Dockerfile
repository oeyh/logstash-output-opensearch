ARG APP_VERSION

FROM docker.elastic.co/logstash/logstash-oss:${APP_VERSION}
# Remove existing logstash aws plugins and install logstash-integration-aws to keep sdk dependency the same
# https://github.com/logstash-plugins/logstash-mixin-aws/issues/38
# https://github.com/opensearch-project/logstash-output-opensearch#configuration-for-logstash-output-opensearch-plugin
RUN logstash-plugin remove logstash-input-s3
RUN logstash-plugin remove logstash-input-sqs
RUN logstash-plugin remove logstash-output-s3
RUN logstash-plugin remove logstash-output-sns
RUN logstash-plugin remove logstash-output-sqs
RUN logstash-plugin remove logstash-output-cloudwatch

RUN logstash-plugin install --version 7.1.1 logstash-integration-aws

COPY ./logstash-output-opensearch-2.0.1-x86_64-linux.gem /usr/share
RUN logstash-plugin install /usr/share/logstash-output-opensearch-2.0.1-x86_64-linux.gem
