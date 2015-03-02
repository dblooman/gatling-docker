Gatling InfluxDB-Grafana Stack
=================

Simple stack for using Gatling with InfluxDB and Grafana to get a real time view of results from load testing.  

### Running Gatling

I think it is best to run Gatling outside of Docker for local testing, logfiles and the result pages are easier to deal with.  Performance could also be a factor depending on what OS/environment you are running Docker on.  If you want to run Gatling inside a Docker container, there are some available on the registry.

### Docker Images

The 2 images for this setup are Grafana, front end, with InfluxDB for the backend.  The InfluxDB image is based off of the Tutum image, but I have included the full Dockerfile for reference.  

### Setup

Both the images are available on the registry, or you can build your own using the Dockerfiles.  In both the InfluxDB and Grafana directories, you can use ONBUILD to add your own custom config.toml file and config.js respectively.  There include configs give a good starting point, but the influxDB regular expressions are greedy, so I suggest you edit them in the view, export them and replace when you are happy with your setup.

### Running the Stack

The simplest way to start the stack is to use the start script in terminal `./start`

You should see 2 container ID's and everything should be running.  Next visit [localhost:8081](http://localhost:8081) or your boot2dockerIP and port e.g [http://192.168.59.103:8081/](http://192.168.59.103:8081/)

This should now show you the Grafana Gatling dashboard preloaded into the Grafana image.  From this point on, as long as the InfluxDB image is running, you can save dashboards to it.  Once it goes down, all data will be lost.  Once you are done with the stack, export your dashboard.

To view the Grafana dashboard across your LAN, you'll need to forward ports for the [boot2docker-vm manually](https://github.com/boot2docker/boot2docker/blob/master/doc/WORKAROUNDS.md#port-forwarding):

```bash
$ VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port8081,tcp,,8081,,8081"
$ VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port8086,tcp,,8086,,8086"
```

Note that this does require the vm to be stopped and restarted - so, `boot2docker stop`, set the forwarding, and then `boot2docker up` again.

### InfluxDB

All the options for InfluxDB are the influxdb directory, but the web interface is located at [localhost:8083](http://localhost:8083) or your boot2dockerIP and port e.g [http://192.168.59.103:8083/](http://192.168.59.103:8083/)

Login and click the database tab to view the gatling data.  Once here, you can type `list series` to view all data in the dashboard.  InfluxDB using a SQLish query language, so queries are straight forward once you know the data format.

### Feeding Data in from Gatling

I have included a sample gatling.conf which is mostly the vanilla conf except for writers section under the data block, as well as the graphite options.  InfluxDB accepts data using the Graphite protocol, so by using these options, data will still go into the database as if it were Whisper database used by Graphite.
