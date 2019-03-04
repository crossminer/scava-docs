
# Running the Administration Application form Sources

## Prerequisites:
* Start running the [Metric Platform](./analysis-platform.md#running-the-analysis-platform-form-sources).

## Development Toolkits
Scava Administration is a based on Angular 6 Framework. To get started with Angular, it's better to install Angular CLI 6.1.4 tool to make application development more quicker and easier (Find more here: [https://angular.io/guide/quickstart](https://angular.io/guide/quickstart)).

````Shell
sudo npm install @angular/cli@6.1.4
````

## Get the Code

Get the latest version of the code, and checkout the `dev` branch. Please don't commit to the `master` branch: see the [Development Guidelines](../../contributors-guide/contributors-guidelignes/scava-developement-process.md#source-code-repository):

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

## Run the Administration webapp

The following instructions show how to run the dashboard web app from source:
  * Enter the `administration/scava-administration/` directory within the scava repository.
  * Install Angular dependency using `npm install`
  * Run the web app on port 4200 using angular-cli: `ng serve`
  * Navigate to `http://localhost:4200/`

  
