FROM centos:7

# install java
RUN yum -y update && yum install -y \
    bzip2 \
    unzip \
    xz-utils \
    python \
    java-1.8.0-openjdk-devel\
    vim \
    wget \
    open-ssl \
    gnupg2 \
    ca-certificates \
    tar

# set timezone
#update system timezone
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
#update application timezone
RUN echo "Asia/Shanghai" >> /etc/timezone

# Configure Flink version
ENV FLINK_VERSION=1.6.0 \
    HADOOP_SCALA_VARIANT=scala_2.11

# Prepare environment
ENV FLINK_HOME=/opt/flink
ENV PATH=$FLINK_HOME/bin:$PATH
WORKDIR $FLINK_HOME

ENV FLINK_URL_FILE_PATH=flink/flink-${FLINK_VERSION}/flink-${FLINK_VERSION}-bin-${HADOOP_SCALA_VARIANT}.tgz
# Not all mirrors have the .asc files
ENV FLINK_TGZ_URL=https://www.apache.org/dyn/closer.cgi?action=download&filename=${FLINK_URL_FILE_PATH} \
    FLINK_ASC_URL=https://www.apache.org/dist/${FLINK_URL_FILE_PATH}.asc

# Install Flink
RUN wget -nv -O flink.tgz "$FLINK_TGZ_URL"; \
    tar -xf flink.tgz --strip-components=1; \
    rm flink.tgz;