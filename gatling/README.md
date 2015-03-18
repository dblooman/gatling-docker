Gatling-Docker
================

This container allows for running [Gatling](http://gatling.io/#/) load tests against a website or service.  

### Running on CI

This container can be used locally or on CI server such as Jenkins.  The workflow could enable load testing as a part of CI rather than at the end of a deliverable.

### Output

All results will be placed into the results directory.

### Building for local use

```sh
docker build -t davey/gatling .
```

### Running Locally

To run locally,

```sh
docker run --rm=true -v /path/to/gatling-docker/user-files/:/opt/gatling/user-files /
                     -v /path/to/gatling-docker/results:/opt/results /
                     davey/gatling -m -s TEST_SCRIPT -rf /opt/results
```
