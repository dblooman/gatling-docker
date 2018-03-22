FROM grafana/grafana:5.0.0

RUN apt-get update && apt-get install -y curl gettext-base && rm -rf /var/lib/apt/lists/*

COPY ./datasource.yaml /etc/grafana/provisioning/datasources/datasource.yaml
COPY ./dashboards.yaml /etc/grafana/provisioning/dashboards/dashboards.yaml
COPY ./default.json /var/lib/grafana/dashboards/default.json
