FROM vuhungkt18/hawkbit-update-server:0.3.0M6-dev

ENV MARIADB_DRIVER_VERSION=2.5.3

COPY KEY .

RUN gpg --import KEY \
    && wget -O $JAVA_HOME/jre/lib/ext/mariadb-java-client.jar --no-verbose https://downloads.mariadb.com/Connectors/java/connector-java-$MARIADB_DRIVER_VERSION/mariadb-java-client-$MARIADB_DRIVER_VERSION.jar \
    && wget -O $JAVA_HOME/jre/lib/ext/mariadb-java-client.jar.asc --no-verbose https://downloads.mariadb.com/Connectors/java/connector-java-$MARIADB_DRIVER_VERSION/mariadb-java-client-$MARIADB_DRIVER_VERSION.jar.asc \
    && gpg --verify --batch $JAVA_HOME/jre/lib/ext/mariadb-java-client.jar.asc $JAVA_HOME/jre/lib/ext/mariadb-java-client.jar

WORKDIR $HAWKBIT_TARGET_PATH

ENTRYPOINT ["java","-jar","hawkbit-update-server.jar","--spring.profiles.active=mysql","-Xms768m -Xmx768m -XX:MaxMetaspaceSize=250m -XX:MetaspaceSize=250m -Xss300K -XX:+UseG1GC -XX:+UseStringDeduplication -XX:+UseCompressedOops -XX:+HeapDumpOnOutOfMemoryError"]

