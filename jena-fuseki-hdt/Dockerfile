# I'm sorry to say that the rdfhdt dockerfiles do not include any tags, so we can't
# use a static version for this.

FROM stain/jena-fuseki:3.14.0
ARG hdt_version=2.1-SNAPSHOT
ARG hdt_digest=sha256:07663c171737f4967241128933a81dc94d46a475ef7f474f0fbfb97640cd241d

# As it stands, we need to rely on including the jar files directly in the repo.
COPY --from=rdfhdt/hdt-java@sha256:07663c171737f4967241128933a81dc94d46a475ef7f474f0fbfb97640cd241d \
/opt/hdt-java/lib/hdt-java-core-${hdt_version}.jar \
/opt/hdt-java/lib/hdt-api-${hdt_version}.jar \
/opt/hdt-java/lib/hdt-jena-${hdt_version}.jar $FUSEKI_HOME/

# We need to modify add a server command with hdt
COPY config.ttl $FUSEKI_HOME/
COPY fuseki-server-hdt $FUSEKI_HOME
RUN chmod 755 $FUSEKI_HOME/fuseki-server-hdt

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/jena-fuseki/fuseki-server-hdt"]
