
# Running the platform

This is a quick start guide to get the OSSMETER platform running from source.

Although these instructions may apply to other versions of Eclipse, they were tested under Eclipse Neon.3 with plug-in development support (Eclipse IDE for RCP Developers package).

A step-by-step video guide is also available at [https://youtu.be/3Ry4KKfNdYg](https://youtu.be/3Ry4KKfNdYg)

## Start MongoDB

You can download MongoDB from the [MongoDb website](http://www.mongodb.org/downloads).

Instructions for starting mongo can be found in the MongoDB [manual](http://docs.mongodb.org/manual/). For example:

````Shell
mongod --dbpath /data/db --port 27017
````

## Get the Code

Get the latest version of the code, and checkout the `dev` branch. Please don't commit to the `master` branch: see the [Development Guidelines](../development/Development-Guidelines):

If you are using __Linux / OS X__:
````Shell
git clone https://github.com/crossminer/scava.git scava
cd scava
git checkout dev
````

If you are using __Windows__ you need to do things differently due to Windows' long file name limit. In the Git shell:
````Shell
mkdir scava
cd scava
git init
git config core.longpaths true
git add remote origin https://github.com/crossminer/scava.git
git fetch
git checkout dev
````

## Setup Eclipse

Open Eclipse and import all projects from the top level directory of the Scava code (`File -> Import -> Existing projects into workspace`), and wait for all the projects to compile without errors.

## Validate and Run the Platform

Open `org.ossmeter.platform.osgi/ossmeterfromfeature.product`
  * Click the `Validate...` icon in the top right of the product configuration editor (the icon is a piece of paper with a tick)
  * If things do not validate, there's something wrong -- get in touch :) Problems related to `org.eclipse.e4.core.di` aren't critical.
  * Then, click the `Export an Eclipse product` on the left of the `Validate...` button. Uncheck the `Generate p2 repository` checkbox, select a destination directory and validate. After a while, the OSSMETER platform will be generated in the selected directory.
  * The platform can then be run using the generated `eclipse` binary; it accepts the following arguments:
    * `-apiServer`: Starts up the client API on localhost:8182
    * `-worker ${id-worker}`: Spawns a thread that analyses registered projects
  * To get a full platform running, first launch a master thread, then a slave, and finally the API server.

If you are developing code for the Scava platform, be sure to check out the [Contributing](../development/Contributing).

## Run the api-gateway

  * Right click on
`scava-api-gateway/src/main/java/org.eclipse.scava.apigateway/ApiGatewayApplication.java`
  * Then click on Run As -> Java Application

## Run the authentication service

  * Right click on
`scava-auth-service/src/main/java/org.eclipse.scava.authservice/AuthServiceApplication.java`
  * Then click on Run As -> Java Application

## Run the administration dashboard

Scava Administration is a single page web application based on Angular 6 Framework. To get started with Angular, it's better to install Angular CLI tool to make application development more quicker and easier (Find more here: https://angular.io/guide/quickstart).

The following instructions show how to run the dashboard web app:
  * Enter the `administration/scava-administration/` directory within the scava repository.
  * Run the web app on port 4200 using angular-cli: `ng serve`
  * Navigate to `http://localhost:4200/`

  
