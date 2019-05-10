FROM centos:7

ENV	UPDATE_VERSION=8u201
ENV	JAVA_VERSION=1.8.0_201

RUN	curl https://s3-ap-northeast-1.amazonaws.com/temp-bnb/java/jdk-8u201-linux-x64.tar.gz -o /tmp/jdk-${UPDATE_VERSION}-linux-x64.tar.gz \
&&  mkdir -p /usr/java \
&&  tar xzf /tmp/jdk-${UPDATE_VERSION}-linux-x64.tar.gz -C /usr/java \
&&  ln -s /usr/java/jdk${JAVA_VERSION} /usr/jdk  \
&&  alternatives --install /usr/bin/java java /usr/java/jdk${JAVA_VERSION}/bin/java 1  \
&&  alternatives --set java /usr/java/jdk${JAVA_VERSION}/bin/java  \
&&  rm /tmp/jdk-${UPDATE_VERSION}-linux-x64.tar.gz

ENV	JAVA_HOME=/usr/java/jdk${JAVA_VERSION}/
ENV PATH=$PATH:/usr/java/jdk${JAVA_VERSION}/bin

RUN yum makecache \
&&  yum install -y telnet vim iproute bind-utils \
&&  yum clean all

WORKDIR /opt/app

ADD run-java.sh /opt/app

RUN mkdir /opt/app/jmx \
&&  curl https://s3-ap-northeast-1.amazonaws.com/temp-bnb/java/jmx_prometheus_javaagent-0.11.0.jar -o /opt/app/jmx/jmx_prometheus_javaagent.jar \
&&  curl https://s3-ap-northeast-1.amazonaws.com/temp-bnb/java/jmx_config.yml -o /opt/app/jmx/jmx_config.yml

ENTRYPOINT /opt/app/run-java.sh
