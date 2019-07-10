
# Platform Installation using DOCKER images

This page is about how to deploy a SCAVA instance on the behalf of Docker.

At the actual stage of the project, there two ways to get started with the docker images:
1. Ready-to-use images are stored on the [Crossminer Docker-hub account](https://hub.docker.com/u/crossminer/).
1. Build them from the [scava-deployment](https://github.com/crossminer/scava-deployment) repository. They have to be built from various Dockerfile's and with help of a docker-compose file.

## Summary of containers

The whole Docker stack consists of 11 services:

|Docker service name|Full Name|Default port| Comments |
|---|---|---|---|
|admin-webapp|Administration UI| 5601 | Built from /web-admin |
|oss-app|Metric Plateform| 8182 | Built from /metric-platform |
|oss-db|MongoDB (metrics storage)| 27017 | Built from /metric-platform to start with a pre-loaded database (few projects analysed) or use a clean MongoDB image for a clean installation (`image: mongo:3.4`). Can be used to connect a MongoDB visualisation tool |
|kb|Knowledge base| 8080 | Built from /KB |
|kb-db|Knowledge base DB (based on MongoDB)| 27018 | Built from /KB-db. Can be used to connect a MongoDB visualisation tool |
|api-gw|API Gateway| 8086 | Built from /api-gw |
|auth|Authentication| 8085 | Built from /auth |
|elasticsearch|ElasticSearch| 9200 | Pulled from docker hub acsdocker/elasticsearch:6.3.1-secured. Can be used to connect an ElasticSearch visualisation tool |
|kibiter|Kibiter (Bitergia’s customized Kibana)| 80 | Pulled from docker hub acsdocker/grimoirelab-kibiter:crossminer-6.3.1 |
|dashb-importer|Dashboard importer (to kibiter)| | No port exposed on the host |
|prosoul|Prosoul Quality Model Viewer| 8000 | Pulled from docker hub bitergia/prosoul |

## Prerequisites

In order to run Scava, you need to:

1. Edit the hosts of your machine, creating a new record for the IP address: `127.0.0.1` with hostname: `admin-webapp`
1. Edit the `docker-compose-build.yml` file and change:
    1. The environment variable `API-GATEWAY_VAR`, replacing `localhost`by the IP address of your host on service `admin-webapp`
    1. Make sure that the ports defined in the file are not already used on the host, and adjust the various ports as required for your setup. Note that the Kibiter dashboard is on port 80 by default.
    1. Update the `ALLOWED_HOST`directive to include the host name on service `prosoul`. This is used by Django on the prosoul image to publish the quality model used by Crossminer.
    
## Building the Docker images

The deployment setup is hosted in the [scava-deployment](https://github.com/crossminer/scava-deployment) repository. One needs to clone the repository locally in order to build and run the docker images.

To build all the required Docker images, simply go to the root of the cloned repository and issue the following command. This will rebuild all images, dismissing any cached layers.

```
$ docker-compose -f docker-compose-build.yml build --no-cache
```
This will build required images using the latest version of the binaries on the CI server and pull images hosted on docker hub.
    
## Setup Configurations
Some optional configurations can be made to customize the dockerized SCAVA instance. These configuration are applied to the docker-compose description files `docker-compose-build.yml` or `docker-compose-dockerhub.yml` and are applied every time that the instance runs.

### Data persistence
Volumes can be created to persist the data of the databases between execution of the Scava platform. To enable the creation of volumes uncomemnt the corresponding lines on the `oss-db` and `kb-db` services:

* On `oss-db`:
```yaml
    volumes: #creates volume on container
        - ~/oss-data:/data/db
```

* On `kb-db`:
```yaml
    volumes: #creates volume on container
        - ~/kb-data:/data/kb-db
```
### Multiple Workers Configuration
One instance of the metric-platform is only able to run one worker. Therefore, a setup where it is required to have more than one worker requires the deployment of multiple instances of metric platform.

The main instance of the metric platform runs under the service `oss-app`. This is the service started by default with the `master` and `apiServer` flags, and launchs the worker `w1`.

To enable a second worker, the `docker-compose-build.yml` (or `docker-compose-dockerhub.yml`) file must be edited and uncomented the service `oss-slave`. This service will launch a new instance of the metric platform that will only run one worker (with default name `w2`). This slave instance **do not have** the flags `master` or `apiServer`.

New slaves can be added (e.g. `oss-slave01`,`oss-slave02`,`oss-slave03`, etc.) by copy-paste of the `oss-slave` service and changing the name of service and name of the worker.
    
## Running the locally built docker images

To run the locally built images, run the following command. Note that if the images are not available they will be rebuilt.

```
$ docker-compose -f docker-compose-build.yml up
```

Access the administration web app by using the following address in the web browser: http://admin-webapp/
For login use user: admin  pass: admin

## Running the pre-built docker images

> Please note that the docker hub images are not yet ready! We're working on it! :-)

The easiest way to run the full Scava setup is to use the docker images [stored on Docker Hub](https://hub.docker.com/r/crossminer/). Use the `docker-compose-dockerhub.yml` file to download all required images and start the stack:

```
$ docker-compose -f docker-compose-dockerhub.yml up
```
Access the administration web app by using the following address in the web browser: http://admin-webapp/

For login use user: admin  pass: admin

## Post-install tasks

### Configuring the GitHub token

In order to use the GitHub connectors, one needs to setup an authentication mechanism. Simply create a authentication token in yourGitHub account, and create a new property in the webadmin UI:

* key: githubToken
* value: the github token created on the github account.

### Kibana dashboard

The first time Kibana is started, it will ask for a default index pattern. To select one, log into the dashboard (admin/admin), go to the dashboard menu item and select `metrics-scava`. Then click on the star on the top right. 

## Continuous integration

We use Codefresh for the CI of our docker images. The latest demo instance of generated docker images can be found in the `#ci` channel in Slack.
