
# Scava Administration

The SCAVA administration dashboard take care of:

* Provide user administration feature, including user profile activation service and roles based authorization management.
* Provide services to analyse automatically open source software projects.

## Administration Dashboard Installation

### Prerequired

The SCAVA administration dashboard  is front end web application based on Angular Framework. It can be executed in both Linux or Windows systems where it's required the installation of the following tools:

#### Node.js

* Download Node.js ver. 8.11.2 (includes npm 5.6.0) or above : https://nodejs.org/en/download/

#### Yarn Package Manager

* Download Yarn ver. 1.7.0 or above : https://yarnpkg.com

### Get Started Scava Administration

Scava Administration is a single page web application based on Angular 6 Framework. To get started with Angular, it's better to install Angular CLI tool to make application development more quicker and easier (Find more here: https://angular.io/guide/quickstart).

## Scava Dashboard Deployment

In order to deploy the Scava Administration, you must to build and copy the output directory to a web server (For instance Apache HTTP Server).

### Using the development profile:

* Execute the development build using the Angular CLI command line : `ng build`.
* Copy everything within the output folder (dist/ by default) to a folder on the server.
* If you copy the files into a server sub-folder, append the build flag, --base-href and set the <base href> appropriately. For example, if the index.html is on the server at /administration/index.html, set the base href to <base href="/administration/"> like this. or simply you can run: `ng build --base-href=/administration/`

### Using the production profile:

* You can generate an optimized build with additional CLI command line flags: `ng build -- prod`.
* Copy everything within the output folder (dist/ by default) to a folder on the server.
* If you copy the files into a server sub-folder, append the build flag, --base-href and set the <base href> appropriately. For example, if the index.html is on the server at /administration/index.html, set the base href to <base href="/administration/"> like this. or simply you can run: `ng build --base-href=/administration/`.
