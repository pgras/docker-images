FROM ubuntu:18.04

ARG kafka_version=2.1.1
ARG scala_version=2.12

ARG filename=kafka_${scala_version}-${kafka_version}.tgz
ARG download_url="http://www-eu.apache.org/dist/kafka/${kafka_version}/${filename}"

ENV KAFKA_VERSION=${kafka_version} \
    SCALA_VERSION=${scala_version} \
    KAFKA_HOME=/opt/kafka \
    PATH=${PATH}:${KAFKA_HOME}/bin

EXPOSE 2181
EXPOSE 9092

RUN apt-get update && apt-get install -y \
  nano \
  openjdk-8-jdk \
  wget \
  && rm -rf /var/lib/apt/lists/*

RUN wget ${download_url} -O /tmp/${filename}

RUN tar xfz /tmp/${filename} -C /opt \
 && rm /tmp/${filename} \
 && ln -s /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION} /opt/kafka \
 && rm -rf /tmp/*

COPY include/kafka_${scala_version}-${kafka_version}/config/server.properties /opt/kafka/config/server.properties
COPY include/kafka_${scala_version}-${kafka_version}/config/zookeper.properties /opt/kafka/config/zookeeper.properties

VOLUME ["/var/lib/zookeeper/data", "/var/lib/zookeeper/log", "/etc/zookeeper/secrets"]

VOLUME ["/var/lib/kafka/data", "/etc/kafka/secrets"]
