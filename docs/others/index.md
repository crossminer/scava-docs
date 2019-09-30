
# Welcome to the Scava documentation

This web site is the main documentation place for the [Eclipse Scava](https://projects.eclipse.org/projects/technology.scava) project.

Useful links:

* Eclipse Scava home project: [Eclipse Scava @ Eclipse](https://projects.eclipse.org/projects/technology.scava)
* Eclipse Scava code repository: [github.com/crossminer/scava](https://github.com/crossminer/scava)
* Eclipse Scava deployment repository: [github.com/crossminer/scava-deployment](https://github.com/crossminer/scava-deployment)
* Eclipse Scava documentation repository: [github.com/crossminer/scava-docs](https://github.com/crossminer/scava-docs)

## Platform installation

* [Docker-SCAVA](deploy/Docker-SCAVA.md) How to build and run the Scava docker image.
* [Running the platform](deploy/Running-the-platform.md) Quick start guide to get the Scava platform running from source on an Eclipse development environment.
* [Configuring the platform](deploy/Platform-configuration.md) Quick start guide to present how to configure the platform using a configuration file.
* [Docker-OSSMETER](deploy/Docker-OSSMETER.md) How to build and run the Ossmeter docker image.

## Administration

* [Scava Administration](admin/SCAVA-Administration.md) The administration dashboard take care of managing Scava's services.
* [API Gateway Configuration](admin/API-Gateway-Configuration.md)
* [Extending MongoDB Data Model](admin/Extend-MongoDB-Data-Model.md)

## Users

* [Scava metrics](users/Scava-Metrics.md) lists metrics computed by the various Scava Components.
* [Consuming the REST services](users/Consuming-REST-Services.md) This guideline is dedicated to clients which would like to used SCAVA REST Services.It adress authentication issues
* [Running Scava in Eclipse](users/Running-Scava-in-Eclipse.md) How to setup and run the Scava Eclipse IDE plugin.
* [REST API Documentation](developers-guide/api-reference-guide/metric-platform-api/) Reference documentation of REST services provided by the Scava platform.
* [REST API Generation](users/REST-API-Generation.md) Tutorial about automatic generation of REST API Scava library using OpenAPI.
* [Accessing Scava resources](users/Scava-Resources.md) A summary of where to find the various outputs of the Scava platform.

## Development

* [Contributing](development/Contributing.md) Collection of Architectural and Technical guidelines dedicated to Scava developers.
* [Development guidelines](development/Development-Guidelines.md) Rules and guidelines used for the development of the Scava project.
* [Testing Guidelines](development/Testing-Guidelines.md) Collection of testing guidelines dedicated to Scava developers.
* [Repository-Organisation](development/Repository-Organisation.md)
* [How to develop a metric provider](development/How-To-Develop-Metric-Provider.md) Want to add a new metric provider? Here are some hints.
* [Licensing](development/Licensing.md) Information about licensing used within Scava.

## Architecture

* [API Gateway Component](architecture/API-Gateway-Component.md) The API Gateway allows to access to all Scava REST services using a centralised and securised common gateway.
* [Authentication Component](architecture/Authentication-Component.md) The administration dashboard takes care of managing Scava's services.
