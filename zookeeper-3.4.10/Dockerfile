FROM centos7-ssh

RUN useradd devops
RUN echo "devops:devops" | chpasswd

ADD jdk-8u151-linux-x64.tar.gz /usr/local/
RUN mv /usr/local/jdk1.8.0_151 /usr/local/jdk1.8
ENV JAVA_HOME /usr/local/jdk1.8
ENV PATH $JAVA_HOME/bin:$PATH

ADD zookeeper-3.4.10.tar.gz /usr/local/
RUN mv /usr/local/zookeeper-3.4.10 /usr/local/zookeeper
ENV ZK_HOME /usr/local/zookeeper
ENV PATH $ZK_HOME/bin:$PATH
ADD conf/zoo.cfg $ZK_HOME/conf/zoo.cfg
RUN mkdir -p /data/zookeeper
RUN chown -R devops:devops /usr/local/zookeeper
RUN chown -R devops:devops /data/zookeeper

RUN yum install -y which sudo
