# SCAVA Naming recommendations

## Component Naming

As consequence of our status of project hosted by the eclipse foundation, we have to follow a specific naming schema for all components implemented in context of SCAVA project.

In this section, "component" means big funcional componen of the SCAVA project.

Component    | _ComponentId_
------------ | -------------
DevOps Dashboard | dashboard
Workflow Execution Engine | workflow
Knowledge Base | knowledgebase
Metric Provider | metricprovider
Administration | administration

## Project Naming

* For Eclipse Plugin 

```
org.eclipse.scava.{componentname}
```

* For Maven Project : the name of the project if the ArtifactId

If your component is composed of one project :
```
{component-name}
```

If your component is composed of several sub projects :
```
{sub-component-name}
 ```

## Source Code Namsespace
All sources must be nemspaces by : 
```
org.eclipse.scava.{componentname}
```

## Maven Ids
For  the Maven projects:

* If your component is composed of one project : 
``` 
Group Id : org.eclipse.scava
ArtifactId : {component-name}
```

* If your component is composed of several sub projects : 
``` 
Group Id : org.eclipse.scava.{component-name}
ArtifactId : {sub-component-name}
```

##  REST services Naming

The REST services are the main integration points between platform components or between the platform and external clients. In order to provide an unified view of  platform services , we need to used a common naming schema for all REST services provided by the platform.

#### How to name a REST service ?

> **/{_componentid_}/{_categoryname_}/{_servicename_}**

* **/_componentid_/**: Name of the Architectural component which provide the service
* **/_categoryname_/ (Optional)** : optional category of the service
* **/_servicename_/** : Name of the rest service

#### Component

Component    | _ComponentId_
------------ | -------------
DevOps Dashboard | dashboard
Workflow Execution Engine | workflow
Knowledge Base | knowledgebase
Metric Provider | metricprovider
Administration | administration




