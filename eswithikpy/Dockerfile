# Elasticsearch 6.8.10

# This image re-bundles the Docker image from the upstream provider, Elastic.

FROM docker.elastic.co/elasticsearch/elasticsearch:6.8.10@sha256:f8e21f6b2ef75dcda374da505fcb0ff4bf7e8d025f12096c498123fa4e372c1b
ARG VERSION=6.8.10

# do all in one step
RUN cd /usr/share/elasticsearch/plugins/ && \
    wget https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v${VERSION}/elasticsearch-analysis-ik-${VERSION}.zip && \
    wget https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v${VERSION}/elasticsearch-analysis-pinyin-${VERSION}.zip && \
    unzip elasticsearch-analysis-ik-${VERSION}.zip -d ik && rm -f elasticsearch-analysis-ik-${VERSION}.zip && \
    unzip elasticsearch-analysis-pinyin-${VERSION}.zip -d pinyin && rm -f elasticsearch-analysis-pinyin-${VERSION}.zip
