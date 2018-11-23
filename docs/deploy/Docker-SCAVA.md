# Docker SCAVA

This page is about how to deploy a SCAVA instance on the behalf of Docker.

At the actual stage of the project, there two ways to get started with the docker images:
1. Ready-to-use images are stored on the [Crossminer Docker-hub account](https://hub.docker.com/u/crossminer/). (todo clarifications)
1. Build them from the [scava-deployment](https://github.com/crossminer/scava-deployment) repository. They have to be built from various Dockerfile's and with help of a docker-compose file. At the time being, we're testing the [dashboard-plus-admin branch](https://github.com/crossminer/scava-deployment/tree/dashboard-plus-admin).

The whole Docker stack consists of 11 services:

|Docker service name|Full Name|
|---|---|
|admin-webapp|Administration UI|
|oss-app|Metric Plateform|
|oss-db|MongoDB (metrics storage)|
|kb|Knowledge base|
|kb-db|Knowledge base DB (based on MongoDB)|
|api-gw|API Gateway|
|auth|Authentication|
|elasticsearch|ElasticSearch|
|kibiter|Kibiter (Bitergia’s customized Kibana)|
|dashb-importer|Dashboard importer (to kibiter)|
|prosoul|Prosoul|

(is the following still relevant ?)
The database comes pre-populated with a project and a user. The loaded dump comes from [md2manoppello's repo](https://github.com/md2manoppello/SCAVA_DUMP). Login information:

* user: `demo@crossminer.org`
* password: `demo18`

Custom quality is in the user object (demo@crossminer.org) stored in the users collection of users db. It resembles the [demo quality model](https://github.com/crossminer/crossminer/blob/dev/web/org-SCAVA-webapp/conf/quality/qualitymodel.json).

## Running the SCAVA docker image

The easiest way to build the full stack is to run the docker-compose file:

```
$ docker-compose up
```

This command will download the images and run them. The application is then available on [localhost:9000](http://localhost:9000).

## Building the SCAVA docker image

Two containers actually need to be built. They can be built individually.

### oss-platform

Build the image from the oss-platform directory:

```
$ docker build -t bbaldassari/SCAVA-platform .
Sending build context to Docker daemon  3.072kB
Step 1/5 : FROM openjdk:8-jdk
```

### oss-web

Build the image from the oss-web directory:

```
$ docker build -t bbaldassari/SCAVA-web .
Sending build context to Docker daemon  3.072kB
Step 1/7 : FROM openjdk:8-jre-alpine
```

## Continuous integration

We use Codefresh for the CI of our docker images. The latest demo instance of generated docker images can be found in the `#ci` channel in Slack.
