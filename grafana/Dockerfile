FROM debian:wheezy
MAINTAINER David Blooman <david.blooman@gmail.com>

RUN apt-get -y update
RUN apt-get -y install python wget

RUN mkdir /src

RUN wget http://grafanarel.s3.amazonaws.com/grafana-1.9.1.tar.gz
RUN tar xzvf grafana-1.9.1.tar.gz && rm grafana-1.9.1.tar.gz
RUN mv grafana-1.9.1 /src/grafana

ADD config.js /src/grafana/config.js
ADD default.json /src/grafana/app/dashboards/default.json

ONBUILD COPY default.json /src/grafana/app/dashboards/default.json

WORKDIR /src/grafana

EXPOSE 8080

CMD ["python", "-m", "SimpleHTTPServer", "8081"]
