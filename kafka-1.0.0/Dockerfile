FROM centos7-ssh

RUN useradd devops
RUN echo "devops:devops" | chpasswd

ADD jdk-8u151-linux-x64.tar.gz /usr/local/
RUN mv /usr/local/jdk1.8.0_151 /usr/local/jdk1.8
ENV JAVA_HOME /usr/local/jdk1.8
ENV PATH $JAVA_HOME/bin:$PATH

ADD kafka_2.11-1.0.0.tgz /usr/local
RUN mv /usr/local/kafka_2.11-1.0.0 /usr/local/kafka
ENV KAFKA_HOME /usr/local/kafka
ENV PATH $KAFKA_HOME/bin:$PATH
ADD conf/server.properties /usr/local/kafka/config

RUN mkdir -p /data/kafka
RUN chown -R devops:devops /usr/local/kafka
RUN chown -R devops:devops /data/kafka

RUN yum install -y which sudo
