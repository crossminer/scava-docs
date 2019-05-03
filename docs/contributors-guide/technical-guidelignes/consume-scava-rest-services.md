# How to consume a SCAVA REST services

# When to use ?

This guideline describes general way of consuming REST services of Scava. Its basically for the use of Scava rest APIs in other tools/applications.

## REST API Reference

The reference guide presenting all REST services implemented by Scava is available [[right here |Development Guidelignes]].

## API Gateway

The Scava integrated platform provide a centralized access point to all web services implemented by the different tools involved in the platform : the Scava API Gateway.

**All web service request form clients have to go through the gateway.**

<img src="https://zupimages.net/up/18/07/k2wp.png" width="800">

The api gateway is in charge to redirect the client request to the right service provider. The gateway also manage authentication mechanism for all services provided by the integrated platform.


## Platform Authentication

The CROSSMIER API Gateway is secruized using JSON Web Tokens (JWT https://jwt.io).
1. To obtain an access to a specific service, the client must authenticate with the authentication service.If the authentication success,he recived a web token that should be include in the header of all of his future requests.
1. When the client request a specific service, the api gateway valivate the token from the authentication  service. If the token is valide, the api gateway transmite the request to the related service.


**Authentication in Java**

Retrieve a Web Tokens from authentication service
```java
private String getAuthToken(String login,String password) throws MalformedURLException, IOException, ProtocolException {
  // Authentication Service URI
  URL url = new URL("http://localhost:8086/api/authentication");

  // AUthentication Request
  HttpURLConnection connection = (HttpURLConnection) url.openConnection();
  connection.setDoOutput(true);
  connection.setRequestMethod("POST");
  connection.setRequestProperty("Content-Type", "application/json");

  String input = "{\"username\":\""+login+"\",\"password\":\""+password+"\"}";
  OutputStream os = connection.getOutputStream();
  os.write(input.getBytes());
  os.flush();

  if (connection.getResponseCode() != HttpURLConnection.HTTP_OK) {
    throw new RuntimeException("Failed : HTTP error code : "+ connection.getResponseCode());
  }

  connection.disconnect();

  // A JWT Token is return in the Header of the response
  return connection.getHeaderField("Authorization");
}
```

**REST Service Call**
```
curl -d '{"username":"admin", "password":"admin"}' -H "Content-Type: application/json" -X POST http://localhost:8086/api/authentication
```
## Service Consumption
To consume a REST service provided by the integrated platform, the client must include the Token in the header of his request.

 ```java
// Service URL
URL url = new URL("http://localhost:8086/api/users");
HttpURLConnection connection = (HttpURLConnection) url.openConnection();
connection.setRequestMethod("GET");

// Add Token to the request header
connection.setRequestProperty("Authorization",token);


