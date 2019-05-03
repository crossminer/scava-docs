# How to access to MongoDB using PONGO

## When to use ?

This guideline present How to the Scava Platform can access to his data stored in a MongoDb data base. The guideline describe how to create a connection to the MongoDb database and how to perform CRUD operation on platform datas.

## Context

The Scava platform use a MongoDb data base to store his data. We go through **PONGO**, a template based _Java POJO generator_ to access **MongoDB** database. With Pongo we can define the data model which generates strongly-typed Java classes.

In this guideligne, we will present  : 
* The access to MongoDb Document on from aneclipse plugin integrate to the Scava platform.
* The access to MongoDb Document on from an external Java application.
* How to preform basic CRUD operation with a PONGO Java data model.

We consider that the PONGO Java data model already exist. If it's not the case, please refer the following guideline to create the data model : [Extend MongoDB Data Model](../development/Extend-MongoDB-Data-Model).

## You want to access to MongoDB Document from an Eclipse Plugin ?

### 1. Add a dependency to the Java Data Model

* Edit the plugin.xml file of your plugin.
* In Dependency section, add a dependency to  the plugin which contained the data model you went to access.
  - To **org.ossmeter.repository.model** to access data related to project administration , metric execution process and authentification system.
  - To **org.ossmeter.repository.model.'project delta manager'** to access  configuration informations related to source codes managemeny tools.
  - To  **specific metric provider plugins**  to access data related to a specific metric provider implementation contains his once data model.
  - ... others plugin which contained the data model
* In Dependency section, add a dependency to **com.googlecode.pongo.runtime** plugin

<a href="http://ibb.co/kEi236"><img src="http://preview.ibb.co/ccjWwR/Pongo_dependency_addition.png" alt="Pongo dependency addition" border="0" /></a>

### 2. Initiate a Connection to the MongoDb

In context of the Scava platform, a Configuration service allow you to initiate a connection whit the mongoDb data base.

* In Dependency section of plugin.xml file , add a dependency to the **org.ossmeter.platform** plugin.
* You can now create a new connection to the database using the Configuration service.

```java
Mongo mongo = Configuration.getInstance().getMongoConnection(); 
```

## You want to access to MongoDB Document on from an External Java Application ?

### 1. Add a dependency to the Java Data Model
* Add to your java project a dependency to the jar which contained  the data model you went to access. You will have to deliver this jar with your application.

<a href="http://imgbb.com/"><img src="http://image.ibb.co/kqmriG/MongoJAr.png" alt="MongoJAr" border="0" /></a>

* Add o your java project a dependency to the **pongo.jar** jar file which can be download at this url : https://github.com/kolovos/pongo/releases

### 2. Initiate a Connection to MongoDb

```java
// Define ServerAddress of the MongoDb database
List<ServerAddress> mongoHostAddresses = new ArrayList<>();
mongoHostAddresses.add(new ServerAddress(s[0], Integer.valueOf(s[1])));

// Create Connection
Mongo mongo = new Mongo(mongoHostAddresses);
```
Once the connection to MongoDb has been created, you have to make the link  between the PONGO Java model and the database. On a MongoDb Server, data are organize by database. You need to know the name of the database to link the Java model with the MongoDb document.

```java
DB db =  mongo.getDB("databasename");

// Initiate the Project Java model
ProjectRepository = new ProjectRepository(db);
```

## Basic CRUD with a PONGO Java data model


### 1. CREATE

```java
// Connect the Data model to the database
DB db =  mongo.getDB("databasename");
MetricProvider metricprovider = new MetricProvider(db);

// Used accessors to intialise the object
metricprovider.setName("Metric1").
......
 
// Create the Document
metricprovider.sync(true);
```
### 2. READ

```java
// Connect the Data model to the database
DB db =  mongo.getDB("databasename");
MetricProvider metricprovider = new MetricProvider(db);

// Used accessors to access object properties
metricprovider.getname();
......
```

### 3. UPDATE

```java
// Connect the Data model to the database
DB db =  mongo.getDB("databasename");
MetricProvider metricprovider = new MetricProvider(db);

// Used accessors to intialise the object
metricprovider.setName("Metric1").
......
 
// Create the Document
metricprovider.sync(true);
```

### 4. DELETE

Mongo mongo = new Mongo();
mongo.dropDatabase("databasename");


