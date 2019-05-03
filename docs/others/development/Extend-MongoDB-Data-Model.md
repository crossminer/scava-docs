
# Extending MongoDB data model

## When to use ?

In this guideline, we describe ways to extend the Scava data model with the existing architecture of Scava. These guidelines are needed to keep order  the data layer of Scava platform during the evolution.

## Context

The Scava platform use MongoBb as database. The access to the database is managed using the Pongo , a framework which manage the mapping between MongoDb documents and Java class.

Each MongoDb document is mapped on a Java class which which extend the Pongo class.This Java class are generated form an emf file which describe the data model.

The current data model is composed of multiple documents which are mapped to several Pongo classes. This Java classes are organized in plugins :

* **The Platform data model (org.ossmeter.repository.model)** : Contains data related to project administration ,  metric execution process and authentification system.
* **Source Code Repositroy managers (org.ossmeter.repository.model.'project delta manager')** : Contains configuration informations related to source codes managemeny tools.
* **Metric Providers data models (in each metric provider plugins)** :  Each metric provider implementation contains his once data model.

## You need to Extend an Existing Data Model ?

The first way would be to make changes directly in the existing model. This option is to be used carefully as it may affect the rest of the platform modules. Therefore, it must be well checked, such that the rest of the part of the platform remains the same.

### 1. Locate the *.emf file of this data model

A presented previously, the Pongo Java class are generated form and EMF file which describe the data model. The file can be found in the implementaion plugin of each data model.

Ex : the platform data model Definition File can be find on the org.ossmeter.repository.model plugin (/src/org/ossmeter/repository/model/ossmeter.emf)

### 2. Update the Data  Model description

A data model description file contains a statical description of a MongoDb document.

```
@db
class ProjectRepository extends NamedElement {
  val Project[*] projects;
  val Role[*] roles;
  .
  val ProjectError[*] errors;
}

@customize
class ProjectError {
	attr Date date;
        .
	attr String stackTrace;
}
...
```

If we would like to add one more attribute to the element `ProjectError`, we could add it this way :

```diff
@db
class ProjectRepository extends NamedElement {
  val Project[*] projects;
  val Role[*] roles;
  .
  val ProjectError[*] errors;
}

@customize
class ProjectError {
	attr Date date;
        .
        .
        .
	attr String stackTrace;
+       attr String TestAttribute;
}
...
```
You can find more information about the data model description syntax at this url : https://github.com/kolovos/pongo/wiki/Model-Design-Guidelines

### 3. Generate the Java Class using the Pongo Tool.

* Download the Pongo tool : https://github.com/kolovos/pongo/releases
* Run the Pongo generator from the command line as follows: **java -jar pongo.jar  youremffile.emf**
* Replace the existing Java class by the new generated java class.

More information about Pongo  : https://github.com/kolovos/pongo/wiki

## You need to Create a new Data Model ?

The second way is to evolve the data model by building a new model/ database/ collection in Mongodb. This pongo model is separate from the existing model with separate database and thus avoids issues of breaking the existing model.

In this case, we invite you to create a new plugin which will contain your data model.

### 1. Create a new Eclipse Plug-In

* Create a new Eclipse Plug-In Project (
  - In Eclipse Toolbar : File > New > Plug-In Project
  - Name of the project : org.scava.**mycomponent**.repository.model
  - Disable the generation of an Activator Class / contribution to the ui
* Edit the MANIFEST.MF file
  - In Dependency : add a dependency to the **org.eclipse.core.runtime** plugin
  - In Dependency : add a dependency to the **com.googlecode.pongo.runtime** plugin
  - In Dependency : add a dependency to the **org.apache.commons.lang3** plugin
  - In Extentions : reference an extension point named **com.googlecode.pongo.runtime.osgi**
* In source directory
  - Create a package named org.scava.**mycomponent**.repository.model
  - In this package create an emf file named **mycomponent.emf**

A presented previously, the Pongo Java class are generated form and EMF file which describe the data model.Define your data model in this file :

```package org.scava.mycomponent.repository.model;

@db
class MyComponent {
     ....
}
```
You can find more information about the data model description syntax at this url : https://github.com/kolovos/pongo/wiki/Model-Design-Guidelines


### 2. Generate the Java Class using the Pongo Tool.

* Download the Pongo tool : https://github.com/kolovos/pongo/releases
* Run the Pongo generator from the command line as follows: **java -jar pongo.jar  youremffile.emf**
* Add this class in your org.scava.**mycomponent**.repository.model package

More information about Pongo  : https://github.com/kolovos/pongo/wiki


## Comment

Here we learnt ways to modify model in the Scava platform. To know more about the access of data with the Pongo APIs [link here](../admin/Access-to-MongoDB-database-using-PONGO).



***
