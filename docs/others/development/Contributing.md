
# Contributing

## Subcategories

* [SCAVA Repository Organisation](Repository-Organisation) Guideline describing how the SCAVA code repository is organised and how to add a new component in this repository.
* [How to name SCAVA components?](Component-Naming) Guideline describing naming constraints for a new scava component (component name, java namespace, maven artefact id and group id, etc.
* [How to name SCAVA REST services?](Naming-Scava-REST-Services) This guideline provide naming rules for each REST services routes implemented by the SCAVA platform.
* [How to manage  Licensing](Licensing) Guideline describing licensing requirements for SCAVA components.


## Technical Guidelines

### REST API

**Each implemented REST services must be documented (see /users directory): [REST API DOCUMENTATION](/developers-guide/api-reference-guide/metric-platform-api/)**

* [How to configure the SCAVA Gateway in order to integrate a new  REST service](../admin/API-Gateway-Configuration) Customers access SCAVA services through the SCAVA API Gateway. This guideline present how to configure the API Gateway to integrate new  remote service provider.
* [How to consume a SCAVA REST services](../users/Consuming-REST-Services) This guideline is dedicated to clients which would like to used SCAVA REST Services.It adress authentication issues.
* [How to implement Restlet services](Implementing-Restlet-Service) Guideline which describe how to integrate and implement a REST service in SCAVA platform using the RESTLET framework.

### DATA ACCESS

* [How to access MongoDB database using PONGO](../admin/Access to MongoDB database using PONGO) Guideline which describe how to the access to MongoDB database using the  PONGO framework.

* [How to extend the SCAVA data model](Extend-MongoDB-Data-Model) Guideline  which describe ways to extend the SCAVA Data Model, stored in a MongoDb database and based on the PONGO framework.

### OSGI

* [How to integrate OSGI service plugin in SCAVA Architecture](OSGI Component Integration) Todo
* [How to communicate between OSGI plugin using JMS](OSGI Plugin Communication) Todo
