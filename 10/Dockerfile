FROM debian:stretch

# Update system and install required packages
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq \
    && apt-get install -y wget curl git unzip libtcnative-1 xmlstarlet gosu \
    && apt-get clean autoclean \
    && apt-get autoremove --yes \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/

# Oracle JDK
ENV ORACLE_JDK_VERSION jdk-10.0.1
ENV ORACLE_JDK_URL http://download.oracle.com/otn-pub/java/jdk/10.0.1+10/fb4372174a714e6b8c52526dc134031e/jdk-10.0.1_linux-x64_bin.tar.gz
RUN mkdir -p /opt/jdk/$ORACLE_JDK_VERSION && \
    wget --header "Cookie: oraclelicense=accept-securebackup-cookie" -O /opt/jdk/$ORACLE_JDK_VERSION/$ORACLE_JDK_VERSION.tar.gz $ORACLE_JDK_URL && \
    tar -zxf /opt/jdk/$ORACLE_JDK_VERSION/$ORACLE_JDK_VERSION.tar.gz --strip-components=1 -C /opt/jdk/$ORACLE_JDK_VERSION && \
    rm /opt/jdk/$ORACLE_JDK_VERSION/$ORACLE_JDK_VERSION.tar.gz && \
    update-alternatives --install /usr/bin/java java /opt/jdk/$ORACLE_JDK_VERSION/bin/java 100 && \
    update-alternatives --install /usr/bin/javac javac /opt/jdk/$ORACLE_JDK_VERSION/bin/javac 100

ENV JAVA_HOME /opt/jdk/${ORACLE_JDK_VERSION}
ENV JAVA_TRUSTSTORE ${JAVA_HOME}/jre/lib/security/cacerts
ENV JAVA_TRUSTSTORE_PASSWORD changeit

ENV PATH $JAVA_HOME/bin:$PATH

VOLUME ["${JAVA_HOME}"]

WORKDIR $JAVA_HOME