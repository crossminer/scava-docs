
# Authentication Component

The Scava Authentication service:

* Provides a centralized mechanisms to securize Scava's components and manage authentication for all services of the platform.
* Provides user management services, including user registration process, user profile editing and roles based authorization management.

## Authentication API

The Authentication server is a component of The Scava platform which manages the authentication for all  services accessible behind the API Gateway.

<table>
<tr><td>Authenticate User</td><td>POST</td><td>/api/authentication</td></tr>
<tr><td colspan="3">Login as a registered user.</td></tr>
</table>
<table>

### JSON Web Tokens (JWT)

JSON Web Token (JWT) is an open industry standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. It consists of three parts separated by dots (.), which are:
* Header
* Payload
* Signature

This solution uses a secure token that holds the information that we want to transmit and other information about our token, basically the user’s **login name** and **authorities**. (Find more about JWT: https://jwt.io/).

### JWT Authentication Implementation

* Users have to login to the authentication service API using their credentials username and password.
````
curl -i -X POST -H "Content-Type:application/json" http://localhost:8086/api/authentication -d '{"username":"admin", "password": "admin"}'
````
* Once the user is authenticated, he will get a JWT token in the HTTP Response Authorization Header.

<a href="https://ibb.co/jifgKJ"><img src="https://preview.ibb.co/nf8qDd/Screenshot_from_2018_07_17_16_55_23.png" alt="Screenshot_from_2018_07_17_16_55_23" border="0"></a>

* The generated token will be used by injecting it inside the HTTP Request Authorization Header to get access to the different Scava's components behind the API Gateway.
````
curl -i -X GET -H "Content-Type:application/json" -H "Authorization:Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJhZG1pbiIsImF1dGhvcml0aWVzIjpbIlJPTEVfQURNSU4iLCJST0xFX1BST0pFQ1RfTUFOQUdFUiIsIlJPTEVfVVNFUiJdLCJpYXQiOjE1MzE4OTk3NDMsImV4cCI6MTUzMTk4NjE0M30.l-iCJcnae-1mlhMb3_y09HM4HZYFaHxe_JctWi2FRUY" http://localhost:8086/api/users
````
<a href="https://ibb.co/nKpVUJ"><img src="https://preview.ibb.co/kFN63d/Screenshot_from_2018_07_17_17_43_49.png" alt="Screenshot_from_2018_07_17_17_43_49" border="0"></a>

## User Management API

The Authentication component provides web services for CRUD user account.

<table>
<tr><td>Register User</td><td>POST</td><td>/api/register</td></tr>
<tr><td colspan="3">Register new user.</td></tr>
</table>
<table>
<tr><td>Activate User</td><td>GET</td><td>/api/activate</td></tr>
<tr><td colspan="3">Activate the registered user.</td></tr>
</table>
<table>
<tr><td>Update User</td><td>PUT</td><td>/api/users</td></tr>
<tr><td colspan="3">Update an existing user.</td></tr>
</table>
<table>
<tr><td>Retrieve Users</td><td>GET</td><td>/api/users</td></tr>
<tr><td colspan="3">Get all registered users.</td></tr>
</table>
<table>
<tr><td>Retrieve Login User</td><td>GET</td><td>/api/users/{login}</td></tr>
<tr><td colspan="3">Get the "login" user.</td></tr>
</table>
<table>
<tr><td>Delete User</td><td>DELETE</td><td>/api/users/{login}</td></tr>
<tr><td colspan="3">Delete the "login" user.</td></tr>
</table>

## Authentication Server Configuration

The Authentication server parametrize inside an external property file (application.properties) placed in the same execution directory of the Authentication component.

### Server Configuration

<table>
<tr><td><b>id : </b>server.port</td><td><b>default :</b> 8085</td></tr>
<tr><td colspan="3">Port of the Authentication API server. Each REST request sent to the gateway must be adressed to this port.</td></tr>
</table>

### JWT Security Configuration

<table>
<tr><td><b>id : </b>apigateway.security.jwt.secret</td><td><b>default :</b> NA</td></tr>
<tr><td colspan="3">Private key pair which allow to sign jwt tokens using RSA.</td></tr>
</table>

### Default ADMIN configuration

Property| Description | Default Value
-------| --------|-----
scava.administration.username|The administrator username|admin
scava.administration.password|The administrator password|admin
scava.administration.admin-role|The admin role|ADMIN
scava.administration.project-manager-role|The project manager role|PROJECT_MANAGER
scava.administration.project-user-role|The user role|USER

### Mongodb Database Configuration

Property| Description | Default Value
-------| --------|-----
spring.data.mongodb.uri|Url of the MongoDB database server|mongodb://localhost:27017
spring.data.mongodb.database|Name of the MongoDB database|scava

### Mail Server configuration

In order to register new users, you have to configure a mail server.

Property| Description | Default Value
-------| --------|-----
spring.mail.host|Url of the mail service|smtp.gmail.com
spring.mail.port|Port of the mail service|587
spring.mail.username|Login of the mail account|
spring.mail.password|Password of the mail account|
spring.mail.protocol|mail protocole|smtp
spring.mail.tls|-|true
spring.mail.properties.mail.smtp.auth|-|true
spring.mail.properties.mail.smtp.starttls.enable|-|true
spring.mail.properties.mail.smtp.ssl.trust=|-|smtp.gmail.com

### Administration Dashboard Setting

<table>
<tr><td><b>id : </b>scava.administration.base-url</td><td><b>default :</b> http://localhost:4200</td></tr>
<tr><td colspan="3">The SCAVA administration base URL to generate the activation account URL.</td></tr>
</table>

## Packaging From Sources
Maven Packaging
```shell
mvn -Pprod install
```

## Authentication Server Execution
1. complete an put the "application.properties" configuration file in the execution directory.
1. Execute the scava-auth-service-1.0.0.jar Jar.
```shell
java -jar scava-auth-service-1.0.0.jar
```
