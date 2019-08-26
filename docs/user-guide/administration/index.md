# Platform Administration User Guide
The guide show up the diffretens features available through the Administration Dashboard, including:
* The Login feature
* The Projects management feature
* The Users management feature
* The Workers feature
* The Properties management feature
* The Stack Traces feature

### The Login feature
The first time the user access the administration dashboard, a login form will be shown in order to authenticate the associated user.

![login-view](./screenshots/login-view.png)

### The Projects management feature
The Projects view displays the list of the OSS projects downloaded from the OSS forges.

![projects-view](./screenshots/projects-view.png)

The administration dashboard provides two operations:
* Import Project: 
If your project is hosted on an OSS forge, you can simply paste the URL on the field and add it.
![import-project-view](./screenshots/import-project-view.png)

* Create Project:
The second operation provides an extra-options to customize the project creation alongside to the metadata available from differents related sources, eg., communication channels and bug tracking systems.
![create-project-view](./screenshots/create-project-view.png)

Once the project has been registred, it's possible to configure inside it some analysis tasks. A analisis task is consist of:
* Label name: the analysis task name.
* Task type: the scheduling tasks execution mechanism which could be:
  * Single Execution: which allow to run a task between a start date and an end date.
  * Monitoring Execution: which permits to run a task from a start date until the current date then to schedule the task execution each new day.
* Start date: the start time range of the analysis process.
* End date: the end time range of the analysis process.
* Metric Providers: the metrics available on the metric-platform through the extension points mechanism.

![analysis-task-view](./screenshots/analysis-task-view.png)

These tasks will be executed later to compute/calculate some metrics that will be used to measure the quality of the OSS projects during various period of time.

![project-config-view](./screenshots/project-config-view.png)


### The Users management feature
The Users view allows to manage the differents users of the the administration dashboards. It provides three levels of roles: * USER ROLE: 
* PROJECT MANAGER ROLE:
* ADMIN ROLE:
![users-management-view](./screenshots/users-management-view.png)

### The Workers feature
The workers view is dedicated to the dashboard administrators which allow them to monitor the status of the analysis tasks processes of the metric-platform. The Platform Workers section illustres the metric-platform's available workers with theirs assigned analysis tasks. The Pending Tasks presents the analysis tasks waiting for a worker to be avalaible

![workers-view](./screenshots/workers-view.png)

### The Properties management feature
The Properties feature allows to configure generic configurations applied to the metric-platform, eg., Github OAuth tokens, ..

![properties-view](./screenshots/properties-view.png)

### The Stack Traces feature
The Stack traces feature allows to display the errors/stracktraces produced during the metric-platform analysis process in the admin UI to ease debugging.

![stacktraces-view](./screenshots/stacktraces-view.png)
