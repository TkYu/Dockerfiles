# Elasticsearch 7.8.0

# This image re-bundles the Docker image from the upstream provider, Elastic.

FROM docker.elastic.co/elasticsearch/elasticsearch:7.8.0@sha256:161bc8c7054c622b057324618a2e8bc49ae703e64901b141a16d9c8bdd3b82f9
ARG VERSION=7.8.0

# do all in one step
RUN cd /usr/share/elasticsearch/plugins/ && \
    wget https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v${VERSION}/elasticsearch-analysis-ik-${VERSION}.zip && \
    wget https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v${VERSION}/elasticsearch-analysis-pinyin-${VERSION}.zip && \
    unzip elasticsearch-analysis-ik-${VERSION}.zip -d ik && rm -f elasticsearch-analysis-ik-${VERSION}.zip && \
    unzip elasticsearch-analysis-pinyin-${VERSION}.zip -d pinyin && rm -f elasticsearch-analysis-pinyin-${VERSION}.zip
