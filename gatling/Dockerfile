FROM java:openjdk-7u75-jre

RUN mkdir -p /opt/results
WORKDIR /opt

RUN apt-get update -y && apt-get install wget -y

RUN wget -O gatling.zip https://oss.sonatype.org/content/repositories/snapshots/io/gatling/highcharts/gatling-charts-highcharts-bundle/2.2.0-SNAPSHOT/gatling-charts-highcharts-bundle-2.2.0-20150317.093647-1-bundle.zip
RUN unzip gatling.zip
RUN mv gatling-charts-highcharts-bundle-2.2.0-SNAPSHOT/ gatling

WORKDIR /opt/gatling

ADD gatling-files/gatling.sh /opt/gatling/bin/gatling.sh
ADD gatling-files/gatling.conf /opt/gatling/conf/gatling.conf

RUN chmod 777 /opt/gatling/bin/gatling.sh

ENV PATH /opt/gatling/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV GATLING_HOME /opt/gatling

ENTRYPOINT ["gatling.sh"]
