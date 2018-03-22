Gatling InfluxDB-Grafana Stack
=================

Simple stack for using Gatling with InfluxDB and Grafana to get a real time view of results from load testing.  

### Running Gatling

I think it is best to run Gatling outside of Docker for local testing, logfiles and the result pages are easier to deal with.  Performance could also be a factor depending on what OS/environment you are running Docker on.  If you want to run Gatling inside a Docker container, there are some available on the registry.

### Docker Images

The 2 images for this setup are Grafana, front end, with InfluxDB for the backend.  

### Setup

Use docker-compose to build the images locally, edit the configuration files to your specific needs.

```sh
docker-compose build
```

### Running the Stack

Run

```
docker-compose up
```

You should see 2 container ID's and everything should be running.  Next visit [localhost:3000](http://localhost:3000)

This should now show you the Grafana Gatling dashboard preloaded into the Grafana image.  From this point on, as long as the InfluxDB image is running, you can save dashboards to it.  Once it goes down, all data will be lost.  Once you are done with the stack, export your dashboard.

### InfluxDB

All the options for InfluxDB are the influxdb directory, but the API interface is located at [localhost:8086](http://localhost:8086)

### Feeding Data in from Gatling

I have included a sample gatling.conf which is mostly the vanilla conf except for writers section under the data block, as well as the graphite options.  InfluxDB accepts data using the Graphite protocol, so by using these options, data will still go into the database as if it were Whisper database used by Graphite.
