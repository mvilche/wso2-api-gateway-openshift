FROM alpine:3.10

RUN apk add --no-cache --update shadow busybox-suid busybox-extras openjdk8 curl unzip wget bash

ENV WSO2_URL=https://bintray.com/wso2/binaryGA/download_file?file_path=wso2am-3.0.0.zip \
MYSQL_DRIVER=http://central.maven.org/maven2/mysql/mysql-connector-java/8.0.18/mysql-connector-java-8.0.18.jar

RUN wget ${WSO2_URL} -O /tmp/wso2.zip && \
cd tmp/ && unzip wso2.zip && mv wso2am-3.0.0 /opt/wso2 && \
rm -rf /tmp/*.zip && \
wget ${MYSQL_DRIVER} -O /opt/wso2/repository/components/dropins/mysql-connector-java-8.0.18.jar

COPY run /usr/bin/run

RUN mkdir -p /opt/custom_config && adduser -D -H -u 1001 api && usermod -aG 0 api && \
chown -R 1001 /opt /usr/bin/run && \
chgrp -R 0 /opt /usr/bin/run && \
chmod -R g=u /opt /usr/bin/run

USER 1001

ENV JAVA_HOME=/usr/lib/jvm/default-jvm

EXPOSE 9763 9443 9999 11111 8280 8243 5672 9711 9611 7711 7611 10397 9099

WORKDIR /opt/wso2

CMD ["/usr/bin/run"]
