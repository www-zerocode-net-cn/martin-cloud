
FROM openjdk:8u312-jdk-oraclelinux7

MAINTAINER martin114@foxmail.com

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime


# set environment
ENV MODE="cluster" \
    PREFER_HOST_MODE="ip"\
    BASE_DIR="/home/nacos" \
    CLASSPATH=".:/home/nacos/conf:$CLASSPATH" \
    CLUSTER_CONF="/home/nacos/conf/cluster.conf" \
    FUNCTION_MODE="all" \
    NACOS_USER="nacos" \
    JAVA="/usr/java/openjdk-8/bin/java" \
    JVM_XMS="512m" \
    JVM_XMX="512m" \
    JVM_XMN="256m" \
    NACOS_DEBUG="n" \
    TOMCAT_ACCESSLOG_ENABLED="false" \
    TZ="Asia/Shanghai"

RUN mkdir -p $BASE_DIR

WORKDIR $BASE_DIR

ADD ./nacos-server-1.4.2.tar.gz /home

ADD ./build/bin/docker-startup.sh $BASE_DIR/bin/docker-startup.sh

ADD ./build/conf/application.properties $BASE_DIR/conf/application.properties



# set startup log dir
RUN mkdir -p $BASE_DIR/logs \
    && cd $BASE_DIR/logs \
    && touch startc.out \
    && ln -sf /dev/stdout start.out \
    && ln -sf /dev/stderr start.out
RUN chmod +x $BASE_DIR/bin/docker-startup.sh

EXPOSE 8848
EXPOSE 9848
ENTRYPOINT  ls $BASE_DIR

ENTRYPOINT $BASE_DIR/bin/docker-startup.sh
