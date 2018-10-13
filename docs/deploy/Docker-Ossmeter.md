
# Docker Ossmeter

This page lists information about the Ossmeter docker image. It should be noted that the generated image uses the old [Ossmeter binaries](https://github.com/ossmeter/ossmeter) and will not be updated -- all new development will go into the Crossminer repository.

All images are stored on the [Crossminer Docker-hub account](https://hub.docker.com/u/crossminer/dashboard/).

The Docker image is composed of 4 services: 

* oss-web: corresponds to the service of OSSMETER platform website.
* oss-app: service running api server and the orchestrator of OSSMETER slave instances.
* oss-slave: service corresponding to the OSSMETER slaves responsible for the analysis of software projects. There can be several slaves serving the same master for load balancing.
* oss-db: service responsible for the the storage of OSSMETER data. Uses a MongoDB image.

The database comes pre-populated with a project and a user. The loaded dump comes from [md2manoppello's repo](https://github.com/md2manoppello/OSSMETER_DUMP). Login information:

* user: `demo@crossminer.org`
* password: `demo18`

Custom quality is in the user object (demo@crossminer.org) stored in the users collection of users db. It resembles the [demo quality model](https://github.com/crossminer/crossminer/blob/dev/web/org-ossmeter-webapp/conf/quality/qualitymodel.json).

## Running the Ossmeter docker image

The easiest way to build the full stack is to run the docker-compose file:

```
$ docker-compose up
```

This command will download the images and run them. The application is then available on [localhost:9000](http://localhost:9000).

## Building the Ossmeter docker image

Two containers actually need to be built. They can be built individually.

### oss-platform

Build the image from the oss-platform directory:

```
$ docker build -t bbaldassari/ossmeter-platform .
Sending build context to Docker daemon  3.072kB
Step 1/5 : FROM openjdk:8-jdk
```

### oss-web

Build the image from the oss-web directory:

```
$ docker build -t bbaldassari/ossmeter-web .
Sending build context to Docker daemon  3.072kB
Step 1/7 : FROM openjdk:8-jre-alpine
```

## Continuous integration

We use Codefresh for the CI of our docker images. The latest demo instance of generated docker images can be found in the `#ci` channel in Slack.
