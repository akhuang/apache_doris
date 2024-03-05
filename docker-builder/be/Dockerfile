# 选择基础镜像
FROM openjdk:8u342-jdk

# 设置环境变量
ENV JAVA_HOME="/usr/local/openjdk-8/" \
    PATH="/opt/apache-doris/be/bin:$PATH"

ENV tag_name=2.0.5
# 下载软件至镜像内，可根据需要替换
RUN apt-get install -y wget && \
    wget -O /opt/apache-doris-${tag_name}-bin-x64.tar.gz https://apache-doris-releases.oss-accelerate.aliyuncs.com/apache-doris-${tag_name}-bin-x64.tar.gz && \
    tar -xzvf /opt/apache-doris-${tag_name}-bin-x64.tar.gz -C /opt
# ADD ./resource/apache-doris-${tag_name}-bin-x64.tar.gz /opt/

RUN apt-get update && \
    apt-get install -y default-mysql-client && \
    apt-get clean && \
    mkdir /opt/apache-doris && \
    cd /opt && \
    mv apache-doris-${tag_name}-bin-x64/be /opt/apache-doris/be

ADD ./resource/init_be.sh /opt/apache-doris/be/bin
RUN chmod 755 /opt/apache-doris/be/bin/init_be.sh

ENTRYPOINT ["/opt/apache-doris/be/bin/init_be.sh"]