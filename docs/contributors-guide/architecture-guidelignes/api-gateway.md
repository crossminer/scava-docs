
# API Gateway component

The Scava API Gateway :

* Provide a centralized access point to all web services implemented by the differents tools involved in the platform (DevOps Dashboard, Workflow Execution Engine, Knowledge Base, Metric Provider, Administration Application).
* Provide a centralized mechanisms to secuerize Scava web services and manage authentication  required to access to this services.

## API Gateway Architecture

The API Gateway  is a pattern which come form microserivces echosystem. An API Gateway is a single point of entry (and control) for front end clients, which could be browser based or mobile. The client only has to know the URL of one server, and the backend can be refactored at will with no change.

The API Gateway act as a revers web proxy in which can be integrated others functions like load balancing and authentication. In case of the Scava platform, the  API Gateway will manage the authentication for all services of the platform.  

<img src="https://zupimages.net/up/18/07/k2wp.png" width="800">



## Authentication Mechanism

#### JSON Web Tokens

The Scava API Gateway is secruized using JSON Web Tokens (JWT) mechanism, an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.

In authentication, when the user successfully logs in using their credentials, a JSON Web Token will be returned and must be saved locally, instead of the traditional approach of creating a session in the server and returning a cookie.When the client request an access to a protected service ,the server's protected routes will check for a valid JWT in the Authorization header of the request, and if it's present, the user will be allowed to access protected resources. (More about JWT : https://jwt.io)


<img src="https://cdn.auth0.com/content/jwt/jwt-diagram.png" width="600">

#### Authentication Architecture

In Scava, the authentification service is a sub component of the Administration Application which centralise Right Management for the whole platform. As for the others services, the authentication service is accessed behind the API Gateway.

<img src="https://zupimages.net/up/18/07/y9nf.png" width="300">

#### Authentication Flow
1. To obtain an access to a specific service, the client must authenticate with the authentication service.If the authentication success,he recived a web token that should be include in the header of all of his future requests.
1. When the client request a specific service, the api gateway valivate the token from the authentication  service. If the token is valide, the api gateway transmite the request to the related service.

<img src="https://zupimages.net/up/18/07/4i2a.png" width="600">

## Implementation

The implementation of the gateway is based on Zuul proxy, a component of the spring-cloud project, an extention of the spring framework dedicated to microservices architectures.

https://projects.spring.io/spring-cloud/spring-cloud.html#_router_and_filter_zuul

## API Gateway Configuration

The Scava Gateway can be configured by the intermediary of an external property file (application.properties) to place in the execution directory of the Scava Gateway component. This file allow to configure the routing of requests send to the gateway an some security parameters.

### Server Configuration

<table>
<tr><td><b>id : </b>server.port</td><td><b>default :</b> 8086</td></tr>
<tr><td colspan="3">Port of the CORSSMINER API server. Each REST request sent to the gateway must be addressed to this port.</td></tr>
</table>


### JWT Security Configuration

<table>
<tr><td><b>id : </b>apigateway.security.jwt.secret</td><td><b>default :</b> NA</td></tr>
<tr><td colspan="3">Private key pair which allow to sign jwt tokens using RSA.</td></tr>
</table>

<table>
<tr><td><b>id : </b>apigateway.security.jwt.url</td><td><b>default :</b> /login</td></tr>
<tr><td colspan="3">URL Path of the authentication service.</td></tr>
</table>

<table>
<tr><td><b>id : </b>apigateway.security.jwt.expiration</td><td><b>default :</b> 86400 (24H)</td></tr>
<tr><td colspan="3">Port of the CORSSMINER API server. Each request sent to the gateway must be addressed to this port.</td></tr>
</table>

### Routing : Authentication Service Configuration

<table>
<tr><td><b>id : </b>zuul.routes.auth-center.path</td><td><b>default :</b> /api/authentication/**</td></tr>
<tr><td colspan="3">Relative path of the authentication service.</td></tr>
</table>
<table>
<tr><td><b>id : </b>zuul.routes.auth-center.url</td><td><b>default :</b> NA</td></tr>
<tr><td colspan="3">URL of the authentification server. Example: http://127.0.0.1:8081/ </td></tr>
</table>
<table>
<tr><td><b>id : </b>zuul.routes.auth-center.sensitiveHeaders</td><td><b>default :</b> Cookie,Set-Cookie</td></tr>
<tr><td colspan="3">Specify a list of ignored headers as part of the route configuration which will be not leaking downstream into external servers.</td></tr>
</table>

<table>
<tr><td><b>id : </b>zuul.routes.auth-center.stripPrefix</td><td><b>default :</b> false</td></tr>
<tr><td colspan="3">Switch off the stripping of the service-specific prefix from individual routes</td></tr>
</table>

### Routing : Service Configuration


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
#API Gateway Port
server.port=8086

# JWT Configuration
apigateway.security.jwt.secret=otherpeopledontknowit
apigateway.security.jwt.url=/api/authentication
apigateway.security.jwt.expiration=86400

# Rooting Configuration : Authentication Service
zuul.routes.auth-center.path=/api/authentication/**
zuul.routes.auth-center.url=http://127.0.0.1:8081/
zuul.routes.auth-center.sensitiveHeaders=Cookie,Set-Cookie
zuul.routes.auth-center.stripPrefix=false


# Rooting Configuration : Test1 Service
zuul.routes.test1.path=/test1/**
zuul.routes.test1.url=http://127.0.0.1:8082/test1

# Rooting Configuration : Test2 Service
zuul.routes.test2.path=/test2/**
zuul.routes.test2.url=http://127.0.0.1:8083/test2
```

### Control access API

The Scava platform comes with public and private APIs to control the access to the REST API using different permission levels. By default, there are three authorization levels which are predefined to get access to all the Scava's APIS, including:
* “ROLE_ADMIN”
* “ROLE_PROJECT_MANAGER”
* “ROLE_USER”

By the way, The frontend SCAVA administration comes with a default “admin” who is mainly the admin user with all authorities access including “ROLE_ADMIN”, “ROLE_PROJECT_MANAGER” and “ROLE_USER” authorizations. His default password is “admin”.

```
# Filtering private restApi

scava.routes.config.adminAccessApi[0]=/api/users
scava.routes.config.adminAccessApi[1]=/api/user/**

scava.routes.config.projectManagerAccessApi[0]=/administration/projects/create
scava.routes.config.projectManagerAccessApi[1]=/administration/projects/import
scava.routes.config.projectManagerAccessApi[2]=/administration/analysis/**

scava.routes.config.userAccessApi[0]=/administration/projects
scava.routes.config.userAccessApi[1]=/administration/projects/p/**
scava.routes.config.userAccessApi[2]=/api/users/**
scava.routes.config.userAccessApi[3]=/api/account
```

## Packaging Form Sources

Maven Packaging
```shell
mvn -Pprod install
```

## API Gateway Execution

1. complete an put the "application.properties" configuration file in the execute directory.
1. Execute the crossmeter-api-gateway-1.0.0.jar Jar.
```shell
java -jar scava-api-gateway-1.0.0.jar
```

## Client Implementation

[How to consume a Scava REST services ?](../users/Consuming-REST-Services) \
This guideline is dedicated to clients which would like to use the REST Services. It adresses authentication issues.
