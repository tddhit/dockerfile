FROM centos7-ssh

RUN useradd devops
RUN echo "devops:devops" | chpasswd

RUN echo "devops  -      nofile  32768 " >> /etc/security/limits.conf
RUN echo "devops  -      nproc   32000" >>  /etc/security/limits.conf
RUN echo "session required pam_limits.so" >>  /etc/pam.d/common-session

ADD jdk-8u151-linux-x64.tar.gz /usr/local/
RUN mv /usr/local/jdk1.8.0_151 /usr/local/jdk1.8
ENV JAVA_HOME /usr/local/jdk1.8
ENV PATH $JAVA_HOME/bin:$PATH

ADD hbase-1.2.6-bin.tar.gz /usr/local
RUN mv /usr/local/hbase-1.2.6 /usr/local/hbase
ENV HBASE_HOME /usr/local/hbase
ENV PATH $HBASE_HOME/bin:$PATH
ADD conf/hbase-site.xml $HBASE_HOME/conf/hbase-site.xml
ADD conf/regionservers $HBASE_HOME/conf/regionservers
RUN echo "export JAVA_HOME=/usr/local/jdk1.8" >> $HBASE_HOME/conf/hbase-env.sh
RUN echo "export HBASE_MANAGES_ZK=false" >> $HBASE_HOME/conf/hbase-env.sh
RUN mkdir -p /data/hbase
RUN chown -R devops:devops /usr/local/hbase
RUN chown -R devops:devops /data/hbase

RUN yum install -y which sudo
