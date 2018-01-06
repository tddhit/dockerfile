#基于centos-ssh构建
FROM centos-ssh

#配置各节点时间同步
RUN yum install -y ntp
#RUN systemctl is-enabled ntpd
#必须在run 容器时授权--privileged
#RUN systemctl enable ntpd
#RUN systemctl start ntpd
#docker容器与宿主机时区同步
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/shanghai" > /etc/timezone

#增加bigdata用户
RUN useradd bigdata 
RUN echo "bigdata:12345678" | chpasswd

#对于Hbase 修改 ulimit 限制
RUN echo "bigdata  -      nofile  32768 " >> /etc/security/limits.conf
RUN echo "bigdata  -      nproc   32000" >>  /etc/security/limits.conf
RUN echo "session required pam_limits.so" >>  /etc/pam.d/common-session

#安装java
ADD jdk-8u151-linux-x64.tar.gz /usr/local/
RUN mv /usr/local/jdk1.8.0_151 /usr/local/jdk1.8

#配置JAVA环境变量
ENV JAVA_HOME /usr/local/jdk1.8
ENV PATH $JAVA_HOME/bin:$PATH

#安装hadoop
ADD hadoop-2.7.5.tar.gz /usr/local
RUN mv /usr/local/hadoop-2.7.5 /usr/local/hadoop

#配置hadoop环境变量
ENV HADOOP_HOME /usr/local/hadoop
ENV PATH $HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH

#安装ZooKeeper
ADD zookeeper-3.4.10.tar.gz /usr/local
RUN mv /usr/local/zookeeper-3.4.10 /usr/local/zookeeper

#配置ZooKeeper环境变量
ENV ZOOKEEPERE_HOME /usr/local/zookeeper
ENV PATH $ZOOKEEPERE_HOME/bin:$PATH

#安装HBase
ADD hbase-1.2.6-bin.tar.gz /usr/local
RUN mv /usr/local/hbase-1.2.6 /usr/local/hbase

#配置Hbase环境变量
ENV HBASE_HOME /usr/local/hbase
ENV PATH $HBASE_HOME/bin:$PATH

ADD conf/hadoop/core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml
ADD conf/hadoop/hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml
ADD conf/hadoop/mapred-site.xml $HADOOP_HOME/etc/hadoop/mapred-site.xml
ADD conf/hadoop/yarn-site.xml $HADOOP_HOME/etc/hadoop/yarn-site.xml
ADD conf/hadoop/slaves $HADOOP_HOME/etc/hadoop/slaves

ADD conf/zookeeper/zoo.cfg $ZOOKEEPERE_HOME/conf/zoo.cfg

ADD conf/hbase/hbase-site.xml $HBASE_HOME/conf/hbase-site.xml
ADD conf/hbase/regionservers $HBASE_HOME/conf/regionservers

RUN echo "export JAVA_HOME=/usr/local/jdk1.8" >> $HBASE_HOME/conf/hbase-env.sh
RUN echo "export HBASE_MANAGES_ZK=false" >> $HBASE_HOME/conf/hbase-env.sh

RUN echo "export JAVA_HOME=/usr/local/jdk1.8" >> $HADOOP_HOME/etc/hadoop/hadoop-env.sh

RUN chown -R bigdata:bigdata /usr/local/hadoop
RUN chown -R bigdata:bigdata /usr/local/hbase
RUN chown -R bigdata:bigdata /usr/local/zookeeper

RUN yum install -y which sudo
