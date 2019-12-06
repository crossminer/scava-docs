# Readers

This document describes the readers used to provide data for the Scava platform.

- [Bug Trackers](#bug-trackers)
- [Communication Channels](#communication-channels)
- [Documentation](#documentation)

## [Bug Trackers](#bug-trackers)

The following readers retrieve data from bug tracking systems.

------

### org.eclipse.scava.platform.bugtrackingsystem.bitbucket

This reader retrieves data from Bitbucket through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ------- |
| URL | `String` |URL of the repository  | https://bitbucket.org/fenics-project/dolfin | Yes |
| Login |`String`  | Username used to log into Bitbucket | admin | Yes |
| Password |`String`       | Password used to log into Bitbucket | admin101 | Yes |

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.bugtrackingsystem.bugzilla

This reader retrieves data from Bugzilla through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ------- |
|  URL  | `String` | URL of the repository | https://bugzilla.redhat.com/xmlrpc.cgi | Yes |
| Product | `String` |An existing project in Bugzilla  |   Red Hat Enterprise Linux 8   |   Yes   |
| Component |`String`  | An existing component of the project | 389-ds-base | Yes |
| Project |`String` | The Project name | Bugzilla | Yes |

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.bugtrackingsystem.github

This reader retrieves data from GitHub through a REST API.  To register a project on the platform the user must use the `Import Project` option and provide the following parameter:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
| URL | `String` | URL of the repository | https://github.com/Adrian-Berrigan/adriantest |

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.bugtrackingsystem.gitlab

This reader retrieves data from GitLab through a REST API.  To register a project on the platform the user must use the `Import Project` option and provide the following parameter:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
| URL | `String` | URL of the repository | https://github.com/Adrian-Berrigan/adriantest |

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.bugtrackingsystem.jira

This reader retrieves data from Jira through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ------- |
|  URL  | `String` | URL of the repository | https://jira.xwiki.org | Yes |
| Login | `String` |Username used to log into Jira  |   admin   |   No   |
| Password |`String`  | Password used to log into Jira | admin101               | No |
| Project | `String`| Name of the project | XWIKI | Yes |

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.bugtrackingsystem.mantis

This reader retrieves data from Mantis through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
|  URL  | `String` | URL of the repository | https://www.mantisbt.org/ |
| Token | `String` |A unique token used to make authentication request  |   6aefdre554675bfgtrhgfy77567   |

<u>*Additional Information*</u> :

-	To retrieve issues with `CLOSED` status from Mantis, the user must ensure that the `$g_hide_status_default` filter parameter located in the config file `.../config/config_inc.php` is set to `META_FILTER_NONE`. It seems this parameter is set to `CLOSED` by default as discussed in [**this**](https://www.mantisbt.org/forums/viewtopic.php?f=3&t=20599&p=54037&hilit=issues+does+not+closed#p54037) forum post.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.bugtrackingsystem.redmine

This reader retrieves data from Redmine through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
|  URL  | `String` | URL of the repository | http://forge.modelio.org |
| Name | `String` |Name of the user  |   Dave   |
| Project | `String` | Name of the project | intocps |

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.bugtrackingsystem.sourceforge

This reader retrieves data from SOURCEFORGE through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameter:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
| URL | `String` | URL of the project repository | https://sourceforge.net/rest/p/vice-emu/bugs |

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
## [Communication Channels](#communication-channels)

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

[<img src="./arrow_drop_up.svg">Back to top](#top)

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

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.communicationchannel.mbox

The Mbox reader uses dumps to parse the data. To register a project on the platform the user must use the `Create Project` option and provide the following parameters:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ---------------------- |
| URL | `String` | The URL location of the archive | https://mail.gnome.org/archives/gtk-list/ | Yes |
| Name | `String` | Name of the Mbox | mboxes | No |
| Description |  `String`| Brief description of the Mbox | The mboxes archive contains | No |
| Compressed File Ext. |`String`  | File extension of the archive | tar.gzip | Yes |
| Username |`String` | Username (for protected archive) | admin | No |
| Password | `String`| Password (for protected archive) | admin101 | No |

<u>*Additional Information*</u> :

- The reader supports compressed tarballs (i.e., `.tar.gzip`, `.tgz`) and specific compressed gz files (`.txt.gz` and `.mbox.gz`).
	- If the format is `.tar.gzip`, `.tgz` or `.txt.gz` the platform supports month based files, following this file format name convention: `YYYY-Month.ext`, e.g. `2019-Janaury.txt.gz`.
	This is similar to the one used in https://mail.gnome.org/archives/gtk-list/
	- If the format is `.mbox.gz`, the platform supports one file containing all the emails from the mailing list. In this case the URL must contain the name of the mailing list, like in:
	https://download.eclipse.org/scava/datasets/eclipse_mls/mboxes/actf-dev . This follows the format used in https://download.eclipse.org/scava/datasets/eclipse_mls/eclipse_mls.html to store dumps of mboxes.
- The reader will manage intelligently the dumps and will store, as a temporal file, only one file. However, the current implementation have some particular characteristics and limitations:
	- If the format is month-year based, the platform will download the files when the month or year of the delta changes. Do not analyze a mailing list that has not generated yet a dump, as the platform is not aware of the date when the dumps are updated. For example, if we are in December 2019, do not ask for analyzing December 2019 until the dump has been made. Otherwise, the platform will create empty deltas and the analysis will not be accurate.
	- If the format is `.mbox.gz` which contains all the emails sent, the dump will update the files only if the platform need to analyze a delta that the dump does not cover. This is done by calculating when was the last update of the dump; the calculation is based on the fact that Eclipse Mailing lists are updated each Sunday at 2am. The platform will pause until Monday and then get a dump that covers the expected date.
- Currently, the reader does not support a user-defined time for updating dumps.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.communicationchannel.nntp

This reader retrieves data from NNTP through a REST API.  To register a project on the platform the user must use the `Create Project` option and provide the following parameter:

| Parameter              | Type     | Description | Example | Mandatory |
| ---------------------- | -------- | ----------- | ------- | ------- |
| URL | `String` | URL of the project repository | news.mozilla.org | Yes |
| NewsGroupName | `String` | The newsgroup name | mozilla.activity-stream | Yes |
| Username | `String` | Username used to log into the newsgroup channel | admin | No |
| Password | `String` | Password used to log into the newsgroup channel | admin101 | No |
| Port | `int` | The port number | 119 by default | Yes |
| Interval | `int` | The frequency of calls | 10000 by default | No |

<u>*Additional Information*</u> :

- The port number is mandatory and defaults to 119. However, the user has the option to change this value, if their port number is different from 119.
- The Interval is not mandatory but defaults to 10000. However, the user has the option to lower or increase this value.

[<img src="./arrow_drop_up.svg">Back to top](#top)

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

[<img src="./arrow_drop_up.svg">Back to top](#top)

## [Documentation](#documentation)

The following readers retrieve project documentation from relevant sources.

------
### org.eclipse.scava.platform.documentation.gitbased

This reader is Git-Based and thus retrieves data through a REST API.  To register a project on the platform the user must use the `Documentation Git-Based` option and provide the following parameter:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
| URL | `String` | URL of the repository | https://github.com/linhr/pongo-pongo/wiki |

<u>*Additional Information*</u> :

-	This reader cannot be used along with a Git project, because internally they use the same model and the `documentation.Git-Based` reader extends the Git project reader.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
### org.eclipse.scava.platform.documentation.systematic

This reader uses web crawler to retrieve data from websites.  To register a project on the platform the user must use the `Documentation Systematic` option and provide the relevant parameter:

| Parameter              | Type     | Description | Example |
| ---------------------- | -------- | ----------- | ------- |
| URL | `String` | URL of the repository | https://wiki.eclipse.org/Trace_Compass#User_Guides |
| ExecutionFrequency* | `int` | Crawling frequency defined in days, e.g., 1 represents a day  | 1 |
| UserName | `String` | The `username` used to log into the website | name@domain.com |
| Password | `String` | The `password` used to log into the website | p$%7876 |
| LoginURL | `String` | The URL of the login page | https://accounts.eclipse.org/user/login?destination=user/login%3Ftakemeback%3Dhttp%253A//www.eclipse.org/forums/index.php%253Ft%253Dlogin |
| UsernameFieldName | `String` | The name used to define the `username` field on the website | name |
| PasswordFieldName | `String` | The name used to define the `password` field on the website | pass |

<u>*Additional Information*</u> :

- *ExecutionFrequency. By default the value is zero, which means that the documentation will be retrieved only once at the beginning of the analysis. Furthermore, we recommend a execution frequency greater than 5 in order to prevent the crawler to be banned from accessing the data.*
-	For clarity, all examples used in the above table are derived from the Eclipse Foundation website. For example, the `username` field is defined as name.
-	The `Documentation Systematic` reader supports both password protected and un-protected sources. `URL` and `ExecutionFrequency` are mandatory for both sources. However, only the password protected sources require the additional paramenters.
-	Dates preceeding the current date are processed once because the reader does not keep track of the website evolution up to the current date.
-	The reader assumes that all textual information within the specified URL location are related to documentation.
-	The crawler is configured to comply with the Robots Exclusion protocol and thus follows the rules in the robots.txt file during crawling.
-   The crawler does not support websites that are based mostly on JavaScript, such as websites based on AngularJS. The reason behind is that the crawler cannot execute JavaScript.

[<img src="./arrow_drop_up.svg">Back to top](#top)
