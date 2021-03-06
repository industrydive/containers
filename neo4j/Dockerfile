FROM java:openjdk-8-jre

ENV NEO4J_VERSION 2.2.5
ENV NEO4J_EDITION community
ENV NEO4J_DOWNLOAD_SHA256 7fadc119f465a3d6adceb610401363fb158a5ed25081f9893d4f56ac4989a998
ENV NEO4J_DOWNLOAD_ROOT http://dist.neo4j.org
ENV NEO4J_TARBALL neo4j-$NEO4J_EDITION-$NEO4J_VERSION-unix.tar.gz
ENV NEO4J_URI $NEO4J_DOWNLOAD_ROOT/$NEO4J_TARBALL



RUN apt-get update --quiet --quiet \
    && apt-get install --quiet --quiet --no-install-recommends lsof \
    && rm -rf /var/lib/apt/lists/*

RUN curl --fail --silent --show-error --location --output neo4j.tar.gz $NEO4J_URI \
    && echo "$NEO4J_DOWNLOAD_SHA256 neo4j.tar.gz" | sha256sum --check --quiet - \
    && tar --extract --file neo4j.tar.gz --directory /var/lib \
    && mv /var/lib/neo4j-* /var/lib/neo4j \
    && rm neo4j.tar.gz

WORKDIR /var/lib/neo4j

RUN mv data /data \
    && ln --symbolic /data

VOLUME /data

COPY docker-entrypoint.sh /docker-entrypoint.sh

EXPOSE 7474 7473

RUN sed -i -e "s|org.neo4j.server.webadmin.rrdb.location=.*|org.neo4j.server.webadmin.rrdb.location=/tmp/rrd|g" /var/lib/neo4j/conf/neo4j-server.properties && \
    touch /tmp/rrd

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["neo4j"]
