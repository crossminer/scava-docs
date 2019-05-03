
# REST API Documentation

## Project Administration API

The Administration API provides services related to platform administration, user management  and registration of projects to  be analyse by the platform.

> Base URL : **"/administration/"**

### Project Management

Manage registration of projects analysed by the platform.

<table>
<tr><td>Projects List</td><td>GET</td> <td> /administration/projects/{page}</td></tr>
<tr><td colspan="3">Retrieve a list of monitored projects.</td></tr>
</table>

<table>
<tr><td>Project Search</td><td>GET</td> <td> /administration/projects/search</td></tr>
<tr><td colspan="3">Retrieve a list of monitored projects base on a search query.</td></tr>
</table>

<table>
<tr><td>Project Info</td><td>GET</td> <td> /administration/projects/{projectId}</td></tr>
<tr><td colspan="3">Retrieve the metadata of a specific project.</td></tr>
</table>

<table>
<tr><td>Import Project</td><td>POST</td> <td> /administration/projects/import</td></tr>
<tr><td colspan="3">Import a new project to be analyzed by the platform. Take as input the URL of the repository of the project to import.</td></tr>
</table>

<table>
<tr><td>Register Project</td><td>POST</td> <td> /administration/projects/register</td></tr>
<tr><td colspan="3">Register a new project to be analyzed by the platform. Take as input the definition of project to analyse.</td></tr>
</table>

### Project Analysis

Analyse projects registered on the platform.

<table>
<tr><td>Create Analysis Task</td><td>POST</td> <td> /administration/task/create</td></tr>
<tr><td colspan="3">Create a new analysis task.</td></tr>
</table>

<table>
<tr><td>Update Analysis Task</td><td>PUT</td> <td> /administration/task/update</td></tr>
<tr><td colspan="3">Update an analysis task.</td></tr>
</table>

<table>
<tr><td>Start Analysis Task</td><td>POST</td> <td> /administration/task/start</td></tr>
<tr><td colspan="3">Start an analysis task.</td></tr>
</table>

<table>
<tr><td>Stop Analysis Task</td><td>POST</td> <td> /administration/task/stop</td></tr>
<tr><td colspan="3">Stop an analysis task.</td></tr>
</table>

<table>
<tr><td>Reset Analysis Task</td><td>POST</td> <td> /administration/task/reset</td></tr>
<tr><td colspan="3">Reset an analysis task.</td></tr>
</table>

<table>
<tr><td>Delete Analysis Task</td><td>DELETE</td> <td> /administration/task/delete/{analysisTaskId}</td></tr>
<tr><td colspan="3">Delete an analysis task.</td></tr>
</table>

<table>
<tr><td>Analysis Tasks List</td><td>GET</td> <td> /analysis/tasks</td></tr>
<tr><td colspan="3">Retrieve a list of analysis tasks.</td></tr>
</table>

<table>
<tr><td>Analysis Task</td><td>GET</td> <td>/analysis/task/{analysistaskid}</td></tr>
<tr><td colspan="3">Retrieve an analysis task by Id.</td></tr>
</table>

<table>
<tr><td>Analysis Tasks List By Project</td><td>GET</td> <td> /analysis/tasks/project/{projectid}</td></tr>
<tr><td colspan="3">Retrieve a list of analysis tasks by project.</td></tr>
</table>

<table>
<tr><td>Analysis Tasks Status By Project</td><td>GET</td> <td> /analysis/tasks/status/project/{projectid}</td></tr>
<tr><td colspan="3">Retrieve a gloabl status of the analysis tasks by project.</td></tr>
</table>

<table>
<tr><td>Workers List</td><td>GET</td> <td> /analysis/workers</td></tr>
<tr><td colspan="3">Retrieve a list of workers.</td></tr>
</table>

<table>
<tr><td>Metric Providers List</td><td>GET</td> <td> /analysis/metricproviders</td></tr>
<tr><td colspan="3">Retrieve a list of Metric Providers.</td></tr>
</table>

<table>
<tr><td>Promote Analysis Task</td><td>DELETE</td> <td> /analysis/task/promote/{analysisTaskId}</td></tr>
<tr><td colspan="3">Push up an analysis task in Workers Queue.</td></tr>
</table>

<table>
<tr><td>Demote Analysis Task</td><td>DELETE</td> <td> /analysis/task/demote/{analysisTaskId}</td></tr>
<tr><td colspan="3">Push down an analysis task in Workers Queue.</td></tr>
</table>

<table>
<tr><td>Push Analysis Task On Worker</td><td>DELETE</td> <td> /analysis/task/pushOnWorker/{analysisTaskId}/w/{workerId}</td></tr>
<tr><td colspan="3">Force the execution of an analysis task by a worker.</td></tr>
</table>

## Metrics Provider API

Access to Mertics collected  by the Metrics Provider component.

<table>
<tr><td>List of Metrics</td><td>GET</td> <td> /metricprovider/metrics</td></tr>
<tr><td colspan="3">Retrieve a list of the visualisable metric providers supported by the plat-
form. It includes information about how the metric provider should be visualised.</td></tr>
</table>


<table>
<tr><td>List of Raw Metrics</td><td>GET</td> <td> /metricprovider/raw/metrics</td></tr>
<tr><td colspan="3">Retrieve a list of the all of the metric providers supported by the plat-
form.</td></tr>
</table>

<table>
<tr><td>List of Metric Visualisation</td><td>GET</td> <td> /metricprovider/projects/p/{projectId}/m/{metricId}</td></tr>
<tr><td colspan="3">Retrieve the visualisation of a specific project metric provider. Visuali-
sations are defined in the MetVis language.</td></tr>
</table>

<table>
<tr><td>List of Factoids</td><td>GET</td> <td> /metricprovider/factoids</td></tr>
<tr><td colspan="3">Retrieve a list of factoids supported by the platform.</td></tr>
</table>

<table>
<tr><td>List of Project Factoids</td><td>GET</td> <td> /metricprovider/projects/p/{projectId}/f</td></tr>
<tr><td colspan="3">Retrieve the data of a specific factoid for a project.</td></tr>
</table>

<table>
<tr><td>Metric Raw  Data</td><td>GET</td> <td> /metricprovider/raw/projects/p/{projectId}/m/{metricId}</td></tr>
<tr><td colspan="3">Retrieve the raw data of a project’s metric provider. This is essentially a
JSON dump of the metric provider’s MongoDB collection.</td></tr>
</table>

## Workflow Execution Engine API

TODO

## Knowledge Base API

<table>
<tr><td>List of analyzed artifacts</td><td>GET</td> <td> /api/artifacts</td></tr>
<tr><td colspan="3">Retrieve a list of monitored artifacts.</td></tr>
</table>

<table>
<tr><td>List of similar artifacts</td><td>GET</td> <td>
/api/recommendation/similar/p/{id}/m/{sim_method}/n/{num}
</td></tr>
<tr><td colspan="3">This resource is used to retrieve projects that are similar to a given project.</td></tr>
</table>

## DevOps Dashboard API
