# Platform Administration User Guide
The guide show up the diffretens features available through the Administration Dashboard, including:


### The Login feature
The first time the user access the administration dashboard, a login form will be shown in order to authenticate the associated user.

![login-view](./screenshots/login-view.png)

### The Projects management feature
The Projects view displays the list of the OSS projects downloaded from the OSS forges.

![projects-view](./screenshots/projects-view.png)

The administration dashboard provides two operations:
* Import Project
If your project is hosted on an OSS forge, you can simply paste the URL on the field and add it.
![import-project-view](./screenshots/import-project-view.png)

* Create Project
The second operation provides an extra-options to customize the project creation alongside to the metadata available from differents related sources, eg., communication channels and bug tracking systems.
![create-project-view](./screenshots/create-project-view.png)

Once the project has been registred, it's possible to configure inside it some analysis tasks.

![analysis-task-view](./screenshots/analysis-task-view.png)

These tasks will be executed later to compute/calculate some metrics that will be used to measure the quality of the OSS projects during various period of time.

![project-config-view](./screenshots/project-config-view.png)


### The Users management feature
The Users view allows to manage the differents users of the the administration dashboards. It provides three levels of roles: USER ROLE, PROJECT MANAGER ROLE and ADMIN ROLE.
![users-management-view](./screenshots/users-management-view.png)

### The Workers feature
The workers view shows up the status of the analysis process of the metric-platform. The Platform Workers section illustres the metric-platform's available workers with theirs assigned analysis tasks. The Pending Tasks presents the analysis tasks waiting for a worker to be avalaible

![workers-view](./screenshots/workers-view.png)

### The Properties management feature
The Properties feature allows to configure generic configurations applied to the metric-platform, eg., Github OAuth tokens, ..

![properties-view](./screenshots/properties-view.png)
