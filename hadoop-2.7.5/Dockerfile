FROM centos7-ssh

RUN useradd devops
RUN echo "devops:devops" | chpasswd

ADD jdk-8u151-linux-x64.tar.gz /usr/local/
RUN mv /usr/local/jdk1.8.0_151 /usr/local/jdk1.8
ENV JAVA_HOME /usr/local/jdk1.8
ENV PATH $JAVA_HOME/bin:$PATH

ADD hadoop-2.7.5.tar.gz /usr/local
RUN mv /usr/local/hadoop-2.7.5 /usr/local/hadoop
ENV HADOOP_HOME /usr/local/hadoop
ENV PATH $HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH
ADD conf/core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml
ADD conf/hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml
ADD conf/mapred-site.xml $HADOOP_HOME/etc/hadoop/mapred-site.xml
ADD conf/yarn-site.xml $HADOOP_HOME/etc/hadoop/yarn-site.xml
ADD conf/slaves $HADOOP_HOME/etc/hadoop/slaves
RUN echo "export JAVA_HOME=/usr/local/jdk1.8" >> $HADOOP_HOME/etc/hadoop/hadoop-env.sh
RUN mkdir -p /data/hadoop
RUN chown -R devops:devops /usr/local/hadoop
RUN chown -R devops:devops /data/hadoop

RUN yum install -y which sudo
