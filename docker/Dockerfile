FROM centos:centos7


ENV JAVA_HOME /usr/lib/jvm/java-11
ARG PRESTO_VERSION=340

RUN \
    set -xeu && \
    yum -y -q update && \
    yum -y -q install java-11-openjdk-devel less curl && \
    yum -q clean all && \
    rm -rf /var/cache/yum && \
    rm -rf /tmp/* /var/tmp/* && \
    groupadd presto --gid 1000 && \
    useradd presto --uid 1000 --gid 1000 && \
    mkdir -p /usr/lib/presto /data/presto  /etc/presto && \
    chown -R "presto:presto" /usr/lib/presto /data/presto /etc/presto


# RUN \
    # curl https://repo1.maven.org/maven2/io/prestosql/presto-server/${PRESTO_VERSION}/presto-server-${PRESTO_VERSION}.tar.gz --output presto-server-${PRESTO_VERSION}.tar.gz \
    # tar xvzf presto-server-*.tar.gz \
    # curl https://repo1.maven.org/maven2/io/prestosql/presto-cli/${PRESTO_VERSION}/presto-cli-${PRESTO_VERSION}-executable.jar --output presto-cli-${PRESTO_VERSION}-executable.jar \
    # mv presto-cli-${PRESTO_VERSION}-executable.jar /usr/bin/presto \
    # mv presto-server-${PRESTO_VERSION} /usr/lib/presto && chown presto:presto presto-server-${PRESTO_VERSION}

COPY src/presto-cli-${PRESTO_VERSION}-executable.jar /usr/bin/presto
COPY --chown=presto:presto src/presto-server-${PRESTO_VERSION}.tar.gz .
RUN \
    tar -xvzf presto-server-*.tar.gz

RUN \
    mv ./presto-server-${PRESTO_VERSION}/* /usr/lib/presto/ && \
    chown -R presto:presto /usr/lib/presto/*

COPY --chown=presto:presto bin/run-presto /usr/lib/presto/bin/run-presto

EXPOSE 8080
USER presto:presto
ENV LANG en_US.UTF-8
CMD ["/usr/lib/presto/bin/run-presto"]
