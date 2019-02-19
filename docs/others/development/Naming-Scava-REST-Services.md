
# Naming Scava REST services

## When to use this guideline ? 
This guideline present how to define the route of a new REST service provided by the Scava platform.

## Context

The REST services are the main integration points between platform components or between the platform and external clients. In order to provide an unified view of  platform services , we need to used a common naming schema for all REST services provided by the platform.

## How to name a REST service ?

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


## Comment
