# Readers

This document describes the readers used to provide data for the Scava platform.

## Bug Trackers

The following readers retrieve data from bug tracking systems.

------

### org.eclipse.scava.platform.bugtrackingsystem.bitbucket

This reader retrieves data from Bitbucket through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ------- |
| URL | `String` |URL of the repository  | https://bitbucket.org/fenics-project/dolfin | Yes |
| Login |`String`  | Username used to log into Bitbucket | admin | Yes |
| Password |`String`       | Password used to log into Bitbucket | admin101 | Yes |

------
### org.eclipse.scava.platform.bugtrackingsystem.bugzilla

This reader retrieves data from Bugzilla through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ------- |
|  URL  | `String` | URL of the repository | https://bugzilla.redhat.com/xmlrpc.cgi | Yes |
| Product | `String` |An existing project in Bugzilla  |   Red Hat Enterprise Linux 8   |   Yes   |
| Component |`String`  | An existing component of the project | 389-ds-base | Yes |
| Project |`String` | The Project name | Bugzilla | Yes |

------
### org.eclipse.scava.platform.bugtrackingsystem.github

This reader retrieves data from GitHub through a REST API.  To register a project on the platform the user must use the `Import Project` option and provide the following parameter:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
| URL | `String` | URL of the repository | https://github.com/Adrian-Berrigan/adriantest |

------
### org.eclipse.scava.platform.bugtrackingsystem.gitlab

This reader retrieves data from GitLab through a REST API.  To register a project on the platform the user must use the `Import Project` option and provide the following parameter:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
| URL | `String` | URL of the repository | https://github.com/Adrian-Berrigan/adriantest |

------
### org.eclipse.scava.platform.bugtrackingsystem.jira

This reader retrieves data from Jira through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ------- |
|  URL  | `String` | URL of the repository | https://jira.xwiki.org | Yes |
| Login | `String` |Username used to log into Jira  |   admin   |   No   |
| Password |`String`  | Password used to log into Jira | admin101               | No |
| Project | `String`| Name of the project | XWIKI | Yes |

------
### org.eclipse.scava.platform.bugtrackingsystem.mantis

This reader retrieves data from Mantis through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
|  URL  | `String` | URL of the repository | https://www.mantisbt.org/ |
| Token | `String` |A unique token used to make authentication request  |   6aefdre554675bfgtrhgfy77567   |

------
### org.eclipse.scava.platform.bugtrackingsystem.redmine

This reader retrieves data from Redmine through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
|  URL  | `String` | URL of the repository | http://forge.modelio.org |
| Name | `String` |Name of the user  |   Dave   |
| Project | `String` | Name of the project | intocps |

------
### org.eclipse.scava.platform.bugtrackingsystem.sourceforge

This reader retrieves data from SOURCEFORGE through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameter:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
| URL | `String` | URL of the project repository | https://sourceforge.net/rest/p/vice-emu/bugs |

------
## Communication Channels

The following readers retrieve data from communication channels.

------
### org.eclipse.scava.platform.communicationchannel.eclipseforums

This reader retrieves data from Eclipse Forums through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameter:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ---------------------- |
| Forum Id | `String` | The unique ID of the eclipse forum | 305 | Yes |
| Forum Name | `String` | Name of the forum | Andmore | Yes |
| Client Id |  `String`| Unique ID provided by eclipse for authenticated access | G12DrqtW86745tTre65476 | No |
| Client Secret |`String`  | Access token provided by eclipse for authenticated access | wp199NB564Frt5R43Ghy87 | No |

<u>*Additional Information*</u> :
-	The `Forum Id` can be found within the forum URL. For example, the `Andmore` forum URL is https://www.eclipse.org/forums/index.php/f/305/ and the `Forum Id` is `305` shown in the last directory of the path.
-	Eclipse enforces a rate limit of 1,000 requests per hour for both authenticated and anonymous requests. However, authenticated users may request to increase the call limit, subject to Eclipse approval.

------
### org.eclipse.scava.platform.communicationchannel.irc

The Irc reader supports data retrieval from log archive. To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ---------------------- |
| URL | `String` | The URL location of the archive | http://localhost/Downloads/ | Yes |
| Name | `String` | Name of the Irc | kubuntu | Yes |
| Description |  `String`| Brief description of the Irc | The kubuntu archive contains .... | Yes |
| Compressed File Ext. |`String`  | File extension of the archive | tar.gzip | Yes |
| Username |`String` | Username (for protected archive) | admin | No |
| Password | `String`| Password (for protected archive) | admin101 | No |

<u>*Additional Information*</u> :
- The reader currently supports "tarballs" (i.e., tar.gzip, tgz).
- Each archive must be stored in the following name format `IrcName-yyyymmdd.ext` , to specify the date of analysis (e.g., `kubuntu-20040306.tar`). The archive may contain one or more files stored in a folder, and each file represents interaction within a single chat room.

------
### org.eclipse.scava.platform.communicationchannel.mbox

The Mbox reader supports data retrieval from log archive. To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ---------------------- |
| URL | `String` | The URL location of the archive | http://localhost/Downloads/ | Yes |
| Name | `String` | Name of the Mbox | mboxes | Yes |
| Description |  `String`| Brief description of the Mbox | The mboxes archive contains .... | Yes |
| Compressed File Ext. |`String`  | File extension of the archive | tar.gzip | Yes |
| Username |`String` | Username (for protected archive) | admin | No |
| Password | `String`| Password (for protected archive) | admin101 | No |

<u>*Additional Information*</u> :

- The reader currently supports "tarballs" (i.e., tar.gzip, tgz).
- The storage location may contain one or more Mbox archive(s), each stored in the following name format `MboxName-yyyymmdd.ext` , to specify the date of analysis. Each Mbox archive must contain one or more email messages (of the same analysis date), stored in a folder. 

------
### org.eclipse.scava.platform.communicationchannel.nntp

This reader retrieves data from NNTP through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameter:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ------- |
| URL | `String` | URL of the project repository | news.mozilla.org | Yes |
| Name | `String` | The newsgroup name | mozilla.activity-stream | Yes |
| Username | `String` | Username used to log into the newsgroup channel | admin | No |
| Password | `String` | Password used to log into the newsgroup channel | admin101 | No |
| Port | `int` | The port number | 119 by default | Yes |
| Interval | `int` | The frequency of calls | 10000 by default | No |

<u>*Additional Information*</u> :

- The port number is mandatory and defaults to 119. However, the user has the option to change this value, if their port number is different from 119.
- The Interval is not mandatory but defaults to 10000. However, the user has the option to lower or increase this value.

------
### org.eclipse.scava.platform.communicationchannel.sympa

The Sympa reader supports data retrieval from log archive. To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ---------------------- |
| URL | `String` | The URL location of the archive | http://localhost/Downloads/ | Yes |
| Name | `String` | Name of the Sympa | sympa | Yes |
| Description |  `String`| Brief description of the Sympa | The sympa archive contains .... | Yes |
| Compressed File Ext. |`String`  | File extension of the archive | tar.gzip | Yes |
| Username |`String` | Username (for protected archive) | admin | No |
| Password | `String`| Password (for protected archive) | admin101 | No |

<u>*Additional Information*</u> :

- The reader currently supports "tarballs" (i.e., tar.gzip, tgz).
- The storage location may contain one or more Sympa archive(s), each stored in the following name format `SympaName-yyyymmdd.ext` , to specify the date of analysis. Each Sympa archive must contain one or more email messages (of the same analysis date), stored in a folder. 
