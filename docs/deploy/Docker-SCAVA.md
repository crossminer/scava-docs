
# Docker SCAVA

This page is about how to deploy a SCAVA instance on the behalf of Docker.

At the actual stage of the project, there two ways to get started with the docker images:
1. Ready-to-use images are stored on the [Crossminer Docker-hub account](https://hub.docker.com/u/crossminer/).
1. Build them from the [scava-deployment](https://github.com/crossminer/scava-deployment) repository. They have to be built from various Dockerfile's and with help of a docker-compose file. At the time being, we're testing the [dashboard-plus-admin branch](https://github.com/crossminer/scava-deployment/tree/dashboard-plus-admin).

## Summary of containers

The whole Docker stack consists of 11 services:

|Docker service name|Full Name|Default port| Comments |
|---|---|---|---|
|admin-webapp|Administration UI| 80 | Built from /web-admin. |
|oss-app|Metric Plateform| 8182 | Built from /metric-platform. |
|oss-db|MongoDB (metrics storage)| 27017 | Built from /metric-platform. Can be used to connect a MongoDB visualisation tool. |
|kb|Knowledge base| 8080 | Built from KB. |
|kb-db|Knowledge base DB (based on MongoDB)| 27018 | Built from /KB-db. Can be used to connect a MongoDB visualisation tool. |
|api-gw|API Gateway| 8086 | Built from /api-gw. |
|auth|Authentication| 8085 | Built from /auth. |
|elasticsearch|ElasticSearch| 9200 | Pulled from docker hub acsdocker/elasticsearch:6.3.1-secured. Can be used to connect an ElasticSearch visualisation tool. |
|kibiter|Kibiter (Bitergia’s customized Kibana)| 5601 | Pulled from docker hub acsdocker/grimoirelab-kibiter:crossminer-6.3.1 |
|dashb-importer|Dashboard importer (to kibiter)| | No port exposed on the host. |
|prosoul|Prosoul Quality Model Viewer| 8000 | Pulled from docker hub acsdocker/prosoul. |

## Building the Docker images

The deployment setup is hosted in the [scava-deployment](https://github.com/crossminer/scava-deployment) repository. One needs to clone the repository locally in order to build and run the docker images.

To build all the required Docker images, simply go to the root of the cloned repository and issue the following command. This will rebuild all images, dismissing any cached layers.

```
$ docker-compose -f docker-compose-build.yml build --no-cache
```
This will build required images and pull images hosted on docker hub.

## Prerequisites

In order to run Scava, you need to:

* Edit the host machine's /etc/hosts file and add `127.0.0.1     admin-webapp`.
* Anything else?

## Running the locally built docker images

To run the locally built images, run the following command. Note that if the images are not available they will be rebuilt.

```
$ docker-compose -f docker-compose-build.yml up
```

## Running the pre-built docker images

The easiest way to run the full Scava setup is to use the docker images [stored on Docker Hub](https://hub.docker.com/r/crossminer/). Use the `docker-compose-dockerhub.yml` file to download all required images and start the stack:

```
$ docker-compose -f docker-compose-dockerhub.yml up
```


## Continuous integration

We use Codefresh for the CI of our docker images. The latest demo instance of generated docker images can be found in the `#ci` channel in Slack.
