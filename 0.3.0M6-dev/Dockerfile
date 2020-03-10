FROM ubuntu:16.04

ENV HAWKBIT_VERSION=0.3.0M6 \
    HAWKBIT_HOME=/opt/hawkbit \
    HAWKBIT_BRANCH=0.3.0M6-dev \
    HAWKBIT_PROJECT_PATH=/opt/hawkbit/hawkbit \
    HAWKBIT_TARGET_PATH=/opt/hawkbit/hawkbit/hawkbit-runtime/hawkbit-update-server/target \
    HAWKBIT_REPOSITORY=https://github.com/nguyenvuhung/hawkbit.git

EXPOSE 8080

# Install JDK 8
# This is in accordance to : https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-get-on-ubuntu-16-04
RUN apt-get update && \
	apt-get install -y openjdk-8-jdk && \
	apt-get install -y ant && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk8-installer;
	
# Fix certificate issues, found as of 
# https://bugs.launchpad.net/ubuntu/+source/ca-certificates-java/+bug/983302
RUN apt-get update && \
	apt-get install -y ca-certificates-java && \
	apt-get clean && \
	update-ca-certificates -f && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk8-installer;

# Setup JAVA_HOME, this is useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
RUN export JAVA_HOME

RUN apt-get update && apt-get -y install gnupg unzip wget git-core maven \
    && mkdir -p $HAWKBIT_HOME \
    && cd $HAWKBIT_HOME \
    && git clone $HAWKBIT_REPOSITORY -b $HAWKBIT_BRANCH

WORKDIR $HAWKBIT_PROJECT_PATH
RUN mvn clean install
WORKDIR $HAWKBIT_TARGET_PATH
RUN cp hawkbit-update-server*SNAPSHOT.jar hawkbit-update-server.jar

VOLUME "$HAWKBIT_HOME/data"

ENTRYPOINT ["java","-jar","hawkbit-update-server.jar","-Xms768m -Xmx768m -XX:MaxMetaspaceSize=250m -XX:MetaspaceSize=250m -Xss300K -XX:+UseG1GC -XX:+UseStringDeduplication -XX:+UseCompressedOops -XX:+HeapDumpOnOutOfMemoryError"]
