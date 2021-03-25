# Kafka and Zookeeper

FROM arm64v8/openjdk:11

ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.13
ENV KAFKA_VERSION 2.6.1
ENV KAFKA_HOME /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}

# Install Kafka, Zookeeper and other needed things
RUN apt-get update
RUN apt-get install -y -f zookeeper 
RUN apt-get install -y -f wget
RUN apt-get install -y -f supervisor
RUN apt-get install -y -f dnsutils
RUN rm -rf /var/lib/apt/lists/* && apt-get clean
RUN wget https://archive.apache.org/dist/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz -O /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz
RUN tar xfz /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz -C /opt
RUN rm /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz

ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

# Supervisor config
ADD supervisor/kafka.conf supervisor/zookeeper.conf /etc/supervisor/conf.d/

# 2181 is zookeeper, 9092 is kafka
EXPOSE 2181 9092

CMD ["supervisord", "-n"]
