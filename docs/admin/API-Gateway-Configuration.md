
# API Gateway configuration

## When to use this guideline ?

This guideline presents how to configure the Scava Gateway in order to integrate a new remote REST API.

## Context 

The Scava Gateway can be configured by the intermediary of an external property file (application.properties) to place in the execution directory of the Scava Gateway component. This file allow to configure the routing of requests send to the gateway an some security parameters.

### Routing : Service Configuration

To reference a new remote REST API in the gateway, you have to add  2 new properties in the application.properties configuration file : the relative path of services  which will be integrated to this route and the redirection URL.All requests sent to the gateway which start by this relatice path will be redirected to the output url after the authentication process.

Examples :
* api gateway url = http://85.36.10.13:8080
* path = /administration/**
* url = http://85.36.10.12:8082/administration

The request http://85.36.10.13:8080/administration/project/create will be redirected to http://85.36.10.12:8082/administration/project/create

<table>
<tr><td><b>id : </b>zuul.routes.**servicename**.path</td><td><b>default :</b> NA</td></tr>
<tr><td colspan="3">Relative path of the incoming service which will be redirected. Example : /test1/**</td></tr>
</table>

<table>
<tr><td><b>id : </b>zuul.routes.**servicename**.url</td><td><b>default :</b> NA</td></tr>
<tr><td colspan="3">Redirection URL of the route. Example : http://127.0.0.1:8082/test1</td></tr>
</table>

### Configuration file example

```
# Rooting Configuration : Test1 Service
zuul.routes.test1.path=/test1/**
zuul.routes.test1.url=http://127.0.0.1:8082/test1

# Rooting Configuration : Test2 Service
zuul.routes.test2.path=/test2/**
zuul.routes.test2.url=http://127.0.0.1:8083/test2
```

## Comments

More information about API Gateway configuration: [API Gateway Component](../architecture/API-Gateway-Component)
