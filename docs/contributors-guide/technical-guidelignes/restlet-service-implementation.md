# How to implement Restlet services

## When to use this guideline ?

This guideline present how to create a new REST service using the RESTLET framework in the Scava platform.

## Context

Scava project manages REST services with the RESTLET framework.

The usage of Restlet framework  has been inherited from the OSSMETER platform. The RESTLET framework is integrated in the platform in a single OSGI plugin :

* org.eclipse.crossmeter.platform.client.api.  

The RESTLET framework used an embedded web server. In order to avoid to multiply the number of deployed web servers, we plan to centralize all REST service implementation in the same plug-in.

## You want to access to create a new REST Service ?

### 1. Create a new Route

To  register a new RESTLET service, the first step is to define the route (base url which allow to access to this service) and make the link between this route an the implementation of the service.

#### Naming the Route

The routes (Base URL) of services provided by the platform is normalize. Please refer to this guideline to know ho to define the route of the new service : [Naming-Scava-REST-Services.html](Naming-Scava-REST-Services)

#### Register the Route

The `org.scava.platform.services` plug-in contained the class `PlatformRoute.java`  responsible for declaring routes.

```java
package org.scava.platform.services;
import org.restlet.Application;
import org.restlet.Restlet;
import org.restlet.routing.Router;

public class PlatformRoute extends Application {
	@Override
	public Restlet createInboundRoot() {
		Router router = new Router(getContext());

		router.attach("/", PingResource.class); 	
		router.attach("/search", SearchProjectResource.class);
                ...
                router.attach("/projects/p/{projectid}", ProjectResource.class);
		router.attach("/raw/metrics", RawMetricListResource.class);
		...
		return router;
	}
}
```

**Route Example :**
```java
router.attach("/raw/metrics", RawMetricListResource.class);
```
* **"/raw/metrics"**: Represent the route URL.
* **"RawMetricListResource.class"** : Represent the class where the service to be implemented for this path.

A route can contained some parameters. In this case, parameters are identified by a name with curly brackets `{}`.

### 2. Implement the Service

A service implementation is a Java class which extend the _ServerResource_ class provided by the RESTLET framework.
To create a new service create a new Class :
* Named "_ServiceName_" + Resource.  Ex : ProjectCreationResource.java
* On a namespace based on the  route. Ex : org.scava.platform.services.administration for platform administration services.
* Who extend the org.restlet.resource.ServerResource class.

#### GET Service

To implement a service of type GET, create a new method :
* Based on the following signature : public final Representation represent()
* Add the @Get("json") annotation

```java

@Get("json")
public final Representation represent() {
  // Initialise Response Header
  Series<Header> responseHeaders = (Series<Header>) getResponse().getAttributes().get("org.restlet.http.headers");
   if (responseHeaders == null) {
    responseHeaders = new Series(Header.class);
     getResponse().getAttributes().put("org.restlet.http.headers", responseHeaders);
  }
  responseHeaders.add(new Header("Access-Control-Allow-Origin", "*"));
  responseHeaders.add(new Header("Access-Control-Allow-Methods", "GET"));

  // Get Route parameter if required {projectid}
  String projectId = (String) getRequest().getAttributes().get("projectid");


  try {
    ....
    // Provide Result
    getResponse().setStatus(Status.SUCCESS_OK);
    return new StringRepresentation(...);
  } catch (IOException e) {
    StringRepresentation rep = new StringRepresentation("{\"status\":\"error\", \"message\" : \""+e.getMessage()+"\"}");
    rep.setMediaType(MediaType.APPLICATION_JSON);
    getResponse().setStatus(Status.CLIENT_ERROR_BAD_REQUEST);
    return rep;
  }
}

```

You can also extend the _AbstractApiResource_ , a service class  provided by the platform and dedicate to services who request a connection to MongoDb database instead of the _ServerResource_. In this case you will have to implement the doRepresent() method.

```java
public class RawMetricListResource extends AbstractApiResource {
	public Representation doRepresent() {
		ObjectNode res = mapper.createObjectNode();

		ArrayNode metrics = mapper.createArrayNode();
		res.put("metrics", metrics);
		...
		return Util.createJsonRepresentation(res);
	}
}
```


#### POST Service

To implement a service of type POST, crate a new method :
* Based on the following signature : public Representation _myServiceName_ (Representation entity)
* Add the @Post annotation

```java
@Post
public Representation myServiceName(Representation entity) {
  try {
    // Read Json Datas
    JsonNode json = mapper.readTree(entity.getText());

    ...

    // Provide Result
    getResponse().setStatus(Status.SUCCESS_CREATED);
    return new StringRepresentation(...);

  } catch (IOException e) {
    StringRepresentation rep = new StringRepresentation("{\"status\":\"error\", \"message\" : \""+e.getMessage()+"\"}");
    rep.setMediaType(MediaType.APPLICATION_JSON);
    getResponse().setStatus(Status.CLIENT_ERROR_BAD_REQUEST);
   return rep;
  }
}
```

#### DELETE Service
To do ....

### 3. Document the Service

The REST services are the main integration points between platform components or between the platform and external clients. This services are the implementation of a contract between the service provider and his consumers. In order to  allow an easy integration, this contract must be documented :

