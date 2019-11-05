# Metrics Reference Guide

This guide describes the historic and transient metric providers, as well as factoids, provided by the Scava platform.

- [Historic Metric Providers](#historic-metric-providers) for:
	- [Bug Trackers](#historic-metric-providers-for-bug-trackers)
	- [Newsgroups and Forums](#historic-metric-providers-for-newsgroups-and-forums)
	- [Commits and Committers](#historic-metric-providers-for-commits-and-committers)
	- [Documentation](#historic-metric-providers-for-documentation)
	- [Generic Source Code](#historic-metric-providers-for-generic-source-code)
	- [Java Code](#historic-metric-providers-for-java-code)
	- [OSGi Dependencies](#historic-metric-providers-for-osgi-dependencies)
	- [Maven Dependencies](#historic-metric-providers-for-maven-dependencies)
        - [Docker Dependencies](#historic-metric-providers-for-docker-dependencies)
        - [Puppet Dependencies](#historic-metric-providers-for-puppet-dependencies)
	- [Docker Smells](#historic-metric-providers-for-docker-smells)
	- [Puppet Smells](#historic-metric-providers-for-puppet-smells)
- [Transient Metric Providers](#transient-metric-providers) for:
	- [Bug Trackers](#transient-metric-providers-for-bug-trackers)
	- [Newsgroups and forums](#transient-metric-providers-for-newsgroups-and-forums)
	- [Documentation](#transient-metric-providers-for-documentation)
	- [Natural Language Processing](#transient-metric-providers-for-natural-language-processing)
	- [Commits and Committers](#transient-metric-providers-for-commits-and-committers)
	- [Generic Source Code](#transient-metric-providers-for-generic-source-code)
	- [Java Code](#transient-metric-providers-for-java-code)
	- [OSGi Dependencies](#transient-metric-providers-for-osgi-dependencies)
	- [Maven Dependencies](#transient-metric-providers-for-maven-dependencies)
        - [Docker Dependencies](#transient-metric-providers-for-docker-dependencies)
        - [Puppet Dependencies](#transient-metric-providers-for-puppet-dependencies)
	- [Docker Smells](#transient-metric-providers-for-docker-smells)
	- [Puppet Smells](#transient-metric-providers-for-puppet-smells)
	- [Docker Antipatterns](#transient-metric-providers-for-docker-antipatterns)
	- [Puppet Antipatterns](#transient-metric-providers-for-puppet-antipatterns)
	- [Projects Relations](#transient-metric-providers-for-projects-relations)
	- [New Versions](#transient-metric-providers-for-new-versions)
	- [Indexing](#transient-metric-providers-for-indexing)
	- [API](#transient-metric-providers-for-api)
- [Factoids](#factoids) for:
	- [Bug Trackers](#factoids-for-bug-trackers)
	- [Newsgroups and Forums](#factoids-for-newsgroups-and-forums)
	- [Documentation](#factoids-for-documentation)

------

## [Historic Metric Providers](#historic-metric-providers)

Historic metrics maintain a record of various heuristics associated with a specific open source project over its lifetime. They typically depend on the results from one or more transient metrics and are typically displayed in the Scava dashboards.

### [Historic Metric Providers for Bug Trackers](#historic-metric-provider-for-bug-trackers)

The following Historic Metric Providers are associated with Issue trackers

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.bugs](#org.eclipse.scava.metricprovider.historic.bugs.bugs)
- **Short name**: historic.bugs.bugs
- **Friendly name**: Number of bugs per day per bug tracker

This metric computes the number of bugs per day for each bug tracker seperately. It also computes additional information such as average comments per bug, average comments per user, average requests and/or replies per user and bug.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.bugmetadata`,

	`org.eclipse.scava.metricprovider.trans.bugs.activeusers`

- <u>Returns</u> :	`BugsBugsHistoricMetric` which contains:

	| Variable							 | Type												|
	| ---------------------- | --------------------------- |
	| bugTrackers						| `List<DailyBugTrackerData>` |
	| numberOfBugs					 | `int`											 |
	| averageCommentsPerBug	| `float`										 |
	| averageRequestsPerBug	| `float`										 |
	| averageRepliesPerBug	 | `float`										 |
	| averageCommentsPerUser | `float`										 |
	| averageRequestsPerUser | `float`										 |
	| averageRepliesPerUser	| `float`										 |

<u>*Additional Information*</u> :

- DailyBugTrackerData :
	- `String`	bugTrackerId
	- `int`	numberOfBugs

<u>*Visualisation Output Information*</u> :

- BugsHistoricMetricProvider :
	- `id`	bugs.bugs
	- `id`	bugs.comments-bugaverage
	- `id`	bugs.comments-useraverage
	- `id`	bugs.requests-bugaverage
	- `id`	bugs.requests-useraverage
	- `id`	bugs.replies-bugaverage
	- `id`	bugs.replies-useraverage
	- `id`	bugs.requestsreplies-useraverage
	- `id`	bugs.requestsreplies-bugaverage

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.comments](#org.eclipse.scava.metricprovider.historic.bugs.comments)
- **Short name**: historic.bugs.comments
- **Friendly name**: Number of bug comments per day per bug tracker

This metric computes the number of bug comments submitted by the community (users) per day for each bug tracker.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.comments`

- <u>Returns</u> :	`BugsCommentsHistoricMetric` which contains:

	| Variable									 | Type								 |
	| -------------------------- | -------------------- |
	| Bugs											 | `List<DailyBugData>` |
	| numberOfComments					 | `int`			|
	| cumulativeNumberOfComments | `int`						|

<u>*Additional Information*</u> :

- DailyBugData :
	- `String`	bugTrackerID
	- `int`	numberOfComments
	- `int`	cumulativeNumberOfComments

<u>*Visualisation Output Information*</u> :

- CommentsHistoricMetricProvider :
	- `id`	bugs.comments
	- `id`	bugs.cumulativeComments

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.emotions](#org.eclipse.scava.metricprovider.historic.bugs.emotions)
- **Short name**: historic.bugs.emotions
- **Friendly name**: Number of emotions per day per bug tracker

This metric computes the emotional dimensions present in bug comments submitted by the community (users) per day for each bug tracker. Emotion can be 1 of 6 (anger, fear, joy, sadness, love or surprise).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.emotions`

- <u>Returns</u> :	`BugsEmotionsHistoricMetric` which contains:

	| Variable	 | Type							 |
	| ---------- | ------------------ |
	| bugData		| `List<BugData>`		|
	| Dimensions | `List<Dimensions>` |

<u>*Additional Information*</u> :

- BugData :
	 - `String`	bugTrackerID
	 - `int`	numberOfComments
	 - `int` 	cumulativeNumberOfComments

- Dimensions :
	- `String`	 bugTrackerId
	- `String` 	emotionLabel (`anger`, `fear`, `joy`, `sadness`, `love`, `surprise`)
	 - `int`	numberOfComments
	 - `int` 	cumulativeNumberOfComments
	 - `float`	percentage
	 - `float`	cumulativePercentage

<u>*Visualisation Output Information*</u> :

- EmotionsHistoricMetricProvider :
	- `id`	bugs.emotions.cumulativeComments
	- `id`	bugs.emotions.cumulativeCommentPercentages
	- `id`	bugs.emotions.comments
	- `id`	bugs.emotions.commentPercentages

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.migrationissues](#org.eclipse.scava.metricprovider.historic.bugs.migrationissues)
- **Short name**: historic.bugs.migrationissues
- **Friendly name**: Migration Issues Detection in Bug Trackers per day per bug tracker

This metric stores how many migration issues have been found per day for each bug tracker.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.migrationissues`

- <u>Returns</u> :	`BugTrackerMigrationIssueHistoricMetric` which contains:

	| Variable							 | Type								 |
	| ---------------------- | -------------------- |
	| dailyBugTrackerMigrationData					 | `List<DailyBugTrackerMigrationData>` |

<u>*Additional Information*</u> :

- DailyBugTrackerMigrationData :
	- `String`	bugTrackerId
	- `List<String>` bugsId;
	- `int`	numberOfBugs

<u>*Visualisation Output Information*</u> :

- BugTrackerMigrationIssueHistoricMetricProvider :
	- `id`	bugs.dailymigrationissues

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.migrationissuesmaracas](#org.eclipse.scava.metricprovider.historic.bugs.migrationissuesmaracas)
- **Short name**: historic.bugs.migrationissuesmaracas
- **Friendly name**: Migration Issues Detection along with Maracas in Bug Trackers per day per bug tracker

This metric stores how many migration issues have been found containing changes detected with *MARACAS* per day for each bug tracker.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.migrationissuesmaracas`

- <u>Returns</u> :	`BugTrackerMigrationIssueMaracasHistoricMetric` which contains:

	| Variable							 | Type								 |
	| ---------------------- | -------------------- |
	| dailyBugTrackerMigrationMaracasData					 | `List<DailyBugTrackerMigrationMaracasData>` |
	| bugTrackerMigrationMaracasData					 | `List<BugTrackerMigrationMaracasData>` |

<u>*Additional Information*</u> :

- DailyBugTrackerMigrationMaracasData :
	- `String`	bugTrackerId
	- `List<String>` bugsId;
	- `int`	numberOfIssues
- BugTrackerMigrationMaracasData :
	- `String`	bugTrackerId
	- `String` bugId;
	- `List<String>` changesAndMatchingPercentage

<u>*Visualisation Output Information*</u> :

- BugTrackerMigrationIssueMaracasHistoricMetricProvider :
	- `id`	bugs.dailymigrationissuesmaracas
	- `id`	bugs.migrationissuesmaracas.changes

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.newbugs](#org.eclipse.scava.metricprovider.historic.bugs.newbugs)
- **Short name**: historic.bugs.newbugs
- **Friendly name**: Number of new bugs per day per bug tracker

This metric computes the number of new bugs reported by the community (users) per day for each bug tracker. A small number of bug reports can indicate either a bug-free, robust project or a project with a small/inactive user community.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.newbugs`

- <u>Returns</u> :	`BugsNewBugsHistoricMetric` which contains:

	| Variable							 | Type								 |
	| ---------------------- | -------------------- |
	| dailyBugData					 | `List<DailyBugData>` |
	| numberOfBugs					 | `int`								|
	| cumulativeNumberOfBugs | `int`								|

<u>*Additional Information*</u> :

- DailyBugData :
	- `String`	bugTrackerId
	- `int`	numberOfBugs
	- `int` 	cumulativeNumberOfBugs

<u>*Visualisation Output Information*</u> :

- NewUsersHistoricMetricProvider :
	- `id`	bugs.cumulativeNewUsers
	- `id`	bugs.newUsers

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.newusers](#org.eclipse.scava.metricprovider.historic.bugs.newusers)
- **Short name**: historic.bugs.newusers
- **Friendly name**: Number of new users per day per bug tracker

This metric computes the number of new users per day  for each bug tracker seperately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.activeusers`

- <u>Returns</u> :	`BugsNewUsersHistoricMetric` which contains:

	| Variable									 | Type												|
	| -------------------------- | --------------------------- |
	| bugTrackers								| `List<DailyBugTrackerData>` |
	| numberOfNewUsers					 | `int`											 |
	| cumulativeNumberOfNewUsers | `int`	|

<u>*Additional Information*</u> :

- DailyBugTrackerData :
	- `String`	bugTrackerId
	- `int`	numberOfNewUsers
	- `int` 	cumulativeNumberOfNewUsers

<u>*Visualisation Output Information*</u> :

- NewUsersHistoricMetricProvider :
	- `id`	bugs.cumulativeNewUsers
	- `id`	bugs.newUsers

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.opentime](#org.eclipse.scava.metricprovider.historic.bugs.opentime)
- **Short name**: historic.bugs.opentime
- **Friendly name**: Average duration to close an open bug

This metric computes the average duration between creating and closing bugs. Format: dd:HH:mm:ss:SS, where dd=days, HH:hours, mm=minutes, ss:seconds, SS=milliseconds.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.bugmetadata`

- <u>Returns</u> :	`OpenTimeHistoricMetricProvider` which contains:

	| Variable									 | Type												|
	| -------------------------- | --------------------------- |
	| avgBugOpenTime	| `String` |
	| avgBugOpenTimeInDays	| `double`	|
	| bugsConsidered | `int`|

<u>*Visualisation Output Information*</u> :

- OpenTimeHistoricMetricProvider :
	- `id`	bugs.bugOpenTime
	- `id`	bugs.bugOpenTime-bugs

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.patches](#org.eclipse.scava.metricprovider.historic.bugs.patches)
- **Short name**: historic.bugs.patches
- **Friendly name**: Number of bug patches per day

This class computes the number of bug patches per day, for each bug tracker seperately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.patches`

- <u>Returns</u> :	`PatchesHistoricMetricProvider` which contains:

	| Variable		 | Type		|
	| -------------------------- | --------------------------- |
	| numberOfPatches	| `int` |
	| cumulativeNumberOfPatches	| `int`	|
	| bugs | `List<DailyBugData>`|


<u>*Additional Information*</u> :

- DailyBugData :
	- `String`	bugTrackerId
	- `int`	numberOfPatches
	- `int`	cumulativeNumberOfPatches

<u>*Visualisation Output Information*</u> :

- PatchesHistoricMetricProvider :
	- `id`	bugs.cumulativePatches
	- `id`	bugs.patches

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.requestsreplies](#org.eclipse.scava.metricprovider.historic.bugs.requestsreplies)
- **Short name**: historic.bugs.requestsreplies
- **Friendly name**: Number of request and replies in bug comments per bug tracker

This metric computes the number of requests and replies realting to comments posted to bugs by the community (users) per day  for each bug tracker seperately.

- <u>Depends-on</u> :`org.eclipse.scava.metricprovider.trans.bugs.bugmetadata`

- <u>Returns</u> :	`BugsRequestsRepliesHistoricMetric` which contains:

	| Variable									 | Type												|
	| -------------------------- | --------------------------- |
	| Bugs											 | `List<DailyBugTrackerData>` |
	| numberOfRequests					 | `int`											 |
	| numberOfReplies						| `int`											 |
	| cumulativeNumberOfRequests | `int`											 |
	| cumulativeNumberOfReplies	| `int`											 |

<u>*Additional Information*</u> :

- DailyBugTrackerData :
	- `String`	bugTrackerId
	- `int`	numberOfRequests
	- `int`	numberOfReplies
	- `int`	cumulativeNumberOfRequests
	- `int`	cumulativeNumberOfReplies

<u>*Visualisation Output Information*</u> :

- RequestsRepliesHistoricMetricProvider :
	- `id`	bugs.replies
	- `id`	bugs.cumulativereplies
	- `id`	bugs.requests
	- `id`	bugs.cumulativerequests
	- `id`	bugs.requestsreplies
	- `id`	bugs.cumulativerequestsreplies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.requestsreplies.average](#org.eclipse.scava.metricprovider.historic.bugs.requestsreplies.average)
- **Short name**: historic.bugs.requestsreplies.average
- **Friendly name**: Average number of requests and replies in bug comments per bug tracker

This metric computes the average number of bug comments considered as request and reply for each bug tracker per day.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.activeusers`

- <u>Returns</u> :	`BugsRequestsRepliesHistoricMetric` which contains:

	| Variable									 | Type												|
	| -------------------------- | --------------------------- |
	| bugs											 | `List<DailyBugTrackerData>` |
	| numberOfRequests					 | `int`											 |
	| numberOfReplies						| `int`											 |
	| cumulativeNumberOfRequests | `int`											 |
	| cumulativeNumberOfReplies	| `int`											 |

<u>*Additional Information*</u> :

- DailyBugTrackerData :
	- `String`	bugTrackerId
	- `int`	numberOfRequests
	- `int`	numberOfReplies
	- `int`	cumulativeNumberOfRequests
	- `int`	cumulativeNumberOfReplies

<u>*Visualisation Output Information*</u> :

- RequestsRepliesHistoricMetricProvider :
	- `id`	bugs.requests-averageperday
	- `id`	bugs.requestsreplies-averageperday
	- `id`	bugs.comments-averageperday
	- `id`	bugs.replies-averageperday

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.responsetime](#org.eclipse.scava.metricprovider.historic.bugs.responsetime)
- **Short name**: historic.bugs.responsetime
- **Friendly name**: Average response time to open bugs per bug tracker

This metric computes the average time in which the community (users) responds to open bugs per day for each bug tracker seperately. Format: dd:HH:mm:ss:SS, where dd=days, HH:hours, mm=minutes, ss:seconds, SS=milliseconds.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.requestsreplies`

- <u>Returns</u> :	`BugsResponseTimeHistoricMetric` which contains:

| Variable			| Type		|
| --------------------------------- | ------- |
| bugTrackerId 				 | `String`  |
| avgResponseTimeFormatted  | `String`  |
| cumulativeAvgResponseTimeFormatted		 | `String`  |
| avgResponseTime		 | `float`   |
| cumulativeAvgResponseTime 		 | `float`   |
| bugsConsidered		 | `int`  |
| cumulativeBugsConsidered 		 | `int`  |

<u>*Visualisation Output Information*</u> :

- ResponseTimeHistoricMetricProvider :
	- `id`	bugs.averageResponseTime
	- `id`	bugs.cumulativeAverageResponseTime
	- `id`	bugs.cumulativeAverageResponseTime-bugs
	- `id`	bugs.averageResponseTime-bugs

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.sentiment](#org.eclipse.scava.metricprovider.historic.bugs.sentiment)
- **Short name**: historic.bugs.sentiment
- **Friendly name**: Overall sentiment per bug tracker

This metric computes the overall sentiment per bug tracker up to the processing date. The overall sentiment score could be -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment). In the computation, the sentiment score for each bug contributes equally, regardless of it's size.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.bugmetadata`

- <u>Returns</u> :	`BugsSentimentHistoricMetric` which contains:

	| Variable			| Type		|
	| --------------------------------- | ------- |
	| overallAverageSentiment					 | `float` |
	| overallSentimentAtThreadBeggining | `float` |
	| overallSentimentAtThreadEnd			 | `float` |

<u>*Visualisation Output Information*</u> :

- SentimentHistoricMetricProvider :
	- `id`	bugs.averageSentiment
	- `id`	bugs.sentimentAtThreadEnd
	- `id`	bugs.sentimentAtThreadBeggining
	- `id`	bugs.sentiment

- The sentiment related variables above all represent a <u>***Polarity***</u> value. A polarity value closer to: <u>-1</u> indicates negative sentiment, closer to <u>0</u> indicates neutral sentiment and closer to <u>1</u> indicates positive sentiment.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.severity](#org.eclipse.scava.metricprovider.historic.bugs.severity)
- **Short name**: historic.bugs.severity
- **Friendly name**: Number of bugs per severity level per bug tracker

This metric computes the number of severity levels for bugs submitted by the community (users) every day for each bug tracker. Specifically, it calculates the number and percentage of bugs that have been categorised into 1 of 8 severity levels (blocker, critical, major, minor, enhancement, normal, trivial, unknown). A bug severity is considered `unknown` if there is not enough information for the classifier to make a decision. For example, an unanswered bug with no user comment to analyse. 	

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.severityclassification`

- <u>Returns</u> :	`BugsSeveritiesHistoricMetric` which contains:

	| Variable			 | Type									 |
	| -------------- | ---------------------- |
	| bugData				| `List<BugData>`				|
	| severityLevels | `List<ServerityLevel>` |

<u>*Additional Information*</u> :

- BugData :
	- `String`	bugTrackerId
	- `int`	numberOfBugs
- SeverityLevel :
	- `String`	bugTrackerId
	- `String`	severityLevel	(`blocker`,`critical`,`major`,`minor`,`enhancement`, `normal`, `trivial`, `unknown`)
	- `int`	numberOfBugs
	- `int`	percentage

<u>*Visualisation Output Information*</u> :

- SeverityHistoricMetricProvider :
	- `id`	bugs.severity
	- `id`	bugs.severity.percentages

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.severitybugstatus](#org.eclipse.scava.metricprovider.historic.bugs.severitybugstatus)
- **Short name**: historic.bugs.severitybugstatus
- **Friendly name**: Number of each bug status per bug severity level

This metric computes the total number and percentage of each bug status per severity level, in bugs submitted every day, per bug tracker. There are 7 bug status (ResolvedClosed, WontFix, WorksForMe, NonResolvedClosed, Invalid, Fixed, Duplicate) and 8 severity  levels (blocker, critical, major, minor, enhancement, normal, trivial, unknown). A bug severity is considered `unknown` if there is not enough information for the classifier to make a decision. For example, an unanswered bug with no user comment to analyse.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.severityclassification`, `org.eclipse.scava.metricprovider.trans.bugs.bugmetadata`

- <u>Returns</u> :	`BugsSeverityBugStatusHistoricMetric` which contains:

	| Variable			 | Type									|
	| -------------- | --------------------- |
	| severityLevels | `List<SeverityLevel>` |

<u>*Additional Information*</u> :

- SeverityLevel :
	- `String`	severityLevel	(`blocker`,`critical`,`major`,`minor`,`enhancement`, `normal`, `trivial`, `unknown`)
	- `int`	numberOfBugs
	- `int`	numberOfWontFixBugs
	- `int`	numberOfWorksForMeBugs
	- `int`	numberOfNonResolvedClosedBugs
	- `int`	numberOfInvalidBugs
	- `int`	numberOfFixedBugs
	- `int`	numberOfDuplicateBugs
	- `float`	percentageOfResolvedClosedBugs
	- `float`	percentageOfWontFixBugs
	- `float`	percentageOfWorksForMeBugs
	- `float`	percentageOfNonResolvedClosedBugs
	- `float`	percentageOfInvalidBugs
	- `float`	percentageOfFixedBugs
	- `float`	percentageOfDuplicateBugs

<u>*Visualisation Output*</u> :

- SeverityBugStatusHistoricMetricProvider :
	- `id`	bugs.severity.duplicateBugs
	- `id`	bugs.severity.duplicateBugs.percentages
	- `id`	bugs.severity.fixedBugs
	- `id`	bugs.severity.fixedBugs.percentages
	- `id`	bugs.severity.invalidBugs
	- `id`	bugs.severity.invalidBugs.percentages
	- `id`	bugs.severity.nonResolvedClosedBugs
	- `id`	bugs.severity.nonResolvedClosedBugs.percentages
	- `id`	bugs.severity.resolvedClosedBugs
	- `id`	bugs.severity.resolvedClosedBugs.percentages
	- `id`	bugs.severity.wontFixBugs
	- `id`	bugs.severity.wontFixBugs.percentages
	- `id`	bugs.severity.worksForMeBugs
	- `id`	bugs.severity.worksForMeBugs.percentages

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.severityresponsetime](#org.eclipse.scava.metricprovider.historic.bugs.severityresponsetime)
- **Short name**: historic.bugs.severityresponsetime
- **Friendly name**: Average response time to bugs per severity level per day

This metric computes the average time in which the community (users) responds to open bugs per severity level per day for each bug tracker. Format: dd:HH:mm:ss:SS, where dd=days, HH:hours, mm=minutes, ss:seconds, SS=milliseconds. Note: there are 8 severity  levels (blocker, critical, major, minor, enhancement, normal, trivial, unknown). A bug severity is considered `unknown` if there is not enough information for the classifier to make a decision. For example, an unanswered bug with no user comment to analyse.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.severityclassification`, `org.eclipse.scava.metricprovider.trans.bugs.requestsreplies`

- <u>Returns</u> :	`BugsSeverityBugStatusHistoricMetric` which contains:

	| Variable			 | Type									|
	| -------------- | --------------------- |
	| severityLevels | `List<SeverityLevel>` |

<u>*Additional Information*</u> :

- SeverityLevel :
	- `String`	severityLevel	(`blocker`,`critical`,`major`,`minor`,`enhancement`, `normal`, `trivial`, `unknown`)
	- `String`	avgResponseTimeFormatted
	- `int`	numberOfBugs
	- `long`	avgResponseTime

<u>*Visualisation Output Information*</u> :

- SeverityResponseTimeHistoricMetricProvider :
	- `id`	bugs.severity.averageResponseTime

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.severitysentiment](#org.eclipse.scava.metricprovider.historic.bugs.severitysentiment)
- **Short name**: historic.bugs.severitysentiment
- **Friendly name**: Average sentiment per bugs severity level per day

This metric computes for each bug severity level, the average sentiment, sentiment at the begining and end of bug comments posted by the community (users) every day for each bug tracker. Sentiment score could be closer to -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment). There are 8 severity levels (blocker, critical, major, minor, enhancement, normal, trivial, unknown). A bug severity is considered `unknown` if there is not enough information for the classifier to make a decision. For example, an unanswered bug with no user comment to analyse.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.severityclassification`, `org.eclipse.scava.metricprovider.trans.bugs.bugmetadata`

- <u>Returns</u> :	`BugsSeverityBugStatusHistoricMetric` which contains:

	| Variable			 | Type									|
	| -------------- | --------------------- |
	| severityLevels | `List<SeverityLevel>` |

<u>*Additional Information*</u> :

- SeverityLevel :
	- `String`	severityLevel	(`blocker`,`critical`,`major`,`minor`,`enhancement`, `normal`, `trivial`, `unknown`)
	- `int`	numberOfBugs
	- `float`	averageSentiment
	- `float`	sentimentAtThreadBeggining
	- `float`	sentimentAtThreadEnd

<u>*Visualisation Output Information*</u> :

- SeveritySentimentHistoricMetricProvider :
	- `id`	bugs.severity.sentiment
	- `id`	bugs.severity.averageSentiment
	- `id`	bugs.severity.sentimentAtThreadBeggining
	- `id`	bugs.severity.sentimentAtThreadEnd

- The sentiment related variables above all represent a <u>***Polarity***</u> value. A polarity value closer to: <u>-1</u> indicates negative sentiment, closer to <u>0</u> indicates neutral sentiment and closer to <u>1</u> indicates positive sentiment.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.status](#org.eclipse.scava.metricprovider.historic.bugs.status)
- **Short name**: historic.bugs.status
- **Friendly name**: Number of bugs per bug status per day

This metric computes the total number of bugs that corresponds to each bug status, in bugs submitted every day, per bug tracker. There are 7 bug status (ResolvedClosed, WontFix, WorksForMe, NonResolvedClosed, Invalid, Fixed, Duplicate).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.bugmetadata`

- <u>Returns</u> :	`BugsStatusHistoricMetric` which contains:

	| Variable											| Type	 |
	| ----------------------------- | ------ |
	| numberOfBugs									| `long` |
	| numberOfResolvedClosedBugs		| `int`	|
	| numberOfWontFixBugs					 | `int`	|
	| numberOfWorksForMeBugs				| `int`	|
	| numberOfNonResolvedClosedBugs | `int`	|
	| numberOfInvalidBugs					 | `int`	|
	| numberOfFixedBugs						 | `int`	|
	| numberOfDuplicateBugs				 | `int`	|

<u>*Visualisation Output Information*</u> :

- StatusHistoricMetricProvider :
	- `id`	bugs.duplicateBugs
	- `id`	bugs.fixedBugs
	- `id`	bugs.invalidBugs
	- `id`	bugs.nonResolvedClosedBugs
	- `id`	bugs.wontFixBugs
	- `id`	bugs.worksForMeBugs
	- `id`	bugs.resolvedClosedBugs

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.topics](#org.eclipse.scava.metricprovider.historic.bugs.status)
- **Short name**: historic.bugs.topics
- **Friendly name**: Labels of topic clusters in bug comments per bug tracker

This metric computes the labels of topic clusters extracted from bug comments submitted by the community (users), per bug tracker.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.topics`

- <u>Returns</u> :	`BugsTopicsHistoricMetric` which contains:

	| Variable	| Type						 |
	| --------- | ---------------- |
	| bugTopics | `List<BugTopic>` |

<u>*Additional Information*</u> :

- SeverityLevel :
	- `String`	bugTrackerId
	- `List<String>`	labels
	- `float`	numberOfDocuments
	- `List<String>` commentsId

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.unansweredbugs](#org.eclipse.scava.metricprovider.historic.bugs.unansweredbugs)
- **Short name**: historic.bugs.unansweredbugs
- **Friendly name**: Number of unanswered bugs per day

This metric computes the number of unanswered bugs per day.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.requestsreplies`

- <u>Returns</u> :	`BugsUnansweredBugsHistoricMetric` which contains:

	| Variable							 | Type	|
	| ---------------------- | ----- |
	| numberOfUnansweredBugs | `int` |

<u>*Visualisation Output Information*</u> :

- UnansweredThreadsHistoricMetricProvider :
	- `id`	bugs.unansweredBugs

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.bugs.users](#org.eclipse.scava.metricprovider.historic.bugs.users)
- **Short name**: historic.bugs.users
- **Friendly name**: Number of users, active and inactive per day per bug tracker

This metric computes the number of users, number of active and inactive users per day for each bug tracker separately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.activeusers`

- <u>Returns</u> :	`BugsUsersHistoricMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| bugTrackers					 | `List<DailyBugTrackingData>` |
	| numberOfUsers				 | `int`												|
	| numberOfActiveUsers	 | `int`												|
	| numberOfInactiveUsers | `int`												|

<u>*Additional Information*</u> :

- DailyBugTrackingData :
	- `String`	bugTrackerId
	- `int`	numberOfUsers
	- `int`	numberOfActiveUsers
	- `int`	numberOfInactiveUsers

<u>*Visualisation Output Information*</u> :

- UsersHistoricMetricProvider :
	- `id`	bugs.users
	- `id`	bugs.activeusers
	- `id`	bugs.inactiveusers

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Historic Metric Providers for Newsgroups and Forums](#historic-metric-provider-for-newsgroups-and-forums)

The following Historic Metric Providers are associated with newsgroups.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.articles](#org.eclipse.scava.metricprovider.historic.newsgroups.articles)
- **Short name**: historic.newsgroups.articles
- **Friendly name**: Number of articles per day per news group

This metric computes the number of articles submitted by the community (users) per day for each newsgroup separately

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.articles`

- <u>Returns</u> :	`NewsgroupsArticlesHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| dailyNewsgroupData		 | `List<DailyNewsgroupData>` |

<u>*Additional Information*</u> :

- DailyNewsgroupData :
	- `String`	newsgroupName
	- `int`	numberOfArticles
	- `int`	cummulativeNumberOfArticles

<u>*Visualisation Output Information*</u> :

- ArticlesHistoricMetricProvider :
	- `id`	newsgroups.articles
	- `id`	newsgroups.cumulativeArticles

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.emotions](#org.eclipse.scava.metricprovider.historic.newsgroups.emotions)
- **Short name**: historic.newsgroups.emotions
- **Friendly name**: Number of emotions per day per newsgroup

This metric computes the emotional dimensions present in newsgroup comments submitted by the community (users) per day for each newsgroup. Emotion can be 1 of 6 (anger, fear, joy, sadness, love or surprise).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.emotions `

- <u>Returns</u> :	`NewsgroupsEmotionsHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| newsgroupsData		 | `List<Newsgroups>` |
	| emotionDimension		 | `List<Emotion>` |

<u>*Additional Information*</u> :

- NewsgroupsData :
	- `String`	newsgroupName
	- `int`	numberOfArticles
	- `int`	cummulativeNumberOfArticles

- EmotionDimension :
	- `String`	newsgroupName
	- `String`	emotionLabel (`anger`, `fear`, `joy`, `sadness`, `love`, `surprise`)
	- `int`	numberOfArticles
	- `int`	cumulativeNumberOfArticles
	- `float`	percentage
	- `float`	cumulativePercentage

<u>*Visualisation Output Information*</u> :

- EmotionsHistoricMetricProvider :
	- `id`	newsgroups.emotions.articlePercentages
	- `id`	newsgroups.emotions.cumulativeArticles
	- `id`	newsgroups.emotions.cumulativeArticlePercentages
	- `id`	newsgroups.emotions.articles

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.migrationissues](#org.eclipse.scava.metricprovider.historic.newsgroups.migrationissues)
- **Short name**: historic.newsgroups.migrationissues
- **Friendly name**: Migration Issues Detection in articles per day per newsgroup

This metric detects migration issues in articles per day for each newgroup.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.migrationissues`

- <u>Returns</u> :	`NewsgroupsMigrationIssueHistoricMetric` which contains:

	| Variable							 | Type								 |
	| ---------------------- | -------------------- |
	| dailyNewsgroupsMigrationData					 | `List<DailyNewsgroupsMigrationData>` |

<u>*Additional Information*</u> :

- DailyBugTrackerMigrationData :
	- `String`	newsgroupName
	- `List<Integer>` threadsId
	- `int`	numberOfIssues

<u>*Visualisation Output Information*</u> :

- NewsgroupsMigrationIssueHistoricMetricProvider :
	- `id`	newsgroups.dailymigrationissues

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.migrationissuesmaracas](#org.eclipse.scava.metricprovider.historic.newsgroups.migrationissuesmaracas)
- **Short name**: historic.newsgroups.migrationissuesmaracas
- **Friendly name**: Migration Issues Detection along with Maracas in articles per day per newsgroup

This metric stores how many migration issues have been found containing changes detected with *MARACAS* per day for each newsgroup.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.migrationissuesmaracas`

- <u>Returns</u> :	`NewsgroupMigrationIssueMaracasHistoricMetric` which contains:

	| Variable							 | Type								 |
	| ---------------------- | -------------------- |
	| dailyNewsgroupMigrationMaracasData					 | `List<DailyNewsgroupMigrationMaracasData>` |
	| newsgroupMigrationMaracasData					 | `List<NewsgroupMigrationMaracasData>` |

<u>*Additional Information*</u> :

- DailyNewsgroupMigrationMaracasData :
	- `String`	newsgroupName
	- `List<Integer>` threadsId;
	- `int`	numberOfIssues
- NewsgroupMigrationMaracasData :
	- `String`	newsgroupName
	- int threadId;
	- `List<String>` changesAndMatchingPercentage

<u>*Visualisation Output Information*</u> :

- NewsgroupMigrationIssueMaracasHistoricMetricProvider :
	- `id`	newsgroups.dailymigrationissuesmaracas
	- `id`	newsgroups.migrationissuesmaracas.changes

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.newthreads](#org.eclipse.scava.metricprovider.historic.newsgroups.newthreads)
- **Short name**: historic.newsgroups.newthreads
- **Friendly name**: Number of new threads per day per newsgroup

This metric computes the number of new threads submitted by the community (users) per day for each newsgroup separately

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.threads`

- <u>Returns</u> :	`NewsgroupsNewThreadsHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| dailyNewsgroupData		 | `List<DailyNewsgroupData>` |

<u>*Additional Information*</u> :

- DailyNewsgroupData :
	- `String`	newsgroupName
	- `int`	numberOfNewThreads
	- `int`	cummulativeNumberOfNewThreads

<u>*Visualisation Output Information*</u> :

- NewThreadsHistoricMetricProvider :
	- `id`	newsgroups.newThreads
	- `id`	newsgroups.cumulativeNewThreads

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.newusers](#org.eclipse.scava.metricprovider.historic.newsgroups.newusers)
- **Short name**: historic.newsgroups.newusers
- **Friendly name**: Number of new users per day per newsgroup

This metric computes the number of new users per day for each newsgroup seperately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.activeusers`

- <u>Returns</u> :	`NewsgroupsNewUsersHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| dailyNewsgroupData		 | `List<DailyNewsgroupData>` |

<u>*Additional Information*</u> :

- DailyNewsgroupData :
	- `String`	newsgroupName
	- `int`	numberOfNewUsers
	- `int`	cummulativeNumberOfNewUsers

<u>*Visualisation Output Information*</u> :

- NewUsersHistoricMetricProvider:
	- `id`	newsgroups.cumulativeNewUsers
	- `id`	newsgroups.newUsers

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.requestsreplies](#org.eclipse.scava.metricprovider.historic.newsgroups.requestsreplies)
- **Short name**: historic.newsgroups.requestsreplies
- **Friendly name**: Number of requests and replies in articles per day

This metric computes the number of requests and replies in newsgroup articles submitted by the community (users) per day for each newsgroup separately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.requestreplyclassification`

- <u>Returns</u> :	`NewsgroupsRequestsRepliesHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| dailyNewsgroupData		 | `List<DailyNewsgroupData>` |

<u>*Additional Information*</u> :

- DailyNewsgroupData :
	- `String`	newsgroupName
	- `int`	numberOfRequests
	- `int`	numberOfReplies
	- `int`	cumulativeNumberOfRequests
	- `int`	cumulativeNumberOfReplies

<u>*Visualisation Output Information*</u> :

- RequestsRepliesHistoricMetricProvider :
	- `id`	newsgroups.requests
	- `id`	newsgroups.cumulativerequests
	- `id`	newsgroups.replies
	- `id`	newsgroups.cumulativereplies
	- `id`	newsgroups.requestsreplies
	- `id`	newsgroups.cumulativerequestsreplies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.requestsreplies.average](#org.eclipse.scava.metricprovider.historic.newsgroups.requestsreplies.average)
- **Short name**: historic.newsgroups.requestsreplies.average
- **Friendly name**: Average number of articles, requests and replies per day

This metric computes the average number of newsgroup articles, including the number of requests and replies within the newsgroup articles per day.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.activeusers`

- <u>Returns</u> :	`NewsgroupsRequestsRepliesAverageHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| averageArticlesPerDay		 | `float` |
	| averageRequestsPerDay		 | `float` |
	| averageRepliesPerDay		 | `float` |

<u>*Visualisation Output Information*</u> :

- RequestsRepliesAverageHistoricMetricProvider :
	- `id`	newsgroups.requestsreplies-averageperday
	- `id`	newsgroups.requests-averageperday
	- `id`	newsgroups.replies-averageperday
	- `id`	newsgroups.comments-averageperday

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.responsetime](#org.eclipse.scava.metricprovider.historic.newsgroups.responsetime)
- **Short name**: historic.newsgroups.responsetime
- **Friendly name**: Average response time to threads per day per newsgroup

This metric computes the average time in which the community responds to open threads per day for each newsgroup separately. Format: dd:HH:mm:ss:SS, where dd=days, HH:hours, mm=minutes, ss:seconds, SS=milliseconds.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.threadsrequestsreplies`

- <u>Returns</u> :	`NewsgroupsResponseTimeHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| newsgroupName		 | `String` |
	| avgResponseTime		 | `long` |
	| avgResponseTimeFormatted		 | `String` |
	| threadsConsidered		 | `int` |
	| cumulativeAvgResponseTimeFormatted		 | `String` |
	| cumulativeThreadsConsidered		 | `int` |

<u>*Visualisation Output Information*</u> :

- ResponseTimeHistoricMetricProvider :
	- `id`	newsgroups.averageResponseTime
	- `id`	newsgroups.cumulativeAverageResponseTime
	- `id`	newsgroups.cumulativeAverageResponseTime-threads
	- `id`	newsgroups.averageResponseTime-threads
	-
[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.sentiment](#org.eclipse.scava.metricprovider.historic.newsgroups.sentiment)
- **Short name**: historic.newsgroups.sentiment
- **Friendly name**: Overall sentiment of newsgroup articles

This metric computes the overall sentiment per newsgroup repository up to the processing date. The overall sentiment score could be -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment). In the computation, the sentiment score of each thread contributes equally, irrespective of its size.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.sentiment`

- <u>Returns</u> :	`NewsgroupsSentimentHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| overallAverageSentiment		 | `float` |
	| overallSentimentAtThreadBegining		 | `float` |
	| overallSentimentAtThreadEnd		 | `float` |

<u>*Visualisation Output Information*</u> :

- SentimentHistoricMetricProvider :
	- `id`	newsgroups.averageSentiment
	- `id`	newsgroups.sentimentAtThreadEnd
	- `id`	newsgroups.sentimentAtThreadBeggining
	- `id`	newsgroups.sentiment

- The sentiment related variables above all represent a <u>***Polarity***</u> value. A polarity value closer to: <u>-1</u> indicates negative sentiment, closer to <u>0</u> indicates neutral sentiment and closer to <u>1</u> indicates positive sentiment.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.severity](#org.eclipse.scava.metricprovider.historic.newsgroups.severity)
- **Short name**: historic.newsgroups.severity
- **Friendly name**: Number of each severity level in newsgroup threads per day

This metric computes the number of each severity levels in threads submitted every day, per newsgroup. There are 7 severity  levels (blocker, critical, major, minor, enhancement,  normal, trivial).  

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.severityclassification `

- <u>Returns</u> :	`NewsgroupsSeveritiesHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| newsgroupData		 | `List<Newsgroups>` |
	| severityLevel		 | `List<SeverityLevel>` |

<u>*Additional Information*</u> :

- NewsgroupData :
	- `String`	newsgroupName
	- `int`	numberThreads

- SeverityLevel :
	- `String`	newsgroupName
	- `String`	severityLabel (`blocker`, `critical`, `major`, `minor`, `enhancement`,  `normal`, `trivial`)
	- `int`	numberOfThreads
	- `float`	percentage

<u>*Visualisation Output Information*</u> :

- SeverityHistoricMetricProvider :
	- `id`	newsgroups.severity
	- `id`	newsgroups.severity.percentages

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.severityresponsetime](#org.eclipse.scava.metricprovider.historic.newsgroups.severityresponsetime)
- **Short name**: historic.newsgroups.severityresponsetime
- **Friendly name**: Average response time to threads per severity level per day

This metric computes the average time in which the community (users) responds to open threads per severity level per day for each bug tracker. Format: dd:HH:mm:ss:SS, where dd=days, HH:hours, mm=minutes, ss:seconds, SS=milliseconds. Note: there are 7 severity  levels (blocker, critical, major, minor, enhancement, normal, trivial).

Average response time to threads per severity level

This metric computes the average response time for newsgroup threads submitted every day, based on their severity levels.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.severityclassification`,
`org.eclipse.scava.metricprovider.trans.newsgroups.threadsrequestsreplies`

- <u>Returns</u> :	`NewsgroupsSeverityResponseTimeHistoricMetric ` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| severityLevel		 | `List<SeverityLevel>` |

<u>*Additional Information*</u> :

- SeverityLevel :
	- `String`	severityLabel (`blocker`, `critical`, `major`, `minor`, `enhancement`,  `normal`, `trivial`)
	- `int`	numberOfThreads
	- `long`	avgResponseTime
	- `String`	avgResponseTimeFormatted

<u>*Visualisation Output Information*</u> :

- SeverityResponseTimeHistoricMetricProvider :
	- `id`	newsgroups.severity.averageResponseTime

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.severitysentiment](#org.eclipse.scava.metricprovider.historic.newsgroups.severitysentiment)
- **Short name**: historic.newsgroups.severitysentiment
- **Friendly name**: Average sentiment in threads per severity level per day

This metric computes the average sentiment, the sentiment at the beginning of threads and the sentiment at the end of threads; for each severity level in newsgroup threads submitted every day. Sentiment can be -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment). Note: there are 7 severity  levels (blocker, critical, major, minor, enhancement, normal, trivial).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.severityclassification`,
`org.eclipse.scava.metricprovider.trans.newsgroups.sentiment`

- <u>Returns</u> :	`NewsgroupsSeveritySentimentHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| severityLevel		 | `List<SeverityLevel>` |

<u>*Additional Information*</u> :

- SeverityLevel :
	- `String`	severityLabel (`blocker`, `critical`, `major`, `minor`, `enhancement`,  `normal`, `trivial`)
	- `int`	numberOfThreads
	- `float`	avgSentiment
	- `float`	avgSentimentThreadBeginning
	- `float`	avgSentimentThreadEnd

<u>*Visualisation Output Information*</u> :

- SeveritySentimentHistoricMetricProvider :
	- `id`	newsgroups.severity.averageSentiment
	- `id`	newsgroups.severity.sentiment
	- `id`	newsgroups.severity.sentimentAtThreadEnd
	- `id`	newsgroups.severity.sentimentAtThreadBeggining

- The sentiment related variables above all represent a <u>***Polarity***</u> value. A polarity value closer to: <u>-1</u> indicates negative sentiment, closer to <u>0</u> indicates neutral sentiment and closer to <u>1</u> indicates positive sentiment.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.threads](#org.eclipse.scava.metricprovider.historic.newsgroups.threads)
- **Short name**: historic.newsgroups.threads
- **Friendly name**: Number of threads per day per newsgroup

This metric computes the number of threads per day for each newsgroup separately. The metric also computes average values for articles per thread, requests per thread, replies per thread, articles per user, requests per user and replies per user.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.threads`,
`org.eclipse.scava.metricprovider.trans.newsgroups.activeusers`

- <u>Returns</u> :	`NewsgroupsThreadsHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| dailyNewsgroupData		 | `List<DailyNewsgroupData>` |

<u>*Additional Information*</u> :

- DailyNewsgroupData :
	- `String`	newsgroupName
	- `int`	numberOfThreads
	- `float`	averageArticlesPerThread
	- `float`	averageRequestsPerThread
	- `float`	averageRepliesPerThread
	- `float`	averageArticlesPerUser
	- `float`	averageRequestsPerUser
	- `float`	averageRepliesPerUser

<u>*Visualisation Output Information*</u> :

- ThreadsHistoricMetricProvider :
	- `id`	newsgroups.threads
	- `id`	newsgroups.articles-threadaverage
	- `id`	newsgroups.articles-useraverage
	- `id`	newsgroups.requests-threadaverage
	- `id`	newsgroups.requests-useraverage
	- `id`	newsgroups.replies-threadaverage
	- `id`	newsgroups.replies-useraverage
	- `id`	newsgroups.requestsreplies-threadaverage
	- `id`	newsgroups.requestsreplies-useraverage

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.topics](#org.eclipse.scava.metricprovider.historic.newsgroups.topics)
- **Short name**: historic.newsgroups.topics
- **Friendly name**: Labels of newsgroup topics per newsgroup

This metric computes the labels of topics clusters in articles submitted by the community (users), for each newsgroup seperately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.topics`

- <u>Returns</u> :	`NewsgroupTopicsHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| newsgroupTopic		 | `List<NewsgrpTopic>` |

<u>*Additional Information*</u> :

- NewsgroupTopic :
	- `String`	newsgroupName
	- `List<String>`	labels
	- `int`	numberOfDocuments
	- `List<Integer>` articlesId

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.unansweredthreads](#org.eclipse.scava.metricprovider.historic.newsgroups.unansweredthreads)
- **Short name**: historic.newsgroups.unansweredthreads
- **Friendly name**: Number of unanswered threads per day per newsgroup

This metric computes the number of unanswered threads per day for each newsgroup separately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.threadsrequestsreplies`

- <u>Returns</u> :	`NewsgroupsUnansweredThreadsHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| dailyNewsgroupData		 | `List<DailyNewsgroupData>` |

<u>*Additional Information*</u> :

- DailyNewsgroupData :
	- `String`	newsgroupName
	- `int`	numberOfUnansweredThreads

<u>*Visualisation Output Information*</u> :

- UnansweredThreadsHistoricMetricProvider :
	- `id`	newsgroups.unansweredThreads

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.newsgroups.users](#org.eclipse.scava.metricprovider.historic.newsgroups.users)
- **Short name**: historic.newsgroups.users
- **Friendly name**: Number of users, active and inactive per day per newsgroup

This metric computes the number of users, including active and inactive users per day for each newsgroup separately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.activeusers`

- <u>Returns</u> :	`NewsgroupsUsersHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| dailyNewsgroupData		 | `List<DailyNewsgroupData>` |

<u>*Additional Information*</u> :

- DailyNewsgroupData :
	- `String`	newsgroupName
	- `int`	numberOfUsers
	- `int`	numberOfActiveUsers
	- `int`	numberOfInactiveUsers

<u>*Visualisation Output Information*</u> :

- UsersHistoricMetricProvider :
	- `id`	newsgroups.users
	- `id`	newsgroups.activeusers
	- `id`	newsgroups.inactiveusers
	- `id`	newsgroups.activeinactiveusers

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Historic Metric Providers for Commits and Committers](#historic-metric-providers-for-commits-and-committers)

The following Historic Metric Providers are related to the commits and committers of a project.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.committersoverfile.historic](#trans.rascal.activecommitters.committersoverfile.historic)
- **Short name**: giniCommittersOverFile.historic
- **Friendly name**: Historic giniCommittersOverFile
- **Historic version of**: trans.rascal.activecommitters.committersoverfile

Calculates the gini coefficient of committers per file

- <u>Depends-on</u>: `trans.rascal.activecommitters.committersoverfile`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.percentageOfWeekendCommits.historic](#trans.rascal.activecommitters.percentageOfWeekendCommits.historic)
- **Short name**: percentageOfWeekendCommits.historic
- **Friendly name**: Historic percentageOfWeekendCommits
- **Historic version of**: trans.rascal.activecommitters.percentageOfWeekendCommits

Percentage of commits made during the weekend

- <u>Depends-on</u>: `trans.rascal.activecommitters.percentageOfWeekendCommits`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.commitsPerDeveloper.historic](#trans.rascal.activecommitters.commitsPerDeveloper.historic)
- **Short name**: commitsPerDeveloper.historic
- **Friendly name**: Historic commitsPerDeveloper
- **Historic version of**: trans.rascal.activecommitters.commitsPerDeveloper

The number of commits per developer indicates not only the volume of the contribution of an individual but also the style in which he or she commits,
when combined with other metrics such as churn. Few and big commits are different from many small commits. This metric is used downstream by other metrics as well.

- <u>Depends-on</u>: `trans.rascal.activecommitters.commitsPerDeveloper`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.numberOfActiveCommittersLongTerm.historic](#trans.rascal.activecommitters.numberOfActiveCommittersLongTerm.historic)
- **Short name**: numberOfActiveCommittersLongTerm.historic
- **Friendly name**: Historic numberOfActiveCommittersLongTerm
- **Historic version of**: trans.rascal.activecommitters.numberOfActiveCommittersLongTerm

Number of long time active committers over time (active in last year). This measures a smooth window of one year, where every day we report the number of developers active in the previous 365 days.

- <u>Depends-on</u>: `trans.rascal.activecommitters.numberOfActiveCommittersLongTerm`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.numberOfActiveCommitters.historic](#trans.rascal.activecommitters.numberOfActiveCommitters.historic)
- **Short name**: numberOfActiveCommitters.historic
- **Friendly name**: Historic numberOfActiveCommitters
- **Historic version of**: trans.rascal.activecommitters.numberOfActiveCommitters

Number of active committers over time (active in last two weeks). This measures a smooth window of two weeks, where every day we report the number of developers in the previous 14 days.

- <u>Depends-on</u>: `trans.rascal.activecommitters.numberOfActiveCommitters`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.commitsToday.historic](#rascal.generic.churn.commitsToday.historic)
- **Short name**: commitsToday.historic
- **Friendly name**: Historic commitsToday
- **Historic version of**: rascal.generic.churn.commitsToday

Counts the number of commits made today.

- <u>Depends-on</u>: `rascal.generic.churn.commitsToday`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnToday.historic](#rascal.generic.churn.churnToday.historic)
- **Short name**: commitsToday.historic
- **Friendly name**: Historic commitsToday
- **Historic version of**: rascal.generic.churn.churnToday

Counts the churn for today: the total number of lines of code added and deleted. This metric is used further downstream to analyze trends.

- <u>Depends-on</u>: `rascal.generic.churn.churnToday`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnPerCommitInTwoWeeks.historic](#rascal.generic.churn.churnPerCommitInTwoWeeks.historic)
- **Short name**: churnPerCommitInTwoWeeks.historic
- **Friendly name**: Historic churnPerCommitInTwoWeeks
- **Historic version of**: rascal.generic.churn.churnPerCommitInTwoWeeks

The ratio between the churn and the number of commits indicates how large each commit is on average. We compute this as a sliding average over two weeks which smoothens exceptions and makes it possible to see a trend historically. Commits should not be to big all the time, because that would indicate either that programmers are not focusing on well-defined tasks or that the system architecture does not allow for separation of concerns.

- <u>Depends-on</u>: `rascal.generic.churn.churnPerCommitInTwoWeeks`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.filesPerCommit.historic](#rascal.generic.churn.filesPerCommit.historic)
- **Short name**: numberOfFilesPerCommit.historic
- **Friendly name**: Historic numberOfFilesPerCommit
- **Historic version of**: rascal.generic.churn.filesPerCommit

Counts the number of files per commit to find out about the separation of concerns in the architecture or in the tasks the programmers perform. This metric is used further downstream.

- <u>Depends-on</u>: `rascal.generic.churn.filesPerCommit`
- <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnPerCommit.historic](#rascal.generic.churn.churnPerCommit.historic)
- **Short name**: churnPerCommit.historic
- **Friendly name**: Historic churnPerCommit
- **Historic version of**: rascal.generic.churn.churnPerCommit

Count churn. Churn is the number lines added or deleted. We measure this per commit because the commit
is a basic unit of work for a programmer. This metric computes a table per commit for today and is not used for comparison between projects. It is used further downstream to analyze activity.

- <u>Depends-on</u>: `rascal.generic.churn.churnPerCommit`
- <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnPerCommitter.historic](#rascal.generic.churn.churnPerCommitter.historic)
- **Short name**: churnPerCommitter.historic
- **Friendly name**: Historic churnPerCommitter
- **Historic version of**: rascal.generic.churn.churnPerCommitter

Count churn per committer: the number of lines of code added and deleted. It zooms in on the single committer producing a table which can be used for downstream processing.

- <u>Depends-on</u>: `rascal.generic.churn.churnPerCommitter`
- <u>Returns</u>: `map[str author, int churn]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.commitsInTwoWeeks.historic](#rascal.generic.churn.commitsInTwoWeeks.historic)
- **Short name**: commitsInTwoWeeks.historic
- **Friendly name**: Historic commitsInTwoWeeks
- **Historic version of**: rascal.generic.churn.commitsInTwoWeeks

Churn in the last two weeks: aggregates the number of commits over a 14-day sliding window.

- <u>Depends-on</u>: `rascal.generic.churn.commitsInTwoWeeks`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnInTwoWeeks.historic](#rascal.generic.churn.churnInTwoWeeks.historic)
- **Short name**: churnInTwoWeeks.historic
- **Friendly name**: Historic churnInTwoWeeks
- **Historic version of**: rascal.generic.churn.churnInTwoWeeks

Churn in the last two weeks: aggregates the lines of code added and deleted over a 14-day sliding window.

- <u>Depends-on</u>: `rascal.generic.churn.churnInTwoWeeks`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.commits.messages.topics](#org.eclipse.scava.metricprovider.historic.commits.messages.topics)
- **Short name**: historic.commits.messages.topics
- **Friendly name**: Labels of topics in commits messages analyzed in the last 30 days

This metric computes the labels of topic clusters in commits messages pushed by users in the last 30 days

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.commits.message.topics`

- <u>Returns</u> :	`CommitsMessagesTopicsHistoricMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| commitMessageTopics			| `List<CommitMessageTopic>` |

<u>*Additional Information*</u> :

- CommitMessageTopic :
	- `String`	repository
	- `String`	labels
	- `int`	numberOfMessages
	- `List<String>`	commitsMessageId

<u>*Visualisation Output Information*</u> :

- CommitsMessagesTopicsHistoricMetricProvider :
	- `id`	commits.topics.messages

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Historic Metric Providers for Documentation](#historic-metric-providers-for-documentation)

The following Historic Metric Providers are associated with documentation analyses.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.documentation.readability](#org.eclipse.scava.metricprovider.historic.documentation.readability)
- **Short name**: historic.documentation.readability
- **Friendly name**: Documentation readability Historic Metric

Historic metric that stores the evolution of the documentation readability. The higher the readability score, the harder to understand the text. 

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.documentation.readability`

- <u>Returns</u> :	`DocumentationReadabilityHistoricMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| documentationReadability	| `List<DocumentationHistoricReadability>` |
	| documentationEntriesReadability | `List<DocumentationEntryHistoricReadability>` |

<u>*Additional Information*</u> :

- DocumentationHistoricReadability :
	- `String`	documentationId
	- `int`	numberOfDocumentationEntries
	- `double`	averageDocumentationReadability

- DocumentationEntryHistoricReadability :
	- `String`	documentationId
	- `String`	entryId
	- `double`	readability

<u>*Visualisation Output Information*</u> :

- readability :
	- `id`	documentation.readability.entries
	- `id`	documentation.readability

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.documentation.sentiment](#org.eclipse.scava.metricprovider.historic.documentation.sentiment)
- **Short name**: historic.documentation.sentiment
- **Friendly name**: Documentation sentiment polarity Historic Metric

Historic metric that stores the evolution of the documentation sentiment polarity. Sentiment score could be closer to -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment)

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.documentation.sentiment`

- <u>Returns</u> :	`DocumentationSentimentHistoricMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| documentationSentiment	| `List<DocumentationHistoricSentiment>` |
	| documentationEntriesSentiment | `List<DocumentationEntryHistoricSentiment>` |

<u>*Additional Information*</u> :

- DocumentationHistoricSentiment :
	- `String`	documentationId
	- `int`	numberOfDocumentationEntries
	- `double`	averageDocumentationSentiment

- DocumentationEntryHistoricSentiment :
	- `String`	documentationId
	- `String`	entryId
	- `String`	polarity

<u>*Visualisation Output Information*</u> :

- sentiment :
	- `id`	documentation.sentiment.entries
	- `id`	documentation.sentiment

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Historic Metric Providers for Generic Source Code](#historic-metric-providers-for-generic-source-code)

These metrics are related to the source code of analyzed projects, regardless of the language(s) they are written in.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.clones.cloneLOCPerLanguage.historic](#trans.rascal.clones.cloneLOCPerLanguage.historic)
- **Short name**: cloneLOCPerLanguage.historic
- **Friendly name**: Historic cloneLOCPerLanguage
- **Historic version of**: trans.rascal.clones.cloneLOCPerLanguage

Lines of code in Type I clones larger than 6 lines, per language. A Type I clone is a literal clone. A large number of literal clones is considered to be bad. This metric is not easily compared between systems because it is not size normalized yet. We use it for further processing downstream. You can analyze the trend over time using this metric.

- <u>Depends-on</u>: `trans.rascal.clones.cloneLOCPerLanguage`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.readability.fileReadabilityQuartiles.historic](#trans.rascal.readability.fileReadabilityQuartiles.historic)
- **Short name**: fileReadabilityQ.historic
- **Friendly name**: Historic fileReadabilityQ
- **Historic version of**: trans.rascal.readability.fileReadabilityQuartiles

We measure file readability by counting exceptions to common usage of whitespace in source code, such as spaces after commas. The quartiles
represent how many of the files have how many of these deviations. A few deviations per file is ok, but many files with many deviations indicates a
lack of attention to readability.

- <u>Depends-on</u>: `trans.rascal.readability.fileReadabilityQuartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.commentLinesPerLanguage.historic](#trans.rascal.comments.commentLinesPerLanguage.historic)
- **Short name**: commentLinesPerLanguage.historic
- **Friendly name**: Historic commentLinesPerLanguage
- **Historic version of**: trans.rascal.comments.commentLinesPerLanguage

Number of lines containing comments per language (excluding headers). The balance between comments and code indicates understandability. Too many comments are often not maintained and may lead to confusion, not enough means the code lacks documentation explaining its intent. This is a basic fact collection metric which is used further downstream.

- <u>Depends-on</u>: `trans.rascal.comments.commentLinesPerLanguage`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.commentedOutCodePerLanguage.historic](#trans.rascal.comments.commentedOutCodePerLanguage.historic)
- **Short name**: commentedOutCodePerLanguage.historic
- **Friendly name**: Historic commentedOutCodePerLanguage
- **Historic version of**: trans.rascal.comments.commentedOutCodePerLanguage

Lines of commented out code per file uses heuristics (frequency of certain substrings typically used in code and not in natural language) to find out how
much source code comments are actually commented out code. Commented out code is, in large quantities is a quality contra-indicator.

- <u>Depends-on</u>: `trans.rascal.comments.commentedOutCodePerLanguage`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.headerPercentage.historic](#trans.rascal.comments.headerPercentage.historic)
- **Short name**: headerPercentage.historic
- **Friendly name**: Historic headerPercentage
- **Historic version of**: trans.rascal.comments.headerPercentage

Percentage of files with headers is an indicator for the amount of files which have been tagged with a copyright statement (or not). If the number is low this indicates a problem with the copyright of the program. Source files without a copyright statement are not open-source, they are owned, in principle, by the author and may not be copied without permission. Note that the existence of a header does not guarantee the presence of an open-source license, but its absence certainly is telling.

- <u>Depends-on</u>: `trans.rascal.comments.headerPercentage`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.LOC.genericLOCoverFiles.historic](#trans.rascal.LOC.genericLOCoverFiles.historic)
- **Short name**: giniLOCOverFiles.historic
- **Friendly name**: Historic giniLOCOverFiles
- **Historic version of**: trans.rascal.LOC.genericLOCoverFiles

We find out how evenly the code is spread over files. The number should be quite stable over time. A jump in this metric indicates a large change in the code base. If the code is focused in only a few very large files then this may be a contra-indicator for quality.

- <u>Depends-on</u>: `trans.rascal.LOC.genericLOCoverFiles`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.LOC.locPerLanguage.historic](#trans.rascal.LOC.locPerLanguage.historic)
- **Short name**: locPerLanguage.historic
- **Friendly name**: Historic locPerLanguage
- **Historic version of**: trans.rascal.LOC.locPerLanguage

Physical lines of code simply counts the number of newline characters (OS independent) in a source code file. We accumulate this number per programming language.
The metric can be used to compare the volume between two systems and to assess in which programming language the bulk of the code is written.

- <u>Depends-on</u>: `trans.rascal.LOC.locPerLanguage`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Historic Metric Providers for Java code](#historic-metric-providers-for-java-code)

These metrics are related to the Java source code of analyzed projects.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.filesWithErrorProneness.historic](#style.filesWithErrorProneness.historic)
- **Short name**: filesWithErrorProneness.historic
- **Friendly name**: Historic filesWithErrorProneness
- **Historic version of**: style.filesWithErrorProneness

Percentage of files with error proneness

- <u>Depends-on</u>: `style.filesWithErrorProneness`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.filesWithUnderstandabilityIssues.historic](#style.filesWithUnderstandabilityIssues.historic)
- **Short name**: filesWithUnderstandabilityIssues.historic
- **Friendly name**: Historic filesWithUnderstandabilityIssues
- **Historic version of**: style.filesWithUnderstandabilityIssues

Percentage of files with understandability issues. This is a basic metric which can not be easily compared between projects.

- <u>Depends-on</u>: `style.filesWithUnderstandabilityIssues`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.spreadOfStyleViolations.historic](#style.spreadOfStyleViolations.historic)
- **Short name**: spreadOfStyleViolations.historic
- **Friendly name**: Historic spreadOfStyleViolations
- **Historic version of**: style.spreadOfStyleViolations

Between 0 and 1 how evenly spread are the style violations. This metric makes sense if there are more than 5 files in a project and can
be compared between projects as well. If problems are widespread this may be a quality contra-indicator, while a localized problem could be easily fixed.

- <u>Depends-on</u>: `style.spreadOfStyleViolations`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.filesWithInefficiencies.historic](#style.filesWithInefficiencies.historic)
- **Short name**: filesWithInefficiencies.historic
- **Friendly name**: Historic filesWithInefficiencies
- **Historic version of**: style.filesWithInefficiencies

Percentage of files with inefficiencies

- <u>Depends-on</u>: `style.filesWithInefficiencies`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.filesWithStyleViolations.historic](#style.filesWithStyleViolations.historic)
- **Short name**: filesWithStyleViolations.historic
- **Friendly name**: Historic filesWithStyleViolations
- **Historic version of**: style.filesWithStyleViolations

Percentage of files with style violations

- <u>Depends-on</u>: `style.filesWithStyleViolations`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.spreadOfUnderstandabilityIssues.historic](#style.spreadOfUnderstandabilityIssues.historic)
- **Short name**: spreadOfUnderstandabilityIssues.historic
- **Friendly name**: Historic spreadOfUnderstandabilityIssues
- **Historic version of**: style.spreadOfUnderstandabilityIssues

Between 0 and 1 how evenly spread are the understandability issues. This metric makes sense if there are more than 5 files in a project and can
be compared between projects as well. If problems are widespread this may be a quality contra-indicator, while a localized problem could be easily fixed.

- <u>Depends-on</u>: `style.spreadOfUnderstandabilityIssues`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.spreadOfInefficiencies.historic](#style.spreadOfInefficiencies.historic)
- **Short name**: spreadOfInefficiencies.historic
- **Friendly name**: Historic spreadOfInefficiencies
- **Historic version of**: style.spreadOfInefficiencies

Between 0 and 1 how evenly spread are the style violations which indicate inefficiencies. This metric makes sense if there are more than 5 files in a project and can
be compared between projects as well. If problems are widespread this may be a quality contra-indicator, while a localized problem could be easily fixed.

- <u>Depends-on</u>: `style.spreadOfInefficiencies`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.spreadOfErrorProneness.historic](#style.spreadOfErrorProneness.historic)
- **Short name**: spreadOfErrorProneness.historic
- **Friendly name**: Historic spreadOfErrorProneness
- **Historic version of**: style.spreadOfErrorProneness

Between 0 and 1 how evenly spread are the style violations which indicate error proneness. This metric makes sense if there are more than 5 files in a project and can
be compared between projects as well. If problems are widespread this may be a quality contra-indicator, while a localized problem could be easily fixed.

- <u>Depends-on</u>: `style.spreadOfErrorProneness`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.testability.java.TestOverPublicMethods.historic](#rascal.testability.java.TestOverPublicMethods.historic)
- **Short name**: percentageOfTestedPublicMethods.historic
- **Friendly name**: Historic percentageOfTestedPublicMethods
- **Historic version of**: rascal.testability.java.TestOverPublicMethods

Number of JUnit tests averaged over the total number of public methods. Ideally all public methods are tested. With this number we
compute how far from the ideal situation the project is.

- <u>Depends-on</u>: `rascal.testability.java.TestOverPublicMethods`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.testability.java.NumberOfTestMethods.historic](#rascal.testability.java.NumberOfTestMethods.historic)
- **Short name**: numberOfTestMethods.historic
- **Friendly name**: Historic numberOfTestMethods
- **Historic version of**: rascal.testability.java.NumberOfTestMethods

Number of JUnit test methods

- <u>Depends-on</u>: `rascal.testability.java.NumberOfTestMethods`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.testability.java.TestCoverage.historic](#rascal.testability.java.TestCoverage.historic)
- **Short name**: estimateTestCoverage.historic
- **Friendly name**: Historic estimateTestCoverage
- **Historic version of**: rascal.testability.java.TestCoverage

This is a static over-estimation of test coverage: which code is executed in the system when all JUnit test cases are executed? We approximate
this by using the static call graphs and assuming every method which can be called, will be called. This leads to an over-approximation,
as compared to a dynamic code coverage analysis, but the static analysis does follow the trend and a low code coverage here is an good indicator
for a lack in testing effort for the project.

- <u>Depends-on</u>: `rascal.testability.java.TestCoverage`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.Ca-Java-Quartiles.historic](#trans.rascal.OO.java.Ca-Java-Quartiles.historic)
- **Short name**: Ca_Java_Q.historic
- **Friendly name**: Historic Ca_Java_Q
- **Historic version of**: trans.rascal.OO.java.Ca-Java-Quartiles

Afferent coupling quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.Ca-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.CF-Java.historic](#trans.rascal.OO.java.CF-Java.historic)
- **Short name**: CF_Java.historic
- **Friendly name**: Historic CF_Java
- **Historic version of**: trans.rascal.OO.java.CF-Java

Coupling factor (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.CF-Java`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.DAC-Java-Quartiles.historic](#trans.rascal.OO.java.DAC-Java-Quartiles.historic)
- **Short name**: DAC_Java_Q.historic
- **Friendly name**: Historic DAC_Java_Q
- **Historic version of**: trans.rascal.OO.java.DAC-Java-Quartiles

Data abstraction coupling quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.DAC-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.MPC-Java-Quartiles.historic](#trans.rascal.OO.java.MPC-Java-Quartiles.historic)
- **Short name**: MPC_Java_Q.historic
- **Friendly name**: Historic MPC_Java_Q
- **Historic version of**: trans.rascal.OO.java.MPC-Java-Quartiles

Message passing coupling quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.MPC-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.PF-Java.historic](#trans.rascal.OO.java.PF-Java.historic)
- **Short name**: PF_Java.historic
- **Friendly name**: Historic PF_Java
- **Historic version of**: trans.rascal.OO.java.PF-Java

Polymorphism factor (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.PF-Java`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.RFC-Java-Quartiles.historic](#trans.rascal.OO.java.RFC-Java-Quartiles.historic)
- **Short name**: RFC_Java_Q.historic
- **Friendly name**: Historic RFC_Java_Q
- **Historic version of**: trans.rascal.OO.java.RFC-Java-Quartiles

Response for class quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.RFC-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.I-Java-Quartiles.historic](#trans.rascal.OO.java.I-Java-Quartiles.historic)
- **Short name**: I_Java_Q.historic
- **Friendly name**: Historic I_Java_Q
- **Historic version of**: trans.rascal.OO.java.I-Java-Quartiles

Instability quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.I-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.MIF-Java-Quartiles.historic](#trans.rascal.OO.java.MIF-Java-Quartiles.historic)
- **Short name**: MIF_Java_Q.historic
- **Friendly name**: Historic MIF_Java_Q
- **Historic version of**: trans.rascal.OO.java.MIF-Java-Quartiles

Method inheritance factor quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.MIF-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.MHF-Java.historic](#trans.rascal.OO.java.MHF-Java.historic)
- **Short name**: MHF_Java.historic
- **Friendly name**: Historic MHF_Java
- **Historic version of**: trans.rascal.OO.java.MHF-Java

Method hiding factor (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.MHF-Java`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.AHF-Java.historic](#trans.rascal.OO.java.AHF-Java.historic)
- **Short name**: AHF_Java.historic
- **Friendly name**: Historic AHF_Java
- **Historic version of**: trans.rascal.OO.java.AHF-Java

Attribute hiding factor (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.AHF-Java`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.LCOM-Java-Quartiles.historic](#trans.rascal.OO.java.LCOM-Java-Quartiles.historic)
- **Short name**: LCOM_Java_Q.historic
- **Friendly name**: Historic LCOM_Java_Q
- **Historic version of**: trans.rascal.OO.java.LCOM-Java-Quartiles

Lack of cohesion in methods quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.LCOM-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.A-Java.historic](#trans.rascal.OO.java.A-Java.historic)
- **Short name**: A_Java.historic
- **Friendly name**: Historic A_Java
- **Historic version of**: trans.rascal.OO.java.A-Java

Abstractness (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.A-Java`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.DIT-Java-Quartiles.historic](#trans.rascal.OO.java.DIT-Java-Quartiles.historic)
- **Short name**: DIT_Java_Q.historic
- **Friendly name**: Historic DIT_Java_Q
- **Historic version of**: trans.rascal.OO.java.DIT-Java-Quartiles

Depth of inheritance tree quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.DIT-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.TCC-Java-Quartiles.historic](#trans.rascal.OO.java.TCC-Java-Quartiles.historic)
- **Short name**: TCC_Java_Q.historic
- **Friendly name**: Historic TCC_Java_Q
- **Historic version of**: trans.rascal.OO.java.TCC-Java-Quartiles

Tight class cohesion quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.TCC-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.LCOM4-Java-Quartiles.historic](#trans.rascal.OO.java.LCOM4-Java-Quartiles.historic)
- **Short name**: LCOM4_Java_Q.historic
- **Friendly name**: Historic LCOM4_Java_Q
- **Historic version of**: trans.rascal.OO.java.LCOM4-Java-Quartiles

Lack of cohesion in methods 4 quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.LCOM4-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.SR-Java.historic](#trans.rascal.OO.java.SR-Java.historic)
- **Short name**: SR_Java.historic
- **Friendly name**: Historic SR_Java
- **Historic version of**: trans.rascal.OO.java.SR-Java

Specialization ratio (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.SR-Java`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.AIF-Java-Quartiles.historic](#trans.rascal.OO.java.AIF-Java-Quartiles.historic)
- **Short name**: AIF_Java_Q.historic
- **Friendly name**: Historic AIF_Java_Q
- **Historic version of**: trans.rascal.OO.java.AIF-Java-Quartiles

Attribute inheritance factor quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.AIF-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.NOC-Java-Quartiles.historic](#trans.rascal.OO.java.NOC-Java-Quartiles.historic)
- **Short name**: NOC_Java_Q.historic
- **Friendly name**: Historic NOC_Java_Q
- **Historic version of**: trans.rascal.OO.java.NOC-Java-Quartiles

Number of children quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.NOC-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.RR-Java.historic](#trans.rascal.OO.java.RR-Java.historic)
- **Short name**: RR_Java.historic
- **Friendly name**: Historic RR_Java
- **Historic version of**: trans.rascal.OO.java.RR-Java

Reuse ratio (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.RR-Java`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.LCC-Java-Quartiles.historic](#trans.rascal.OO.java.LCC-Java-Quartiles.historic)
- **Short name**: LCC_Java_Q.historic
- **Friendly name**: Historic LCC_Java_Q
- **Historic version of**: trans.rascal.OO.java.LCC-Java-Quartiles

Loose class cohesion quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.LCC-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.Ce-Java-Quartiles.historic](#trans.rascal.OO.java.Ce-Java-Quartiles.historic)
- **Short name**: Ce_Java_Q.historic
- **Friendly name**: Historic Ce_Java_Q
- **Historic version of**: trans.rascal.OO.java.Ce-Java-Quartiles

Efferent coupling quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.Ce-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.NOM-Java-Quartiles.historic](#trans.rascal.OO.java.NOM-Java-Quartiles.historic)
- **Short name**: NOM_Java_Q.historic
- **Friendly name**: Historic NOM_Java_Q
- **Historic version of**: trans.rascal.OO.java.NOM-Java-Quartiles

Number of methods quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.NOM-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.NOA-Java-Quartiles.historic](#trans.rascal.OO.java.NOA-Java-Quartiles.historic)
- **Short name**: NOA_Java_Q.historic
- **Friendly name**: Historic NOA_Java_Q
- **Historic version of**: trans.rascal.OO.java.NOA-Java-Quartiles

Number of attributes quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.NOA-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.CBO-Java-Quartiles.historic](#trans.rascal.OO.java.CBO-Java-Quartiles.historic)
- **Short name**: CBO_Java_Q.historic
- **Friendly name**: Historic CBO_Java_Q
- **Historic version of**: trans.rascal.OO.java.CBO-Java-Quartiles

Coupling between objects quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.CBO-Java-Quartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.advancedfeatures.java.AdvancedLanguageFeaturesJavaQuartiles.historic](#trans.rascal.advancedfeatures.java.AdvancedLanguageFeaturesJavaQuartiles.historic)
- **Short name**: countUsesOfAdvancedLanguageFeaturesQ.historic
- **Friendly name**: Historic countUsesOfAdvancedLanguageFeaturesQ
- **Historic version of**: trans.rascal.advancedfeatures.java.AdvancedLanguageFeaturesJavaQuartiles

Quartiles of counts of advanced Java features (wildcards, union types and anonymous classes). The numbers indicate the thresholds that delimit the first 25%, 50% and 75% of the data as well as the maximum and minumum values.

- <u>Depends-on</u>: `trans.rascal.advancedfeatures.java.AdvancedLanguageFeaturesJavaQuartiles`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.CC.java.CCHistogramJava.historic](#trans.rascal.CC.java.CCHistogramJava.historic)
- **Short name**: CCHistogramJava.historic
- **Friendly name**: Historic CCHistogramJava
- **Historic version of**: trans.rascal.CC.java.CCHistogramJava

Number of Java methods per CC risk factor, counts the number of methods which are in a low, medium or high risk factor. The histogram can be compared between projects to indicate which is probably easier to maintain on a method-by-method basis.

- <u>Depends-on</u>: `trans.rascal.CC.java.CCHistogramJava`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.CC.java.CCOverJavaMethods.historic](#trans.rascal.CC.java.CCOverJavaMethods.historic)
- **Short name**: giniCCOverMethodsJava.historic
- **Friendly name**: Historic giniCCOverMethodsJava
- **Historic version of**: trans.rascal.CC.java.CCOverJavaMethods

Calculates how cyclomatic complexity is spread over the methods of a system. If high CC is localized, then this may be easily fixed but if many methods have high complexity, then the project may be at risk. This metric is good to compare between projects.

- <u>Depends-on</u>: `trans.rascal.CC.java.CCOverJavaMethods`
- <u>Returns</u>: `real`

### [Historic Metric Providers for OSGi Dependencies](#historic-metric-providers-for-osgi-dependencies)

These metrics are related to OSGi dependencies declared in `MANIFEST.MF` files.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.numberOSGiBundleDependencies.historic](#trans.rascal.dependency.osgi.numberOSGiBundleDependencies.historic)
- **Short name**: numberOSGiBundleDependencies.historic
- **Friendly name**: Historic numberOSGiBundleDependencies
- **Historic version of**: trans.rascal.dependency.osgi.numberOSGiBundleDependencies

Retrieves the number of OSGi bunlde dependencies (i.e. Require-Bundle dependencies).

- <u>Depends-on</u>: `trans.rascal.dependency.osgi.numberOSGiBundleDependencies`
- <u>Returns</u>: `int`

### [Historic Metric Providers for Maven Dependencies](#historic-metric-providers-for-maven-dependencies)

These metrics are related to Maven dependencies declared in `pom.xml` files.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.maven.numberMavenDependencies.historic](#trans.rascal.dependency.maven.numberMavenDependencies.historic)
- **Short name**: numberMavenDependencies.historic
- **Friendly name**: Historic numberMavenDependencies
- **Historic version of**: trans.rascal.dependency.maven.numberMavenDependencies

Retrieves the number of Maven dependencies.

- <u>Depends-on</u>: `trans.rascal.dependency.maven.numberMavenDependencies`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Historic Metric Providers for Docker Dependencies](#historic-metric-providers-for-docker-dependencies)

The following Historic Metric Provider is associated with Docker Dependencies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.configuration.docker.dependencies](#org.eclipse.scava.metricprovider.historic.configuration.docker.dependencies)
- **Short name**: historic.configuration.docker.dependencies
- **Friendly name**: Number of dependencies defined in Dockerfiles per day

This metric computes the number of the dependencies that are defined in the Dockerfiles of a project per day. It also computes additional information such as the number of each version of the dependencies (image/package).

- <u>Depends-on</u>: `org.eclipse.scava.metricprovider.trans.configuration.docker.dependencies`
- <u>Returns</u> :	`DockerDependenciesHistoricMetric` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| numberOfDockerDependencies	| `int`			|
	| numberOfDockerPackageDependencies	| `int `	|
	| numberOfDockerImageDependencies	| `int `	|

<u>*Visualisation Output Information*</u> :

- DockerDependenciesHistoricMetric :
	- `id`	docker.dependencies
	- `id`	docker.packageDependencies
	- `id`	docker.imageDependencies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Historic Metric Providers for Puppet Dependencies](#historic-metric-providers-for-puppet-dependencies)

The following Historic Metric Provider is associated with Puppet Dependencies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.configuration.puppet.dependencies](#org.eclipse.scava.metricprovider.historic.configuration.puppet.dependencies)
- **Short name**: historic.configuration.puppet.dependencies
- **Friendly name**: Number of dependencies defined in Puppet manifests per day

This metric computes the number of the dependencies that are defined in the Puppet manifests of a project per day.

- <u>Depends-on</u>: `org.eclipse.scava.metricprovider.trans.configuration.puppet.dependencies`
- <u>Returns</u> :	`PuppetDependenciesHistoricMetric` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| numberOfPuppetDependencies	| `int`			|

<u>*Visualisation Output Information*</u> :

- DockerDependenciesHistoricMetric :
	- `id`	puppet.dependencies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------


### [Historic Metric Providers for Docker Smells](#historic-metric-providers-for-docker-smells)

The following Historic Metric Provider is associated with Docker Smells

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.configuration.docker.smells](#org.eclipse.scava.metricprovider.historic.configuration.docker.smells)
- **Short name**: historic.configuration.docker.smells
- **Friendly name**: Number of smells detected in Dockerfiles per day

This metric computes the number of the smells that are detected in the Dockerfiles of a project per day. It also computes additional information such as the number of each type of the smell.

- <u>Depends-on</u>: `org.eclipse.scava.metricprovider.trans.configuration.docker.smells`
- <u>Returns</u> :	`DockerSmellsHistoricMetric` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| cumulativeNumberOfDockerSmells	| `int`			|
	| numberOfImproperUpgradeSmells	| `int `	|
	| numberOfUnknownPackageVersionSmells	| `int `	|
	| numberOfUntaggedImageSmells	| `int`			|
	| numberOfImproperSudoSmells	| `int `	|
	| numberOfImproperCopySmells	| `int `	|
	| numberOfImproperFromSmells	| `int`			|
	| numberOfImproperCmdSmells	| `int `	|
	| numberOfMeaninglessSmells	| `int `	|
	| numberOfInvalidPortsSmells	| `int `	|
	| numberOfImproperShellSmells	| `int `	|
	| numberOfImproperEntrypointSmells	| `int `	|
	| numberOfDeprecatedInstructionSmells	| `int `	|

<u>*Visualisation Output Information*</u> :

- DockerDependenciesHistoricMetric :
	- `id`	docker.smells
	- `id`	docker.smells.improperUpgradeSmells
	- `id`	docker.smells.unknownPackageVersionSmells
	- `id`	docker.smells.untaggedImageSmells
	- `id`	docker.smells.improperSudoSmells
	- `id`	docker.smells.improperCopySmells
	- `id`	docker.smells.improperFromSmells
	- `id`	docker.smells.improperCmdSmells
	- `id`	docker.smells.meaninglessSmells
	- `id`	docker.smells.invalidPortsSmells
	- `id`	docker.smells.improperShellSmells
	- `id`	docker.smells.improperEntrypointSmells
	- `id`	docker.smells.deprecatedInstructionSmells

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Historic Metric Providers for Puppet Smells](#historic-metric-providers-for-puppet-smells)

The following Historic Metric Providers are associated with Puppet Smells

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.configuration.puppet.designsmells](#org.eclipse.scava.metricprovider.historic.configuration.puppet.designsmells)
- **Short name**: historic.configuration.puppet.designsmells
- **Friendly name**: Number of design smells detected in Puppet manifests per day

This metric computes the number of the design smells that are detected in the Puppet manifests of a project per day. It also computes additional information such as the number of each type of the smell.

- <u>Depends-on</u>: `org.eclipse.scava.metricprovider.trans.configuration.puppet.designsmells`
- <u>Returns</u> :	`PuppetDesignSmellsHistoricMetric` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| cumulativeNumberOfDesignSmells	| `int`			|
	| numberOfMultifacetedSmells	| `int `	|
	| numberOfUnnecessarySmells	| `int `	|
	| numberOfImperativeSmells	| `int`			|
	| numberOfMissAbSmells	| `int `	|
	| numberOfInsufficientSmells	| `int `	|
	| numberOfUnstructuredSmells	| `int`			|
	| numberOfTightSmells	| `int `	|
	| numberOfBrokenSmells	| `int `	|
	| numberOfMissingDepSmells	| `int `	|
	| numberOfHairballSmells	| `int `	|
	| numberOfDeficientSmells	| `int `	|
	| numberOfWeakenSmells	| `int `	|

<u>*Visualisation Output Information*</u> :

- DockerDependenciesHistoricMetric :
	- `id`	puppet.design.smells
	- `id`	puppet.design.multifacetedSmells
	- `id`	puppet.design.unnecessarySmells
	- `id`	puppet.design.imperativeSmells
	- `id`	puppet.design.missAbSmells
	- `id`	puppet.design.insufficientSmells
	- `id`	puppet.design.unstructuredSmells
	- `id`	puppet.design.tightSmells
	- `id`	puppet.design.brokenSmells
	- `id`	puppet.design.missingDepSmells
	- `id`	puppet.design.hairballSmells
	- `id`	puppet.design.deficientSmells
	- `id`	puppet.design.weakenSmells

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.historic.configuration.puppet.implementationsmells](#org.eclipse.scava.metricprovider.historic.configuration.puppet.implementationsmells)
- **Short name**: historic.configuration.puppet.implementationsmells
- **Friendly name**: Number of implementation smells detected in Puppet manifests per day

This metric computes the number of the implementation smells that are detected in the Puppet manifests of a project per day. It also computes additional information such as the number of each type of the smell.

- <u>Depends-on</u>: `org.eclipse.scava.metricprovider.trans.configuration.puppet.implementationsmells`
- <u>Returns</u> :	`PuppetImplementationSmellsHistoricMetric` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| cumulativeNumberOfImplementationSmells	| `int`			|
	| numberOfMissingDefaultCaseSmells	| `int `	|
	| numberOfInconsistentNamingSmells	| `int `	|
	| numberOfDuplicateEntitySmells	| `int`			|
	| numberOfMisplacedAttributeSmells	| `int `	|
	| numberOfImproperAlignment	| `int `	|
	| numberOfInvalidPropertySmells	| `int`			|
	| numberOfImproperQuoteSmells	| `int `	|
	| numberOfLongStatementsSmells	| `int `	|
	| numberOfUnguardedVariableSmells	| `int `	|
	| numberOfMissingDocSmells	| `int `	|
	| numberOfDeprecatedStatementsSmells	| `int `	|
	| numberOfIncompleteTasksSmells	| `int `	|
	| numberOfComplexExpressionSmells	| `int `	|
	| numberOfMissingElseSmells	| `int `	|

<u>*Visualisation Output Information*</u> :

- DockerDependenciesHistoricMetric :
	- `id`	puppet.implementation.smells
	- `id`	puppet.implementation.missingDefaultCaseSmells
	- `id`	puppet.implementation.inconsistentNamingSmells
	- `id`	puppet.implementation.duplicateEntitySmells
	- `id`	puppet.implementation.misplacedAttributeSmells
	- `id`	puppet.implementation.improperAlignmentSmells
	- `id`	puppet.implementation.invalidPropertySmells
	- `id`	puppet.implementation.improperQuoteSmells
	- `id`	puppet.implementation.longStatementsSmells
	- `id`	puppet.implementation.unguardedVariableSmells
	- `id`	puppet.implementation.missingDocSmells
	- `id`	puppet.implementation.deprecatedStatementsSmells
	- `id`	puppet.implementation.incompleteTasksSmells
	- `id`	puppet.implementation.complexExpressionSmells
	- `id`	puppet.implementation.missingElseSmells

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

## [Transient Metric Providers](#transient-metric-providers)

Transient metrics are used to calculate heuristics that are associated with a particular period in time, i.e. a single day. Transient Metrics are stored temporarily within the knowledge base and their output is passed as parameters in the calculation of other transient and historic metrics. Depending on the complexity, a transient metric can depend on the output from other tools, other transient metircs or have no dependencies at all.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Bug Trackers](#transient-metric-providers-for-bug-trackers)

The following Transient Metric Providers are associated with Issue trackers.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.activeusers](#org.eclipse.scava.metricprovider.trans.bugs.activeusers)
- **Short name**: trans.bugs.activeusers
- **Friendly name**: Number of users with new bug comment in the last 15 days

This metric computes the number of users that submitted new bug comments in the last 15 days, for each bug tracker.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.requestreplyclassification`

- <u>Returns</u> : ` BugsActiveUsersTransMetric` which contains:

	| Variable | Type						 |
	| -------- | ---------------- |
	| bugs		 | `List<BugsData>` |
	| users		| `List<User>`		 |

<u>*Additional Information*</u> :

- BugData :
	- `String` 	bugTrackerId
	- `int`	activeUsers
	- ` int `	inactiveUsers
	- `int`	previousUsers
	- `int`	users
	- `int`	days
- User :
	- `String`	bugTrackerId
	- `String`	userId
	- `String`	lastActivityDate
	- `int`	comments
	- `int`	requests
	- `int`	replies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.bugmetadata](#org.eclipse.scava.metricprovider.trans.bugs.bugmetadata)
- **Short name**: trans.bugs.bugmetadata
- **Friendly name**: Bug header metadata

This metric computes various metadata in bug header, i.e. priority, status, operation system and resolution. Other values computed by this metric includes average sentiment, content class and requests/replies.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.requestreplyclassification`,`org.eclipse.scava.metricprovider.trans.sentimentclassification`, `org.eclipse.scava.metricprovider.trans.detectingcode`

- <u>Returns</u> :	`BugsBugMetadataTransMetric` which contains:

	| Variable		| Type								|
	| ----------- | ------------------- |
	| BugData		 | `List<BugData>`		 |
	| CommentData | `List<CommentData>` |

<u>*Additional Information*</u> :

- BugData :
	- `String`	bugTrackerId
	- `String`	bugId
	- `String`	status
	- `List<String>`	resolution
	- `String`	operatingSystem
	- `String`	priority
	- `String`	creationTime
	- `String`	lastClosedTime
	- `String`	startSentiment
	- `String`	endSentiment
	- `float`	averageSentiment
	- `int`		commentSum
	- `int`		sentimentSum
	- `String`	firstCommentId
	- `String`	lastCommentId

- CommentData :
	- `String`	bugTrackerId
	- `String`	bugId
	-	`String`	commentId
	-	`String`	creationTime
	-	`String`	creator
	-	`String`	contentClass
	-	`String`	requestReplyPrediction

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.comments](#org.eclipse.scava.metricprovider.trans.bugs.comments)
- **Short name**: trans.bugs.comments
- **Friendly name**: Number of bug comments

This metric computes the number of bug comments, per bug tracker.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`BugsCommentsTransMetric` which contains:

	| Variable			 | Type									 |
	| -------------- | ---------------------- |
	| bugTrackerData | `List<BugTrackerData>` |

<u>*Additional Information*</u> :

- BugTrackerData:
	- `String`	bugTrackerId
	- `int`	numberOfComments
	- `int`	cumulativeNumberOfComments

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.contentclasses](#org.eclipse.scava.metricprovider.trans.bugs.contentclasses)
- **Short name**: trans.bugs.contentclasses
- **Friendly name**: Content classes in bug comments

This metric computes the frequency and percentage of content Classes in bug comments, per bug tracker.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.bugmetadata`

- <u>Returns</u> :	`BugsContentClassesTransMetric` which contains:

	| Variable			 | Type									 |
	| -------------- | ---------------------- |
	| bugTrackerData | `List<BugTrackerData>` |
	| contentClasses | `List<ContentClass>`	 |

<u>*Additional Information*</u> :

- BugTrackerData :
  - `String`	bugTrackerId
  - `int`	numberOfComments
- ContentClass :
  - `String`	bugTrackerId
  - `String`	classLabel
  - `int`	numberOfComments
  - `float`	percentage
    
<u>*Note*</u> : `classLabel` could be one of the content classes shown in the hierarchical tree structure below. Where a node consists of sub-trees of children, only the child nodes are considered as `classLabel`. For example, bug comments of type  **1. Clarification** can be labelled as either **1.1** or **1.2**. A node without sub-trees such as **2. Suggestion of solution** is considered `classLabel` on its own.

  ![Content Class Labels ](./content_class.png)

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.dailyrequestsreplies](#org.eclipse.scava.metricprovider.trans.bugs.dailyrequestsreplies)
- **Short name**: trans.bugs.dailyrequestsreplies
- **Friendly name**: Number of bug comments, requests and replies per day

This metric computes the number of bug comments, including those regarded as requests and replies each day, per bug tracker.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.requestreplyclassification`

- <u>Returns</u> :	`BugsDailyRequestsRepliesTransMetric` which contains:

	| Variable		| Type								|
	| ----------- | ------------------- |
	| dayComments | `List<DayComments>` |

<u>*Additional Information*</u> :

- DayComments :
	- `String`	name
	- `String`	bugTrackerId
	- `int`	numberOfComments
	- `int`	numberOfRequests
	- `int`	numberOfReplies
	- `float`	percentageOfComments
	- `float`	percentageOfRequests
	- `float`	percentageOfReplies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.emotions](#org.eclipse.scava.metricprovider.trans.bugs.emotions)
- **Short name**: trans.bugs.emotions
- **Friendly name**: Emotions in bug comments

This metric computes the emotional dimensions in bug comments, per bug tracker. There are 6 emotion labels (anger, fear, joy, sadness, love, surprise).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.emotionclassification`

- <u>Returns</u> :	`BugsEmotionsTransMetric` which contains:

	| Variable			 | Type										 |
	| -------------- | ------------------------ |
	| bugTrackerData | `List<BugTrackerData>`	 |
	| dimensions		 | `List<EmotionDimension>` |

<u>*Additional Information*</u> :

- BugTrackerData :
	- `String`	bugTrackerId
	- `int`	numberOfComments
	- `int`	cumulativeNumberOfComments
- EmotionDimension :
	- `String`	bugTrackerId
	- `String`	emotionLabel (`anger`, `fear`, `joy`, `sadness`, `love`, `surprise`)
	- `int`	numberOfComments
	- `int`	cumulativeNumberOfComments
	- `float`	percentage
	- `float`	cumulativePercentage

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.hourlyrequestsreplies](#org.eclipse.scava.metricprovider.trans.bugs.hourlyrequestsreplies)
- **Short name**: trans.bugs.hourlyrequestsreplies
- **Friendly name**: Number of bug comments, requests and replies per hour

This metric computes the number of bug comments, including those regarded as requests and replies, every hour of the day, per bug tracker.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.requestreplyclassification`

- <u>Returns</u> :	`BugsHourlyRequestsRepliesTransMetric` which contains:

	| Variable		 | Type								 |
	| ------------ | -------------------- |
	| hourComments | `List<HourComments>` |

<u>*Additional Information*</u> :

- HourComments :
	- `String`	bugTrackerId
	- `String`	hour
	- `int`	numberOfComments
	- `int`	numberOfRequests
	- `int`	numberOfReplies
	- `float`	percentageOfComments
	- `float`	percentageOfRequests
	- `float`	percentageOfReplies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.migrationissues](#org.eclipse.scava.metricprovider.trans.bugs.migrationissues)
- **Short name**: trans.bugs.migrationissues
- **Friendly name**: Migration Issues Detection in Bug Trackers

This metric detects migration issues in Bug Tracking Systems.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`, `org.eclipse.scava.metricprovider.trans.topics`

- <u>Returns</u> :	`BugTrackerMigrationIssueTransMetric` which contains:

	| Variable		 | Type								 |
	| ------------ | -------------------- |
	| bugTrackerMigrationIssues | `List<BugTrackerMigrationIssue>` |

<u>*Additional Information*</u> :

- BugTrackerMigrationIssue :
	- `String`	bugTrackerId
	- `String`	bugId
	- `String`  summary

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.migrationissuesmaracas](#org.eclipse.scava.metricprovider.trans.bugs.migrationissuesmaracas)
- **Short name**: trans.bugs.migrationissuesmaracas
- **Friendly name**: Migration Issues Detection Maracas in Bug Trackers

This metric detects migration issues in Bug Tracking Systems along with data from Maracas.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`, `org.eclipse.scava.metricprovider.trans.bugs.migrationissues`, `org.eclipse.scava.metricprovider.trans.migrationissuesmaracas`, `org.eclipse.scava.metricprovider.trans.plaintextprocessing`

- <u>Returns</u> :	`BugTrackerMigrationIssueMaracasTransMetric` which contains:

	| Variable		 | Type								 |
	| ------------ | -------------------- |
	| bugTrackerMigrationIssuesMaracas | `List<BugTrackerMigrationIssueMaracas>` |

<u>*Additional Information*</u> :

- BugTrackerMigrationIssueMaracas :
	- `String`	bugTrackerId
	- `String`	bugId
	- `List<String>` changes
	- `List<Double>` matchingPercentage

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.newbugs](#org.eclipse.scava.metricprovider.trans.bugs.newbugs)
- **Short name**: trans.bugs.newbugs
- **Friendly name**: Number of new bugs

This metric computes the number of new bugs over time, per bug tracker.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`BugsNewBugsTransMetric` which contains:

	| Variable			 | Type	 |
	| -------------- | ------ |
	| bugTrackerData | `type` |

<u>*Additional Information*</u> :

- BugTrackerData :
	- `String`	bugTrackerId
	- `int`	numberOfBugs
	- `int`	cumulativeNumberOfBugs

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.patches](#org.eclipse.scava.metricprovider.trans.bugs.patches)
- **Short name**: trans.bugs.patches
- **Friendly name**: Number of patches per bug

This metric computes the number of patches submitted by the community (users) for each bug.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`BugsPatchesTransMetric` which contains:

	| Variable			 | Type	 |
	| -------------- | ------ |
	| bugTrackerData | `type` |

<u>*Additional Information*</u> :

- BugTrackerData :
	- `String`	bugTrackerId
	- `int`	numberOfPatches
	- `int`	cumulativeNumberOfPatches

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.references](#org.eclipse.scava.metricprovider.trans.bugs.references)
- **Short name**: trans.bugs.references
- **Friendly name**: Bugs References

This metrics search for references of commits or bugs within comments comming from bugs comments.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`BugsReferenceTransMetric` which contains:

	| Variable | Type									|
	| -------- | --------------------- |
	| bugs		 | `List<BugReferringTo>` |

<u>*Additional Information*</u> :

- BugReferringTo :
	- `String`	bugTrackerId
	- `String`	bugId
	- `String`	commentId
	- `List<String>`	bugsReferred 	(URLs)
	- `List<String>`	commitsReferred (URLs)


<u>*Note*</u> :
	When this metric is used on GitHub, it should be noted that some references of bugs will be in fact pull requests. The reason is that GitHub considers pull requests equally as issues.


[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.bugs.requestsreplies](#org.eclipse.scava.metricprovider.trans.bugs.requestsreplies)
- **Short name**: trans.bugs.requestreplies
- **Friendly name**: Bug statistics (answered?, response time)

This metric computes for each bug, whether it was  answered. If so, it computes the time taken to respond.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.bugmetadata`

- <u>Returns</u> :	`BugsRequestsRepliesTransMetric` which contains:

	| Variable | Type									|
	| -------- | --------------------- |
	| bugs		 | `List<BugStatistics>` |

<u>*Additional Information*</u> :

- BugStatistics :
	- `String`	bugTrackerId
	- `String`	bugId
	- `boolean`	answered
	- `long`	responseDurationSec
	- `String`	responseDate

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Newsgroups and Forums](#transient-metric-providers-for-newsgroups-and-forums)

The following Transient Metric Providers are associated with communication channels in general, either newsgroups or forums.
Despite the name of the metrics are newsgroups, all the metrics are valid for communication channels.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.activeusers ](#org.eclipse.scava.metricprovider.trans.newsgroups.activeusers )
- **Short name**: trans.newsgroups.activeusers
- **Friendly name**: Number of users with new comment in the last 15 days

This metric computes the number of users that submitted news comments in the last 15 days, per newsgroup.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.requestreplyclassification`

- <u>Returns</u> :	`NewsgroupsActiveUsersTransMetric` which contains:

	| Variable			| Type									|
	| ------------- | --------------------- |
	| newsgroupData | `List<NewsgroupData>` |
	| user					| `List<User>`					|

<u>*Additional Information*</u> :

- NewsgroupData :
	- `String`	newsgroupName
	- `int`	activeUsers
	- `int`	inactiveUsers
	- `int`	previousUsers
	- `int`	users
	- `int`	days

- User :
	- `String`	newsgroupName
	- `String`	userId
	- `String`	lastActiveDate
	- `int`	articles
	- `int`	requests
	- `int`	replies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.articles](#org.eclipse.scava.metricprovider.trans.newsgroups.articles)
- **Short name**: trans.newsgroups.articles
- **Friendly name**: Number of articles per newsgroup

This metric computes the number of articles, per newsgroup.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`NewsgroupsArticlesTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| newsgroupData		 | `List<NewsgroupData>` |

<u>*Additional Information*</u> :

- NewsgroupData :
	- `String`	newsgroupName
	- `int`	numberOfArticles
	- `int`	cumulativeNumberOfArticles

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.contentclasses](#org.eclipse.scava.metricprovider.trans.newsgroups.contentclasses)
- **Short name**: trans.newsgroups.contentclasses
- **Friendly name**: Content classes in newsgroup articles

This metric computes the content classes in newgroup articles, per newsgroup.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.threads`

- <u>Returns</u> :	`NewsgroupsContentClassesTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| newsGroupData		 | `List<NewsgroupData>` |
	| contentClass		 | `List< ContentClass>` |

<u>*Additional Information*</u> :

- NewsGroupData:
	- `String`	newsgroupName
	- `int`	numberOfArticles

- ContentClass:
	- `String`	newsgroupName
	- `String`	classLabel
	- `int`	numberOfArticles
	- `float`	percentage

<u>*Note*</u> : `classLabel` could be one of the content classes shown in the hierarchical tree structure below. Where a node consists of sub-trees of children, only the child nodes are considered as `classLabel`. For example, articles of type  **1. Clarification** can be labelled as either **1.1** or **1.2**. A node without sub-trees such as **2. Suggestion of solution** is considered `classLabel` on its own.

  ![Content Class Labels ](./content_class.png)

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.dailyrequestsreplies](#org.eclipse.scava.metricprovider.trans.newsgroups.dailyrequestsreplies)
- **Short name**: trans.newsgroups.dailyrequestsreplies
- **Friendly name**: Number of articles, requests and replies per day

This metric computes the number of articles, including those regarded as requests and replies for each day of the week, per newsgroup.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.requestreplyclassification`

- <u>Returns</u> :	`NewsgroupsDailyRequestsRepliesTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| dailyArticles		 | `List<DailyArticles>` |

<u>*Additional Information*</u> :

- DailyArticles :
	- `String`	name
	- `int`	numberOfArticles
	- `int`	numberOfRequests
	- `int`	numberOfReplies
	- `float`	percentageOfArticles
	- `float`	percentageOfRequests
	- `float`	percentageOfReplies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.emotions](#org.eclipse.scava.metricprovider.trans.newsgroups.emotions)
- **Short name**: trans.newsgroups.emotions
- **Friendly name**: Emotions in newsgroup articles

This metric computes the emotional dimensions in newsgroup articles, per newsgroup. There are 6 emotion labels (anger, fear, joy, sadness, love, surprise).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.emotionclassification`

- <u>Returns</u> :	`NewsgroupsEmotionsTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| newsgroupData		 | `List<NewsgroupData>` |
	| emotionDimension		 | `List<EmotionDimension>` |

<u>*Additional Information*</u> :

- NewsgroupData :
	- `String`	newsgroupName
	- `int`	numberOfArticles
	- `int`	cumulativeNumberOfArticles

- EmotionDimension :
	- `String`	newsgroupName
	- `String`	emotionLabel (`anger`, `fear`, `joy`, `sadness`, `love`, `surprise`)
	- `int`	numberOfArticles
	- `int`	cumulativeNumberOfArticles
	- `float`	percentage
	- `float`	cumulativePercentage

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.hourlyrequestsreplies](#org.eclipse.scava.metricprovider.trans.newsgroups.hourlyrequestsreplies)
- **Short name**: trans.newsgroups.hourlyrequestsreplies
- **Friendly name**: Number of articles, requests and replies per hour

This metric computes the number of articles, including those regarded as requests and replies for each hour of the day, per newsgroup.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.requestreplyclassification`

- <u>Returns</u> :	`NewsgroupsHourlyRequestsRepliesTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| hourArticles		 | `List<HourArticles>` |

<u>*Additional Information*</u> :

- HourArticles :
	- `String`	hour
	- `int`	numberOfArticles
	- `int`	numberOfRequests
	- `int`	numberOfReplies
	- `float`	percentageOfArticles
	- `float`	percentageOfRequests
	- `float`	percentageOfReplies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.migrationissues](#org.eclipse.scava.metricprovider.trans.newsgroups.migrationissues)
- **Short name**: trans.newsgroups.migrationissues
- **Friendly name**: Migration Issues Detection in Communication Channels

This metric detects migration issues in Communication Channels articles.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`, `org.eclipse.scava.metricprovider.trans.topics`, `org.eclipse.scava.metricprovider.trans.newsgroups.threads`

- <u>Returns</u> :	`NewsgroupsMigrationIssueTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| newsgroupsMigrationIssues		 | `List<NewsgroupsMigrationIssue>` |

<u>*Additional Information*</u> :

- NewsgroupsMigrationIssue :
	- `String`	newsgroupName
	- `int`	threadId
	- `long` articleId

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.migrationissuesmaracas](#org.eclipse.scava.metricprovider.trans.newsgroups.migrationissuesmaracas)
- **Short name**: trans.newsgroups.migrationissuesmaracas
- **Friendly name**: Migration Issues Detection Maracas in Newsgroups

This metric detects migration issues in Newsgroups along with data from Maracas.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`, `org.eclipse.scava.metricprovider.trans.newsgroups.migrationissues`, `org.eclipse.scava.metricprovider.trans.migrationissuesmaracas`, `org.eclipse.scava.metricprovider.trans.plaintextprocessing`

- <u>Returns</u> :	`BugTrackerMigrationIssueMaracasTransMetric` which contains:

	| Variable		 | Type								 |
	| ------------ | -------------------- |
	| newsgroupsMigrationIssuesMaracas | `List<NewsgroupMigrationIssueMaracas>` |

<u>*Additional Information*</u> :

- NewsgroupMigrationIssueMaracas :
	- `String`	newsgrupName
	- `int`	threadId
	- `List<String>` changes
	- `List<Double>` matchingPercentage

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.sentiment](#org.eclipse.scava.metricprovider.trans.newsgroups.sentiment)
- **Short name**: trans.newsgroups.sentiment
- **Friendly name**: Average sentiment in newsgroup threads

The metric computes the average sentiment, including sentiment at the beginning and end of each thread, per newsgroup. Sentiment polarity value could be closer to -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment)

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.threads`, `org.eclipse.scava.metricprovider.trans.sentimentclassification`

- <u>Returns</u> :	`NewsgroupsSentimentTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| threadStatistics		 | `List<ThreadStatistics>` |

<u>*Additional Information*</u> :

- ThreadStatistics :
  - `String`	newsgroupName
  - `int`	threadId
  - `float`	averageSentiment
  - `String`	startSentiment
  - `String`	endSentiment

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.threads](#org.eclipse.scava.metricprovider.trans.newsgroups.threads)
- **Short name**: trans.newsgroups.threads
- **Friendly name**: Assigns newsgroup articles to threads

This metric holds information for assigning newsgroup articles to threads. The threading algorithm is executed from scratch every time.

- <u>Depends-on</u> : `None`,

- <u>Returns</u> :	`NewsgroupsThreadsTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| articleData		 | `List<ArticleData>` |
	| threadData		 | `List<ThreadData>` |
	| newsgroupData		 | `List<NewsgroupData>` |
	| currentDate		 | `List<CurrentDate>` |

<u>*Additional Information*</u> :

- ArticleData :
	- `String`	newsgroupName
	- `int`	articleNumber
	- `String`	articlesId
	- `String`	date
	- `String`	from
	- `String`	subject
	- `String`	contentClass
	- `String`	references

- ThreadData :
	- `int`	threadId

- NewsgroupData :
	- `String`	newsgroupName
	- `int`	threads
	- `int`	previousThreads

- CurrentDate :
	- `String`	date

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newsgroups.threadsrequestsreplies](#org.eclipse.scava.metricprovider.trans.newsgroups.threadsrequestsreplies)
- **Short name**: trans.newsgroups.threadsrequestsreplies
- **Friendly name**: Thread statistics (answered?, response time)

The metric computes for each thread whether it is answered. If so, it computes the response time.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.threads`, `org.eclipse.scava.metricprovider.trans.requestreplyclassification`

- <u>Returns</u> :	`NewsgroupsThreadsRequestsRepliesTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| threadStatistics		 | `List<ThreadStatistics>` |

<u>*Additional Information*</u> :

- ThreadStatistics :
	- `String`	newsgroupName
	- `int`	threadId
	- `boolean`	firstRequest
	- `boolean`	answered
	- `long`	responseDurationSec
	- `String`	responseDate

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Documentation](#transient-metric-providers-for-documentation)

The following Transient Metric Providers are associated with documentation analyses.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.documentation](#org.eclipse.scava.metricprovider.trans.documentation)
- **Short name**: trans.documentation
- **Friendly name**: Documentation processing

This metric process the files returned from the documentation readers and extracts the body (in format HTML or text)

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`

- <u>Returns</u> :	`DocumentationTransMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| documentationEntries	| `List<DocumentationEntry>` |
	| documentation | `List<Documentation>` |

<u>*Additional Information*</u> :

- DocumentationEntry :
	- `String`	documentationId
	- `String`	entryId
	- `String`	body
	- `String`	originalFormatName
	- `String`	originalFormatMime
	- `boolean`	htmlFormatted

- Documentation :
	- `String`	documentationId
	- `List<String>`	entriesId
	- `List<String>`	removedEntriesId
	- `String`	lastUpdateDate
	- `String`	lastRevisionAnalyzed
	- `String`	nextUpdateDate

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.documentation.classification](#org.eclipse.scava.metricprovider.trans.documentation.classification)
- **Short name**: trans.documentation.classification
- **Friendly name**: Documentation classification

This metric determines which type of documentation is present. The possible types are: *API*, *Development*, *Installation*, *Started*, *User*.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.documentation`, `org.eclipse.scava.metricprovider.trans.indexing.preparation`

- <u>Returns</u> :	`DocumentationClassificationTransMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| documentationEntriesClassification	| `List<DocumentationEntryClassification>` |

<u>*Additional Information*</u> :

- DocumentationEntryClassification :
	- `String`	documentationId
	- `String`	entryId
	- `List<String>`	types

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.documentation.detectingcode](#org.eclipse.scava.metricprovider.trans.documentation.detectingcode)
- **Short name**: trans.documentation.detectingcode
- **Friendly name**: Documentation detection of code

This metric process the plain text from documentation and detects the portions corresponding to code and natural language

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`, `org.eclipse.scava.metricprovider.trans.documentation.plaintext`

- <u>Returns</u> :	`DocumentationDetectingCodeTransMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| documentationEntriesDetectingCode	| `List<DocumentationEntryDetectingCode>` |

<u>*Additional Information*</u> :

- DocumentationEntryDetectingCode :
	- `String`	documentationId
	- `String`	entryId
	- `String`	naturalLanguage
	- `String`	code

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.documentation.plaintext](#org.eclipse.scava.metricprovider.trans.documentation.plaintext)
- **Short name**: trans.documentation.plaintext
- **Friendly name**: Documentation plain text processor

This metric process the body of each documentation entry and extracts the plain text

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`, `org.eclipse.scava.metricprovider.trans.documentation`

- <u>Returns</u> :	`DocumentationPlainTextTransMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| documentationEntriesPlainText	| `List<DocumentationEntryPlainText>` |

<u>*Additional Information*</u> :

- DocumentationEntryPlainText :
	- `String`	documentationId
	- `String`	entryId
	- `List<String>`	plainText

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.documentation.readability](#org.eclipse.scava.metricprovider.trans.documentation.readability)
- **Short name**: trans.documentation.readability
- **Friendly name**: Documentation calculation of readability

This metric calculates the readability of each documentation entry. The higher the score, the more difficult to understand the text.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`, `org.eclipse.scava.metricprovider.trans.documentation`, `org.eclipse.scava.metricprovider.trans.documentation.detectingcode`

- <u>Returns</u> :	`DocumentationReadabilityTransMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| documentationEntriesReadability	| `List<DocumentationEntryReadability>` |

<u>*Additional Information*</u> :

- DocumentationEntryReadability :
	- `String`	documentationId
	- `String`	entryId
	- `double`	readability

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.documentation.sentiment](#org.eclipse.scava.metricprovider.trans.documentation.sentiment)
- **Short name**: trans.documentation.sentiment
- **Friendly name**: Documentation Sentiment Analysis

This metric calculates the sentiment polarity of each documentation entry. Sentiment polarity value could be closer to -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment)

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`, `org.eclipse.scava.metricprovider.trans.documentation`, `org.eclipse.scava.metricprovider.trans.documentation.detectingcode`

- <u>Returns</u> :	`DocumentationSentimentTransMetric` which contains:

	| Variable							| Type												 |
	| --------------------- | ---------------------------- |
	| documentationEntriesSentiment	| `List<DocumentationEntrySentiment>` |

<u>*Additional Information*</u> :

- DocumentationEntrySentiment :
	- `String`	documentationId
	- `String`	entryId
	- `String`	polarity

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Natural Language Processing](#transient-metric-providers-for-natural-language-processing)

The following Transient Metric Providers are associated with Natural Language Processing tools.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.detectingcode](#org.eclipse.scava.metricprovider.trans.detectingcode)
- **Short name**: trans.detectingcode
- **Friendly name**: Distinguishes between code and natural language

This metric determines the parts of a bug comment or a newsgroup article that contains code or natural language.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.plaintextprocessing`

- <u>Returns</u> :	`DetectingCodeTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| bugTrackerComments		 | `List<BugTrackerCommentDetectingCode>` |
	| newsgroupArticles		 | `List<NewsgroupArticleDetectingCode>` |
	| forumPosts		 | `List<ForumPostsDetectingCode>` |

<u>*Additional Information*</u> :

- BugTrackerCommentDetectingCode :
	- `String`	bugTrackerId
	- `String`	bugId
	- `String`	commentId
	- `String`	naturalLanguage
	- `String`	code

- NewsgroupArticleDetectingCode :
	- `String`	newsgroupName
	- `String`	articleNumber
	- `String`	naturalLanguage
	- `String`	code

- ForumPostsDetectingCode :
	- `String`	forumId
	- `String`	topicId
	- `String`	postId
	- `String`	naturalLanguage
	- `String`	code

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.emotionclassification](#org.eclipse.scava.metricprovider.trans.emotionclassification)
- **Short name**: trans.emotionclassification
- **Friendly name**: Emotion classifier

This metric computes the emotions present in each bug comment, newsgroup article or forum post. There are 6 emotion labels (anger, fear, joy, sadness, love, surprise).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.detectingcode`

- <u>Returns</u> :	`EmotionClassificationTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| bugTrackerComments		 | `List<BugTrackerCommentEmotionClassification>` |
	| newsgroupArticles		 | `List<NewsgroupArticleEmotionClassification>` |
	| forumPosts		 | `List<ForumPostsEmotionClassification>` |

<u>*Additional Information*</u> :

- BugTrackerCommentEmotionClassification :
	- `String`	bugTrackerId
	- `String`	bugId
	- `String`	commentId
	- `String`	emotions

- NewsgroupArticleEmotionClassification :
	- `String`	newsgroupName
	- `String`	articleNumber
	- `String`	emotions

- ForumPostsEmotionClassification :
	- `String`	forumId
	- `String`	topicId
	- `String`	postId
	- `String`	emotions

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.plaintextprocessing](#org.eclipse.scava.metricprovider.trans.plaintextprocessing)
- **Short name**: trans.plaintextprocessing
- **Friendly name**: Plain text processing

This metric preprocess each bug comment, newsgroup article or forum post into a split plain text format.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`PlainTextProcessingTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| bugTrackerComments		 | `List<BugTrackerCommentPlainTextProcessing>` |
	| newsgroupArticles		 | `List<NewsgroupArticlePlainTextProcessing>` |
	| forumPosts		 | `List<ForumPostsPlainTextProcessing>` |

<u>*Additional Information*</u> :

- BugTrackerCommentPlainTextProcessing :
  - `String`	bugTrackerId
  - `String`	bugId
  - `String`	commentId
  - `String`	plainText
  - `boolean`	hadReplies

- NewsgroupArticlePlainTextProcessing :
  - `String`	newsgroupName
  - `String`	articleNumber
  - `String`	plainText
  - `boolean`	hadReplies

- ForumPostsPlainTextProcessing :
  - `String`	forumId
  - `String`	topicId
  - `String`	postId
  - `String`	plainText
  - `boolean`	hadReplies

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.requestreplyclassification](#org.eclipse.scava.metricprovider.trans.requestreplyclassification)
- **Short name**: trans.requestreplyclassification
- **Friendly name**: Request/Reply classification

This metric computes if a bug comment, newsgroup article or forum post is a request of a reply.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.plaintextprocessing`, `org.eclipse.scava.metricprovider.trans.detectingcode`

- <u>Returns</u> :	`RequestReplyClassificationTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| bugTrackerComments		 | `List<BugTrackerComments>` |
	| newsgroupArticles		 | `List<NewsgroupArticles>` |
	| forumPosts		 | `List<ForumPosts>` |

<u>*Additional Information*</u> :

- BugTrackerComments :
  - `String`	bugTrackerId
  - `String`	bugId
  - `String`	commentId
  - `String`	classificationResult
  - `String`	date

- NewsgroupArticles :
  - `String`	newsgroupName
  - `String`	articleNumber
  - `String`	classificationResult
  - `String`	date

- ForumPosts :
  - `String`	forumId
  - `String`	topicId
  - `String`	postId
  - `String`	classificationResult
  - `String`	date

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.sentimentclassification](#org.eclipse.scava.metricprovider.trans.sentimentclassification)
- **Short name**: trans.sentimentclassification
- **Friendly name**: Sentiment classification

This metric computes the sentiment of each bug comment, newsgroup article or forum post. Sentiment can be -1 (negative sentiment), 0 (neutral sentiment) or 1 (positive sentiment).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.detectingcode`

- <u>Returns</u> :	`SentimentClassificationTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| bugTrackerComments		 | `List<BugTrackerCommentsSentimentClassification>` |
	| newsgroupArticles		 | `List<NewsgroupArticlesSentimentClassification>` |
	| forumPosts		 | `List<ForumPostSentimentClassification>` |

<u>*Additional Information*</u> :

- BugTrackerCommentsSentimentClassification :
  - `String`	bugTrackerId
  - `String`	bugId
  - `String`	commentId
  - `String`	polarity (`negative (-1)`, `neutral (0)` or `positive (1)`)

- NewsgroupArticlesSentimentClassification :
  - `String`	newsgroupName
  - `String`	articleNumber
  - `String`	polarity (`negative (-1)`, `neutral (0)` or `positive (1)`)

- ForumPostSentimentClassification :
  - `String`	forumId
  - `String`	topicId
  - `String`	postId
  - `String`	polarity (`negative (-1)`, `neutral (0)` or `positive (1)`)

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.severityclassification](#org.eclipse.scava.metricprovider.trans.severityclassification)
- **Short name**: trans.severityclassification
- **Friendly name**: Severity classification

This metric computes the severity of each bug comment, newsgroup article or forum post. Severity could be blocker, critical, major, minor, enhancement,  normal). For bug comments, there is an additional severity level called `unknown`. A bug severity is considered `unknown` if there is not enough information for the classifier to make a decision. For example, an unanswered bug with no user comment to analyse.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.detectingcode`, `org.eclipse.scava.metricprovider.trans.newsgroups.threads`

- <u>Returns</u> :	`SeverityClassificationTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| bugTrackerBugs		 | `List<BugTrackerBugsData>` |
	| newsgroupArticles		 | `List<NewsgroupArticleData>` |
	| newsgroupThreads		 | `List<NewsgroupThreadData>` |
	| forumPosts		 | `ForumPostData>` |

<u>*Additional Information*</u> :

- BugTrackerBugsData :
  - `String`	bugTrackerId
  - `String`	bugId
  - `String`	severity
  - `int`	unigrams
  - `int`	bigrams
  - `int`	trigrams
  - `int`	quadgrams
  - `int`	charTrigrams
  - `int`	charQuadgrams
  - `int`	charFivegrams

- NewsgroupArticleData :
  - `String`	NewsgroupName
  - `long`	articleNumber
  - `int`	unigrams
  - `int`	bigrams
  - `int`	trigrams
  - `int`	quadgrams
  - `int`	charTrigrams
  - `int`	charQuadgrams
  - `int`	charFivegrams

- NewsgroupThreadData :
  - `String`	newsgroupName
  - `int`	threadId
  - `String`	severity

- BugTrackerBugsData :
  - `String`	forumId
  - `String`	topicId
  - `String`	severity
  - `int`	unigrams
  - `int`	bigrams
  - `int`	trigrams
  - `int`	quadgrams
  - `int`	charTrigrams
  - `int`	charQuadgrams
  - `int`	charFivegrams

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.topics](#org.eclipse.scava.metricprovider.trans.topics)
- **Short name**: trans.topics
- **Friendly name**: Topic clustering

This metric computes topic clusters for each bug comment, newsgroup article or forum post in the last 30 days.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.detectingcode`

- <u>Returns</u> :	`TopicsTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| bugTrackerComments		 | `List<BugTrackerCommentsData>` |
	| bugTrackerTopics		 | `List<BugTrackerTopic>` |
	| newsgroupArticles		 | `List<NewsgroupArticlesData>` |
	| newsgroupTopics		 | `List<NewsgroupTopic>` |

<u>*Additional Information*</u> :

- BugTrackerCommentsData :
  - `String`	bugTrackerId
  - `String`	bugId
  - `String`	commentId
  - `String`	subject
  - `String`	text
  - `String`	date

- NewsgroupArticlesData :
  - `String`	newsgroupName
  - `long`	articleNumber
  - `String`	subject
  - `String`	text
  - `String`	date

- BugTrackerTopic :
  - `String`	bugTrackerId
  - `List<String>`	labels
  - `int`	numberOfDocuments
  - `List<String>` commentsId

- NewsgroupTopic :
  - `String`	newsgroupName
  - `List<String>`	labels
  - `int`	numberOfDocuments
  - `List<Long>` articlesId

------

### [Transient Metric Providers for Commits and Committers](#transient-metric-providers-for-commits-and-committers)

These metrics are related to the commits and committers of a project.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.commits.message.plaintext](#org.eclipse.scava.metricprovider.trans.commits.message.plaintext)
- **Short name**: trans.commits.message.plaintext
- **Friendly name**: Commits message plain text

This metric preprocess each commit message to get a split plain text version.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`

- <u>Returns</u> :	`CommitsMessagePlainTextTransMetric` which contains:

	| Variable | Type									|
	| -------- | --------------------- |
	| commitsMessagesPlainText		 | `List<CommitMessagePlainText>` |

<u>*Additional Information*</u> :

- CommitMessagePlainText :
	- `String`	repository (URL)
	- `String`	revision (Commit SHA)
	- `List<String>`	plainText

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.commits.messagereferences](#org.eclipse.scava.metricprovider.trans.commits.messagereferences)
- **Short name**: trans.commits.messagereferences
- **Friendly name**: Commits Messages References

This metrics search for references of commits or bugs within the messages of commits. In order to detect bugs references, it is necessary to use at the same time one Bug Tracker, as the retrieval of references are based on patterns defined by bug trackers. If multiple or zero Bug Trackers are defined in the project, the metric will only search for commits (alphanumeric strings of 40 characters).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`

- <u>Returns</u> :	`CommitsMessageReferenceTransMetric` which contains:

	| Variable | Type									|
	| -------- | --------------------- |
	| commitsMessagesReferringTo		 | `List<CommitMessageReferringTo>` |

<u>*Additional Information*</u> :

- BugReferringTo :
	- `String`	repository (URL)
	- `String`	revision (Commit SHA)
	- `List<String>`	bugsReferred 	(URLs)
	- `List<String>`	commitsReferred (URLs)

<u>*Note*</u> :
	When this metric is used on GitHub, it should be noted that some references of bugs will be in fact pull requests. The reason is that GitHub considers pull requests equally as issues.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.commits.message.topics](#org.eclipse.scava.metricprovider.trans.commits.message.topics)
- **Short name**: trans.commits.message.topics
- **Friendly name**: Commits Messages Topic Clustering

This metric computes topic clusters for each commit message.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.commits.message.plaintext`

- <u>Returns</u> :	`CommitsMessageTopicsTransMetric` which contains:

	| Variable | Type									|
	| -------- | --------------------- |
	| commitsMessages		 | `List<CommitMessage>` |
	| commitsTopics		 | `List<CommitsTopic>` |

<u>*Additional Information*</u> :

- CommitMessage :
	- `String`	repository (URL)
	- `String`	revision (Commit SHA)
	- `String`	subject
	- `String`	message
	- `Date`	date

- CommitsTopic :
	- `String`	repository (URL)
	- `List<String>`	labels
	- `int`	numberOfMessages
	- `List<String>`	commitsMessageId

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.activeCommitters](#trans.rascal.activecommitters.activeCommitters)
- **Short name**: activeCommitters
- **Friendly name**: Committers of last two weeks

A list of committers who have been active the last two weeks. This metric is meant for downstream processing.

- <u>Depends-on</u>: `trans.rascal.activecommitters.committersToday`
- <u>Returns</u>: `rel[datetime,set[str]]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.committersoverfile](#trans.rascal.activecommitters.committersoverfile)
- **Short name**: giniCommittersOverFile
- **Friendly name**: Committers over file

Calculates the gini coefficient of committers per file

- <u>Depends-on</u>: `trans.rascal.activecommitters.countCommittersPerFile`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.countCommittersPerFile](#trans.rascal.activecommitters.countCommittersPerFile)
- **Short name**: countCommittersPerFile
- **Friendly name**: Number of committers per file

Count the number of committers that have touched a file.

- <u>Depends-on</u>: `trans.rascal.activecommitters.committersPerFile`
- <u>Returns</u>: `map[loc file, int numberOfCommitters]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.firstLastCommitDatesPerDeveloper](#trans.rascal.activecommitters.firstLastCommitDatesPerDeveloper)
- **Short name**: firstLastCommitDates
- **Friendly name**: First and last commit dates per developer

Collects per developer the first and last dates on which he or she contributed code. This basic metric is used downstream for other metrics, but
it is also used to drill down on the membership of specific individuals of the development team.

- <u>Depends-on</u>: `trans.rascal.activecommitters.committersToday`
- <u>Returns</u>: `map[str, tuple[datetime,datetime]]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.developmentTeam](#trans.rascal.activecommitters.developmentTeam)
- **Short name**: developmentTeam
- **Friendly name**: Development team

Lists the names of people who have been contributing code at least once in the history of the project.

- <u>Depends-on</u>: `trans.rascal.activecommitters.committersToday`
- <u>Returns</u>: `set[str]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.percentageOfWeekendCommits](#trans.rascal.activecommitters.percentageOfWeekendCommits)
- **Short name**: percentageOfWeekendCommits
- **Friendly name**: Percentage of weekend commits

Percentage of commits made during the weekend

- <u>Depends-on</u>: `trans.rascal.activecommitters.commitsPerWeekDay`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.maximumActiveCommittersEver](#trans.rascal.activecommitters.maximumActiveCommittersEver)
- **Short name**: maximumActiveCommittersEver
- **Friendly name**: Maximum active committers ever

What is the maximum number of committers who have been active together in any two week period?

- <u>Depends-on</u>: `trans.rascal.activecommitters.numberOfActiveCommitters.historic`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.developmentTeamEmails](#trans.rascal.activecommitters.developmentTeamEmails)
- **Short name**: developmentTeamEmails
- **Friendly name**: Development team

Lists the names of people who have been contributing code at least once in the history of the project.

- <u>Depends-on</u>: `trans.rascal.activecommitters.committersEmailsToday`
- <u>Returns</u>: `set[str]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.developmentDomainNames](#trans.rascal.activecommitters.developmentDomainNames)
- **Short name**: developmentDomainNames
- **Friendly name**: Development team domain names

Lists the domain names of email addresses of developers if such information is present.

- <u>Depends-on</u>: `trans.rascal.activecommitters.developmentTeamEmails`
- <u>Returns</u>: `set[str]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.committersPerFile](#trans.rascal.activecommitters.committersPerFile)
- **Short name**: committersPerFile
- **Friendly name**: Committers per file

Register which committers have contributed to which files

- <u>Depends-on</u>: - <u>Returns</u>: `rel[loc,str]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.longerTermActiveCommitters](#trans.rascal.activecommitters.longerTermActiveCommitters)
- **Short name**: longerTermActiveCommitters
- **Friendly name**: Committers of last year

Committers who have been active the last 12 months. This metric is meant for downstream processing.

- <u>Depends-on</u>: `trans.rascal.activecommitters.committersToday`
- <u>Returns</u>: `rel[datetime,set[str]]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.commitsPerDeveloper](#trans.rascal.activecommitters.commitsPerDeveloper)
- **Short name**: commitsPerDeveloper
- **Friendly name**: Number of commits per developer

The number of commits per developer indicates not only the volume of the contribution of an individual but also the style in which he or she commits,
when combined with other metrics such as churn. Few and big commits are different from many small commits. This metric is used downstream by other metrics as well.

- <u>Depends-on</u>: - <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.committersAge](#trans.rascal.activecommitters.committersAge)
- **Short name**: ageOfCommitters
- **Friendly name**: Developer experience in project

Measures in days the amount of time between the first and last contribution of each developer.

- <u>Depends-on</u>: `trans.rascal.activecommitters.firstLastCommitDatesPerDeveloper`
- <u>Returns</u>: `rel[str,int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.committersToday](#trans.rascal.activecommitters.committersToday)
- **Short name**: committersToday
- **Friendly name**: Active committers

Who have been active today?

- <u>Depends-on</u>: - <u>Returns</u>: `set[str]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.projectAge](#trans.rascal.activecommitters.projectAge)
- **Short name**: projectAge
- **Friendly name**: Age of the project (nr of days between first and last commit)

Age of the project (nr of days between first and last commit)

- <u>Depends-on</u>: `trans.rascal.activecommitters.firstLastCommitDatesPerDeveloper`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.commitsPerWeekDay](#trans.rascal.activecommitters.commitsPerWeekDay)
- **Short name**: commitsPerWeekDay
- **Friendly name**: Commits per week day

On which day of the week do commits take place?

- <u>Depends-on</u>: - <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.committersEmailsToday](#trans.rascal.activecommitters.committersEmailsToday)
- **Short name**: committersEmailsToday
- **Friendly name**: Active committers

Who have been active today?

- <u>Depends-on</u>: - <u>Returns</u>: `set[str]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.sizeOfDevelopmentTeam](#trans.rascal.activecommitters.sizeOfDevelopmentTeam)
- **Short name**: sizeOfDevelopmentTeam
- **Friendly name**: Size of development team

How many people have ever contributed code to this project?

- <u>Depends-on</u>: `trans.rascal.activecommitters.developmentTeam`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.numberOfActiveCommittersLongTerm](#trans.rascal.activecommitters.numberOfActiveCommittersLongTerm)
- **Short name**: numberOfActiveCommittersLongTerm
- **Friendly name**: Number of active committers long term

Number of long time active committers over time (active in last year). This measures a smooth window of one year, where every day we report the number of developers active in the previous 365 days.

- <u>Depends-on</u>: `trans.rascal.activecommitters.longerTermActiveCommitters`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.activecommitters.numberOfActiveCommitters](#trans.rascal.activecommitters.numberOfActiveCommitters)
- **Short name**: numberOfActiveCommitters
- **Friendly name**: Number of active committers

Number of active committers over time (active in last two weeks). This measures a smooth window of two weeks, where every day we report the number of developers in the previous 14 days.

- <u>Depends-on</u>: `trans.rascal.activecommitters.activeCommitters`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.commitsToday](#rascal.generic.churn.commitsToday)
- **Short name**: commitsToday
- **Friendly name**: Number of commits today

Counts the number of commits made today.

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnToday](#rascal.generic.churn.churnToday)
- **Short name**: commitsToday
- **Friendly name**: Churn of today

Counts the churn for today: the total number of lines of code added and deleted. This metric is used further downstream to analyze trends.

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnPerCommitInTwoWeeks](#rascal.generic.churn.churnPerCommitInTwoWeeks)
- **Short name**: churnPerCommitInTwoWeeks
- **Friendly name**: Churn per commit in two weeks

The ratio between the churn and the number of commits indicates how large each commit is on average. We compute this as a sliding average over two weeks which smoothens exceptions and makes it possible to see a trend historically. Commits should not be to big all the time, because that would indicate either that programmers are not focusing on well-defined tasks or that the system architecture does not allow for separation of concerns.

- <u>Depends-on</u>: `rascal.generic.churn.churnInTwoWeeks`
`rascal.generic.churn.commitsInTwoWeeks`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnActivity](#rascal.generic.churn.churnActivity)
- **Short name**: churnActivity
- **Friendly name**: Churn over the last two weeks

Churn in the last two weeks: collects the lines of code added and deleted over a 14-day sliding window.

- <u>Depends-on</u>: `rascal.generic.churn.churnToday`
- <u>Returns</u>: `rel[datetime,int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.commitActivity](#rascal.generic.churn.commitActivity)
- **Short name**: commitActivity
- **Friendly name**: Commits in last two weeks

Number of commits in the last two weeks: collects commit activity over a 14-day sliding window.

- <u>Depends-on</u>: `rascal.generic.churn.commitsToday`
- <u>Returns</u>: `rel[datetime,int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.coreCommittersChurn](#rascal.generic.churn.coreCommittersChurn)
- **Short name**: coreCommittersChurn
- **Friendly name**: Churn per core committer

Find out about the committers what their total number of added and deleted lines for this system.

- <u>Depends-on</u>: `rascal.generic.churn.churnPerCommitter`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.filesPerCommit](#rascal.generic.churn.filesPerCommit)
- **Short name**: numberOfFilesPerCommit
- **Friendly name**: Number of files per commit

Counts the number of files per commit to find out about the separation of concerns in the architecture or in the tasks the programmers perform. This metric is used further downstream.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnPerCommit](#rascal.generic.churn.churnPerCommit)
- **Short name**: churnPerCommit
- **Friendly name**: Counts number of lines added and deleted per commit.

Count churn. Churn is the number lines added or deleted. We measure this per commit because the commit
is a basic unit of work for a programmer. This metric computes a table per commit for today and is not used for comparison between projects. It is used further downstream to analyze activity.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnPerCommitter](#rascal.generic.churn.churnPerCommitter)
- **Short name**: churnPerCommitter
- **Friendly name**: Churn per committer

Count churn per committer: the number of lines of code added and deleted. It zooms in on the single committer producing a table which can be used for downstream processing.

- <u>Depends-on</u>: - <u>Returns</u>: `map[str author, int churn]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnPerFile](#rascal.generic.churn.churnPerFile)
- **Short name**: churnPerFile
- **Friendly name**: Churn per file

Churn per file counts the number of files added and deleted for a single file. This is a basic metric to indicate hotspots in the design of the system which is changed often. This metric is used further downstream.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc file, int churn]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.commitsInTwoWeeks](#rascal.generic.churn.commitsInTwoWeeks)
- **Short name**: commitsInTwoWeeks
- **Friendly name**: Number of commits in the last two weeks

Churn in the last two weeks: aggregates the number of commits over a 14-day sliding window.

- <u>Depends-on</u>: `rascal.generic.churn.commitActivity`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.generic.churn.churnInTwoWeeks](#rascal.generic.churn.churnInTwoWeeks)
- **Short name**: churnInTwoWeeks
- **Friendly name**: Sum of churn in the last two weeks

Churn in the last two weeks: aggregates the lines of code added and deleted over a 14-day sliding window.

- <u>Depends-on</u>: `rascal.generic.churn.churnActivity`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Generic Source Code](#transient-metric-providers-for-generic-source-code)

These metrics are related to the source code of analyzed projects, regardless of the language(s) they are written in.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.readability.fileReadability](#trans.rascal.readability.fileReadability)
- **Short name**: fileReadability
- **Friendly name**: File readability

Code readability per file, measured by use of whitespace measures deviations from common usage of whitespace in source code, such
as spaces after commas. This is a basic collection metric which is used further downstream.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.readability.fileReadabilityQuartiles](#trans.rascal.readability.fileReadabilityQuartiles)
- **Short name**: fileReadabilityQ
- **Friendly name**: File readability quartiles

We measure file readability by counting exceptions to common usage of whitespace in source code, such as spaces after commas. The quartiles
represent how many of the files have how many of these deviations. A few deviations per file is ok, but many files with many deviations indicates a
lack of attention to readability.

- <u>Depends-on</u>: `trans.rascal.readability.fileReadability`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.headerCounts](#trans.rascal.comments.headerCounts)
- **Short name**: headerCounts
- **Friendly name**: Number of appearances of estimated unique headers

In principle it is expected for the files in a project to share the same license. The license text in the header of each file may differ slightly due to different copyright years and or lists of contributors. The heuristic allows for slight differences. The metric produces the number of different types of header files found. A high number is a contra-indicator, meaning either a confusing licensing scheme or the source code of many different projects is included in the code base of the analyzed system.

- <u>Depends-on</u>: - <u>Returns</u>: `list[int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.commentedOutCode](#trans.rascal.comments.commentedOutCode)
- **Short name**: commentedOutCode
- **Friendly name**: Lines of commented out code per file

Lines of commented out code per file uses heuristics (frequency of certain substrings typically used in code and not in natural language) to find out how
much source code comments are actually commented out code. Commented out code is, in large quantities is a quality contra-indicator.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.commentLOC](#trans.rascal.comments.commentLOC)
- **Short name**: commentLOC
- **Friendly name**: Number of lines containing comments per file

Number of lines containing comments per file is a basic metric used for downstream processing. This metric does not consider the difference
between natural language comments and commented out code.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.commentLinesPerLanguage](#trans.rascal.comments.commentLinesPerLanguage)
- **Short name**: commentLinesPerLanguage
- **Friendly name**: Number of lines containing comments per language (excluding headers)

Number of lines containing comments per language (excluding headers). The balance between comments and code indicates understandability. Too many comments are often not maintained and may lead to confusion, not enough means the code lacks documentation explaining its intent. This is a basic fact collection metric which is used further downstream.

- <u>Depends-on</u>: `trans.rascal.comments.commentLOC`
`trans.rascal.comments.headerLOC`
`trans.rascal.comments.commentedOutCode`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.commentedOutCodePerLanguage](#trans.rascal.comments.commentedOutCodePerLanguage)
- **Short name**: commentedOutCodePerLanguage
- **Friendly name**: Lines of commented out code per language

Lines of commented out code per file uses heuristics (frequency of certain substrings typically used in code and not in natural language) to find out how
much source code comments are actually commented out code. Commented out code is, in large quantities is a quality contra-indicator.

- <u>Depends-on</u>: `trans.rascal.comments.commentedOutCode`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.headerLOC](#trans.rascal.comments.headerLOC)
- **Short name**: headerLOC
- **Friendly name**: Header size per file

Header size per file is a basic metric counting the size of the comment at the start of each file. It is used for further processing downstream.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.matchingLicenses](#trans.rascal.comments.matchingLicenses)
- **Short name**: matchingLicenses
- **Friendly name**: Used licenses (from selected list of known licenses)

We match against a list of known licenses to find out which are used in the current project

- <u>Depends-on</u>: - <u>Returns</u>: `set[str]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.comments.headerPercentage](#trans.rascal.comments.headerPercentage)
- **Short name**: headerPercentage
- **Friendly name**: Percentage of files with headers.

Percentage of files with headers is an indicator for the amount of files which have been tagged with a copyright statement (or not). If the number is low this indicates a problem with the copyright of the program. Source files without a copyright statement are not open-source, they are owned, in principle, by the author and may not be copied without permission. Note that the existence of a header does not guarantee the presence of an open-source license, but its absence certainly is telling.

- <u>Depends-on</u>: `trans.rascal.comments.headerLOC`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.LOC.genericLOC](#trans.rascal.LOC.genericLOC)
- **Short name**: countLoc
- **Friendly name**: Language independent physical lines of code

Physical lines of code simply counts the number of newline characters (OS independent) in a source code file.
The metric can be used to compare the volume between two systems.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.LOC.genericLOCoverFiles](#trans.rascal.LOC.genericLOCoverFiles)
- **Short name**: giniLOCOverFiles
- **Friendly name**: Spread of code over files

We find out how evenly the code is spread over files. The number should be quite stable over time. A jump in this metric indicates a large change in the code base. If the code is focused in only a few very large files then this may be a contra-indicator for quality.

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.LOC.locPerLanguage](#trans.rascal.LOC.locPerLanguage)
- **Short name**: locPerLanguage
- **Friendly name**: Physical lines of code per language

Physical lines of code simply counts the number of newline characters (OS independent) in a source code file. We accumulate this number per programming language.
The metric can be used to compare the volume between two systems and to assess in which programming language the bulk of the code is written.

- <u>Depends-on</u>: `trans.rascal.LOC.genericLOC`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.clones.cloneLOCPerLanguage](#trans.rascal.clones.cloneLOCPerLanguage)
- **Short name**: cloneLOCPerLanguage
- **Friendly name**: Lines of code in Type I clones larger than 6 lines, per language

Lines of code in Type I clones larger than 6 lines, per language. A Type I clone is a literal clone. A large number of literal clones is considered to be bad. This metric is not easily compared between systems because it is not size normalized yet. We use it for further processing downstream. You can analyze the trend over time using this metric.

- <u>Depends-on</u>: - <u>Returns</u>: `map[str, int]`

------

### [Transient Metric Providers for Java Code](#transient-metric-providers-for-java-code)

These metrics are related to the Java source code of analyzed projects.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.filesWithErrorProneness](#style.filesWithErrorProneness)
- **Short name**: filesWithErrorProneness
- **Friendly name**: Files with style violations which make the code error prone. This is basic metric which can not be easily compared between projects.

Percentage of files with error proneness

- <u>Depends-on</u>: `style.errorProneness`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.understandability](#style.understandability)
- **Short name**: understandability
- **Friendly name**: Inefficient code

Percentage of the projects files with coding style violations which indicate the code may be hard to read and understand,
but not necessarily more error prone.

- <u>Depends-on</u>: `style.styleViolations`
- <u>Returns</u>: `Table`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.inefficiencies](#style.inefficiencies)
- **Short name**: inefficiencies
- **Friendly name**: Inefficient code

Percentage of the projects files with coding style violations which indicate common inefficient ways of doing things in Java.

- <u>Depends-on</u>: `style.styleViolations`
- <u>Returns</u>: `Table`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.filesWithUnderstandabilityIssues](#style.filesWithUnderstandabilityIssues)
- **Short name**: filesWithUnderstandabilityIssues
- **Friendly name**: Files with style violations which make the code harder to understand

Percentage of files with understandability issues. This is a basic metric which can not be easily compared between projects.

- <u>Depends-on</u>: `style.understandability`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.errorProneness](#style.errorProneness)
- **Short name**: errorProneness
- **Friendly name**: Error proneness

Percentage of the projects files with coding style violations which indicate error prone code. This is a basic metric which collects per file all the style violations, recording the line number and the kind of style violation.
  Each kind of violation is grouped into a category. The resulting table is hard to interpret manually and can not be compared between projects.
  Other metrics further downstream do aggregate this information.

- <u>Depends-on</u>: `style.styleViolations`
- <u>Returns</u>: `Table`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.spreadOfStyleViolations](#style.spreadOfStyleViolations)
- **Short name**: spreadOfStyleViolations
- **Friendly name**: Spread of style violations over files

Between 0 and 1 how evenly spread are the style violations. This metric makes sense if there are more than 5 files in a project and can
be compared between projects as well. If problems are widespread this may be a quality contra-indicator, while a localized problem could be easily fixed.

- <u>Depends-on</u>: `style.styleViolations`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.filesWithInefficiencies](#style.filesWithInefficiencies)
- **Short name**: filesWithInefficiencies
- **Friendly name**: Files with style violations which indicate inefficiencies. This is a basic metric which can not be easily compared between projects.

Percentage of files with inefficiencies

- <u>Depends-on</u>: `style.inefficiencies`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.filesWithStyleViolations](#style.filesWithStyleViolations)
- **Short name**: filesWithStyleViolations
- **Friendly name**: Counts the number of files with any kind of style violation. This metric can not be easily compared between projects.

Percentage of files with style violations

- <u>Depends-on</u>: `style.styleViolations`
- <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.spreadOfUnderstandabilityIssues](#style.spreadOfUnderstandabilityIssues)
- **Short name**: spreadOfUnderstandabilityIssues
- **Friendly name**: Spread of understandability issues over files

Between 0 and 1 how evenly spread are the understandability issues. This metric makes sense if there are more than 5 files in a project and can
be compared between projects as well. If problems are widespread this may be a quality contra-indicator, while a localized problem could be easily fixed.

- <u>Depends-on</u>: `style.understandability`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.spreadOfInefficiencies](#style.spreadOfInefficiencies)
- **Short name**: spreadOfInefficiencies
- **Friendly name**: Spread of inefficiencies over files

Between 0 and 1 how evenly spread are the style violations which indicate inefficiencies. This metric makes sense if there are more than 5 files in a project and can
be compared between projects as well. If problems are widespread this may be a quality contra-indicator, while a localized problem could be easily fixed.

- <u>Depends-on</u>: `style.inefficiencies`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.styleViolations](#style.styleViolations)
- **Short name**: styleViolations
- **Friendly name**: All style violations


  This is a basic metric which collects per file all the style violations, recording the line number and the kind of style violation.
  Each kind of violation is grouped into a category. The resulting table is hard to interpret manually and can not be compared between projects.
  Other metrics further downstream do aggregate this information.


- <u>Depends-on</u>: - <u>Returns</u>: `Table`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [style.spreadOfErrorProneness](#style.spreadOfErrorProneness)
- **Short name**: spreadOfErrorProneness
- **Friendly name**: Spread of error proneness style violations over files

Between 0 and 1 how evenly spread are the style violations which indicate error proneness. This metric makes sense if there are more than 5 files in a project and can
be compared between projects as well. If problems are widespread this may be a quality contra-indicator, while a localized problem could be easily fixed.

- <u>Depends-on</u>: `style.errorProneness`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.testability.java.TestOverPublicMethods](#rascal.testability.java.TestOverPublicMethods)
- **Short name**: percentageOfTestedPublicMethods
- **Friendly name**: Number of JUnit tests averaged over the total number of public methods

Number of JUnit tests averaged over the total number of public methods. Ideally all public methods are tested. With this number we
compute how far from the ideal situation the project is.

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.testability.java.NumberOfTestMethods](#rascal.testability.java.NumberOfTestMethods)
- **Short name**: numberOfTestMethods
- **Friendly name**: Number of JUnit test methods. This is an intermediate absolute metric used to compute others. The bare metric is hard to compare between projects.

Number of JUnit test methods

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [rascal.testability.java.TestCoverage](#rascal.testability.java.TestCoverage)
- **Short name**: estimateTestCoverage
- **Friendly name**: Static Estimation of test coverage

This is a static over-estimation of test coverage: which code is executed in the system when all JUnit test cases are executed? We approximate
this by using the static call graphs and assuming every method which can be called, will be called. This leads to an over-approximation,
as compared to a dynamic code coverage analysis, but the static analysis does follow the trend and a low code coverage here is an good indicator
for a lack in testing effort for the project.

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.MIF-Java](#trans.rascal.OO.java.MIF-Java)
- **Short name**: MIF_Java
- **Friendly name**: Method inheritance factor (Java)

Method inheritance factor (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.Ca-Java-Quartiles](#trans.rascal.OO.java.Ca-Java-Quartiles)
- **Short name**: Ca_Java_Q
- **Friendly name**: Afferent coupling quartiles (Java)

Afferent coupling quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.Ca-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.DAC-Java](#trans.rascal.OO.java.DAC-Java)
- **Short name**: DAC_Java
- **Friendly name**: Data abstraction coupling (Java)

Data abstraction coupling (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.CF-Java](#trans.rascal.OO.java.CF-Java)
- **Short name**: CF_Java
- **Friendly name**: Coupling factor (Java)

Coupling factor (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.I-Java](#trans.rascal.OO.java.I-Java)
- **Short name**: I_Java
- **Friendly name**: Instability (Java)

Instability (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.Ce-Java`
`trans.rascal.OO.java.Ca-Java`
- <u>Returns</u>: `map[loc, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.DAC-Java-Quartiles](#trans.rascal.OO.java.DAC-Java-Quartiles)
- **Short name**: DAC_Java_Q
- **Friendly name**: Data abstraction coupling quartiles (Java)

Data abstraction coupling quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.DAC-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.MPC-Java-Quartiles](#trans.rascal.OO.java.MPC-Java-Quartiles)
- **Short name**: MPC_Java_Q
- **Friendly name**: Message passing coupling quartiles (Java)

Message passing coupling quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.MPC-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.NOM-Java](#trans.rascal.OO.java.NOM-Java)
- **Short name**: NOM_Java
- **Friendly name**: Number of methods (Java)

Number of methods (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.LCOM-Java](#trans.rascal.OO.java.LCOM-Java)
- **Short name**: LCOM_Java
- **Friendly name**: Lack of cohesion in methods (Java)

Lack of cohesion in methods (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.CBO-Java](#trans.rascal.OO.java.CBO-Java)
- **Short name**: CBO_Java
- **Friendly name**: Coupling between objects (Java)

Coupling between objects (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.Ce-Java](#trans.rascal.OO.java.Ce-Java)
- **Short name**: Ce_Java
- **Friendly name**: Efferent coupling (Java)

Efferent coupling (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.PF-Java](#trans.rascal.OO.java.PF-Java)
- **Short name**: PF_Java
- **Friendly name**: Polymorphism factor (Java)

Polymorphism factor (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.RFC-Java-Quartiles](#trans.rascal.OO.java.RFC-Java-Quartiles)
- **Short name**: RFC_Java_Q
- **Friendly name**: Response for class quartiles (Java)

Response for class quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.RFC-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.I-Java-Quartiles](#trans.rascal.OO.java.I-Java-Quartiles)
- **Short name**: I_Java_Q
- **Friendly name**: Instability quartiles (Java)

Instability quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.I-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.RFC-Java](#trans.rascal.OO.java.RFC-Java)
- **Short name**: RFC_Java
- **Friendly name**: Response for class (Java)

Response for class (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.LCC-Java](#trans.rascal.OO.java.LCC-Java)
- **Short name**: LCC_Java
- **Friendly name**: Loose class cohesion (Java)

Loose class cohesion (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.MIF-Java-Quartiles](#trans.rascal.OO.java.MIF-Java-Quartiles)
- **Short name**: MIF_Java_Q
- **Friendly name**: Method inheritance factor quartiles (Java)

Method inheritance factor quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.MIF-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.DIT-Java](#trans.rascal.OO.java.DIT-Java)
- **Short name**: DIT_Java
- **Friendly name**: Depth of inheritance tree (Java)

Depth of inheritance tree (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.MHF-Java](#trans.rascal.OO.java.MHF-Java)
- **Short name**: MHF_Java
- **Friendly name**: Method hiding factor (Java)

Method hiding factor (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.TCC-Java](#trans.rascal.OO.java.TCC-Java)
- **Short name**: TCC_Java
- **Friendly name**: Tight class cohesion (Java)

Tight class cohesion (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.AHF-Java](#trans.rascal.OO.java.AHF-Java)
- **Short name**: AHF_Java
- **Friendly name**: Attribute hiding factor (Java)

Attribute hiding factor (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.LCOM-Java-Quartiles](#trans.rascal.OO.java.LCOM-Java-Quartiles)
- **Short name**: LCOM_Java_Q
- **Friendly name**: Lack of cohesion in methods quartiles (Java)

Lack of cohesion in methods quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.LCOM-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.Ca-Java](#trans.rascal.OO.java.Ca-Java)
- **Short name**: Ca_Java
- **Friendly name**: Afferent coupling (Java)

Afferent coupling (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.A-Java](#trans.rascal.OO.java.A-Java)
- **Short name**: A_Java
- **Friendly name**: Abstractness (Java)

Abstractness (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.DIT-Java-Quartiles](#trans.rascal.OO.java.DIT-Java-Quartiles)
- **Short name**: DIT_Java_Q
- **Friendly name**: Depth of inheritance tree quartiles (Java)

Depth of inheritance tree quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.DIT-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.TCC-Java-Quartiles](#trans.rascal.OO.java.TCC-Java-Quartiles)
- **Short name**: TCC_Java_Q
- **Friendly name**: Tight class cohesion quartiles (Java)

Tight class cohesion quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.TCC-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.LCOM4-Java-Quartiles](#trans.rascal.OO.java.LCOM4-Java-Quartiles)
- **Short name**: LCOM4_Java_Q
- **Friendly name**: Lack of cohesion in methods 4 quartiles (Java)

Lack of cohesion in methods 4 quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.LCOM4-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.LCOM4-Java](#trans.rascal.OO.java.LCOM4-Java)
- **Short name**: LCOM4_Java
- **Friendly name**: Lack of cohesion in methods 4 (Java)

Lack of cohesion in methods 4 (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.SR-Java](#trans.rascal.OO.java.SR-Java)
- **Short name**: SR_Java
- **Friendly name**: Specialization ratio (Java)

Specialization ratio (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.AIF-Java-Quartiles](#trans.rascal.OO.java.AIF-Java-Quartiles)
- **Short name**: AIF_Java_Q
- **Friendly name**: Attribute inheritance factor quartiles (Java)

Attribute inheritance factor quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.AIF-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.NOC-Java-Quartiles](#trans.rascal.OO.java.NOC-Java-Quartiles)
- **Short name**: NOC_Java_Q
- **Friendly name**: Number of children quartiles (Java)

Number of children quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.NOC-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.NOC-Java](#trans.rascal.OO.java.NOC-Java)
- **Short name**: NOC_Java
- **Friendly name**: Number of children (Java)

Number of children (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.AIF-Java](#trans.rascal.OO.java.AIF-Java)
- **Short name**: AIF_Java
- **Friendly name**: Attribute inheritance factor (Java)

Attribute inheritance factor (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.RR-Java](#trans.rascal.OO.java.RR-Java)
- **Short name**: RR_Java
- **Friendly name**: Reuse ratio (Java)

Reuse ratio (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.LCC-Java-Quartiles](#trans.rascal.OO.java.LCC-Java-Quartiles)
- **Short name**: LCC_Java_Q
- **Friendly name**: Loose class cohesion quartiles (Java)

Loose class cohesion quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.LCC-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.NOA-Java](#trans.rascal.OO.java.NOA-Java)
- **Short name**: NOA_Java
- **Friendly name**: Number of attributes (Java)

Number of attributes (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.Ce-Java-Quartiles](#trans.rascal.OO.java.Ce-Java-Quartiles)
- **Short name**: Ce_Java_Q
- **Friendly name**: Efferent coupling quartiles (Java)

Efferent coupling quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.Ce-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.NOM-Java-Quartiles](#trans.rascal.OO.java.NOM-Java-Quartiles)
- **Short name**: NOM_Java_Q
- **Friendly name**: Number of methods quartiles (Java)

Number of methods quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.NOM-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.NOA-Java-Quartiles](#trans.rascal.OO.java.NOA-Java-Quartiles)
- **Short name**: NOA_Java_Q
- **Friendly name**: Number of attributes quartiles (Java)

Number of attributes quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.NOA-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.CBO-Java-Quartiles](#trans.rascal.OO.java.CBO-Java-Quartiles)
- **Short name**: CBO_Java_Q
- **Friendly name**: Coupling between objects quartiles (Java)

Coupling between objects quartiles (Java)

- <u>Depends-on</u>: `trans.rascal.OO.java.CBO-Java`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.OO.java.MPC-Java](#trans.rascal.OO.java.MPC-Java)
- **Short name**: MPC_Java
- **Friendly name**: Message passing coupling (Java)

Message passing coupling (Java)

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.LOC.java.LOCoverJavaClass](#trans.rascal.LOC.java.LOCoverJavaClass)
- **Short name**: giniLOCOverClassJava
- **Friendly name**: Distribution of physical lines of code over Java classes, interfaces and enums

The distribution of physical lines of code over Java classes, interfaces and enums explains how complexity is distributed over the design elements of a system.

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.advancedfeatures.java.AdvancedLanguageFeaturesJavaQuartiles](#trans.rascal.advancedfeatures.java.AdvancedLanguageFeaturesJavaQuartiles)
- **Short name**: countUsesOfAdvancedLanguageFeaturesQ
- **Friendly name**: Usage of advanced Java features quartiles

Quartiles of counts of advanced Java features (wildcards, union types and anonymous classes). The numbers indicate the thresholds that delimit the first 25%, 50% and 75% of the data as well as the maximum and minumum values.

- <u>Depends-on</u>: `trans.rascal.advancedfeatures.java.AdvancedLanguageFeaturesJava`
- <u>Returns</u>: `map[str, real]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.advancedfeatures.java.AdvancedLanguageFeaturesJava](#trans.rascal.advancedfeatures.java.AdvancedLanguageFeaturesJava)
- **Short name**: countUsesOfAdvancedLanguageFeatures
- **Friendly name**: Usage of advanced Java features

Usage of advanced Java features (wildcards, union types and anonymous classes), reported per file and line number of the occurrence. This metric is for downstream processing by other metrics.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc file, int count]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.CC.java.CCHistogramJava](#trans.rascal.CC.java.CCHistogramJava)
- **Short name**: CCHistogramJava
- **Friendly name**: Number of Java methods per CC risk factor

Number of Java methods per CC risk factor, counts the number of methods which are in a low, medium or high risk factor. The histogram can be compared between projects to indicate which is probably easier to maintain on a method-by-method basis.

- <u>Depends-on</u>: `trans.rascal.CC.java.CCJava`
- <u>Returns</u>: `map[str, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.CC.java.CCOverJavaMethods](#trans.rascal.CC.java.CCOverJavaMethods)
- **Short name**: giniCCOverMethodsJava
- **Friendly name**: CC over Java methods

Calculates how cyclomatic complexity is spread over the methods of a system. If high CC is localized, then this may be easily fixed but if many methods have high complexity, then the project may be at risk. This metric is good to compare between projects.

- <u>Depends-on</u>: `trans.rascal.CC.java.CCJava`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.CC.java.CCJava](#trans.rascal.CC.java.CCJava)
- **Short name**: getCC
- **Friendly name**: McCabe's Cyclomatic Complexity Metric (Java)

Cyclomatic complexity is a measure of the number of unique control flow paths in the methods of a class. This indicates how many different test cases
you would need to test the method. A high number indicates also a lot of work to understand the method.  This metric is a basic metric for further processing downstream. It is not easily compared between projects.

- <u>Depends-on</u>: - <u>Returns</u>: `map[loc, int]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.CC.java.WMCJava](#trans.rascal.CC.java.WMCJava)
- **Short name**: getWMC
- **Friendly name**: Weighted Method Count (Java)

Cyclomatic complexity is a measure of the number of unique control flow paths in the methods of a class. This indicates how many different test cases
you would need to test the method. A high number indicates also a lot of work to understand the method. The weighted method count for a class is the sum
of the cyclomatic complexity measures of all methods in the class. This metric is a basic metric for further processing downstream. It is not easily compared between projects.

- <u>Depends-on</u>: `trans.rascal.CC.java.CCJava`
- <u>Returns</u>: `map[loc class, int wmcCount]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for OSGi Dependencies](#transient-metric-providers-for-osgi-dependencies)

These metrics are related to OSGi dependencies declared in `MANIFEST.MF` files.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.numberRequiredPackagesInSourceCode](#trans.rascal.dependency.numberRequiredPackagesInSourceCode)
- **Short name**: numberRequiredPackagesInSourceCode
- **Friendly name**: Number required packages in source code

Retrieves the number of required packages found in the project source code.

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.allOSGiPackageDependencies](#trans.rascal.dependency.osgi.allOSGiPackageDependencies)
- **Short name**: allOSGiPackageDependencies
- **Friendly name**: All OSGi package dependencies

Retrieves all the OSGi package dependencies (i.e. Import-Package and DynamicImport-Package dependencies).

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.unversionedOSGiRequiredBundles](#trans.rascal.dependency.osgi.unversionedOSGiRequiredBundles)
- **Short name**: unversionedOSGiRequiredBundles
- **Friendly name**: Unversioned OSGi required bundles

Retrieves the set of unversioned OSGi required bundles (declared in the Require-Bundle header).
If returned value != {} there is a smell in the Manifest.

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.unusedOSGiImportedPackages](#trans.rascal.dependency.osgi.unusedOSGiImportedPackages)
- **Short name**: unusedOSGiImportedPackages
- **Friendly name**: Unused OSGi imported packages

Retrieves the set of unused OSGi imported packages. If set != {} then developers are importing more packages than needed (smell).

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.numberOSGiSplitImportedPackages](#trans.rascal.dependency.osgi.numberOSGiSplitImportedPackages)
- **Short name**: numberOSGiSplitImportedPackages
- **Friendly name**: Number OSGi split imported packages

Retrieves the number of split imported packages. If returned value > 0 there is a smell in the Manifest.

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.ratioUnusedOSGiImportedPackages](#trans.rascal.dependency.osgi.ratioUnusedOSGiImportedPackages)
- **Short name**: ratioUnusedOSGiImportedPackages
- **Friendly name**: Ratio of unused OSGi imported packages

Retrieves the ratio of unused OSGi imported packages with regards to the whole set of imported and dynamically imported OSGi packages.

- <u>Depends-on</u>: `trans.rascal.dependency.osgi.unusedOSGiImportedPackages`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.allOSGiBundleDependencies](#trans.rascal.dependency.osgi.allOSGiBundleDependencies)
- **Short name**: allOSGiBundleDependencies
- **Friendly name**: All OSGi bundle dependencies

Retrieves all the OSGi bunlde dependencies (i.e. Require-Bundle dependencies).

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.unversionedOSGiExportedPackages](#trans.rascal.dependency.osgi.unversionedOSGiExportedPackages)
- **Short name**: unversionedOSGiExportedPackages
- **Friendly name**: Unversioned OSGi exported packages

Retrieves the set of unversioned OSGi exported packages (declared in the Export-Package header).
If returned value != {} there is a smell in the Manifest.

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.numberOSGiSplitExportedPackages](#trans.rascal.dependency.osgi.numberOSGiSplitExportedPackages)
- **Short name**: numberOSGiSplitExportedPackages
- **Friendly name**: Number OSGi split exported packages

Retrieves the number of split exported packages. If returned value > 0 there is a smell in the Manifest.

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.allOSGiDynamicImportedPackages](#trans.rascal.dependency.osgi.allOSGiDynamicImportedPackages)
- **Short name**: allOSGiDynamicImportedPackages
- **Friendly name**: All OSGi dynamically imported packages

Retrieves all the OSGi dynamically imported packages. If returned value != {} a smell exists in the Manifest file.

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.numberOSGiBundleDependencies](#trans.rascal.dependency.osgi.numberOSGiBundleDependencies)
- **Short name**: numberOSGiBundleDependencies
- **Friendly name**: Number all OSGi bundle dependencies

Retrieves the number of OSGi bunlde dependencies (i.e. Require-Bundle dependencies).

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.ratioUnversionedOSGiImportedPackages](#trans.rascal.dependency.osgi.ratioUnversionedOSGiImportedPackages)
- **Short name**: ratioUnversionedOSGiImportedPackages
- **Friendly name**: Ratio unversioned OSGi imported packages

Retrieves the ratio of unversioned OSGi imported packages.

- <u>Depends-on</u>: `trans.rascal.dependency.osgi.unversionedOSGiImportedPackages`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.unversionedOSGiImportedPackages](#trans.rascal.dependency.osgi.unversionedOSGiImportedPackages)
- **Short name**: unversionedOSGiImportedPackages
- **Friendly name**: Unversioned OSGi imported packages

Retrieves the set of unversioned OSGi imported packages (declared in the Import-Package header).
If returned value != {} there is a smell in the Manifest.

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.numberOSGiPackageDependencies](#trans.rascal.dependency.osgi.numberOSGiPackageDependencies)
- **Short name**: numberOSGiPackageDependencies
- **Friendly name**: Number of all OSGi package dependencies

Retrieves the number of OSGi package dependencies (i.e. Import-Package and DynamicImport-Package dependencies).

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.ratioUnversionedOSGiRequiredBundles](#trans.rascal.dependency.osgi.ratioUnversionedOSGiRequiredBundles)
- **Short name**: ratioUnversionedOSGiRequiredBundles
- **Friendly name**: Ratio unversioned OSGi required bundles

Retrieves the ratio of unversioned OSGi required bundles.

- <u>Depends-on</u>: `trans.rascal.dependency.osgi.unversionedOSGiRequiredBundles`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.usedOSGiUnimportedPackages](#trans.rascal.dependency.osgi.usedOSGiUnimportedPackages)
- **Short name**: usedOSGiUnimportedPackages
- **Friendly name**: Used OSGi unimported packages

Retrieves the set of used but unimported packages. This metric does not consider packages implicitly imported through the Bundle-Require header.
If set != {} then developers may be depending on the execution environment (smell).

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.ratioUnversionedOSGiExportedPackages](#trans.rascal.dependency.osgi.ratioUnversionedOSGiExportedPackages)
- **Short name**: ratioUnversionedOSGiExportedPackages
- **Friendly name**: Ratio of unversioned OSGi exported packages

Retrieves the ratio of unversioned OSGi exported packages.

- <u>Depends-on</u>: `trans.rascal.dependency.osgi.unversionedOSGiExportedPackages`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.osgi.ratioUsedOSGiImportedPackages](#trans.rascal.dependency.osgi.ratioUsedOSGiImportedPackages)
- **Short name**: ratioUsedOSGiImportedPackages
- **Friendly name**: Ratio of used OSGi imported packages

Retrieves the ratio of used imported packages. If ratio == 0.0 all imported packages have been used in the project code.

- <u>Depends-on</u>: - <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Maven dependencies](#transient-metric-providers-for-maven-dependencies)

These metrics are related to Maven dependencies declared in `pom.xml` files.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.numberRequiredPackagesInSourceCode](#trans.rascal.dependency.numberRequiredPackagesInSourceCode)
- **Short name**: numberRequiredPackagesInSourceCode
- **Friendly name**: Number required packages in source code

Retrieves the number of required packages found in the project source code.

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.maven.ratioOptionalMavenDependencies](#trans.rascal.dependency.maven.ratioOptionalMavenDependencies)
- **Short name**: ratioOptionalMavenDependencies
- **Friendly name**: Ratio optional Maven dependencies

Retrieves the ratio of optional Maven dependencies.

- <u>Depends-on</u>: `trans.rascal.dependency.maven.allOptionalMavenDependencies`
- <u>Returns</u>: `real`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.maven.numberUniqueMavenDependencies](#trans.rascal.dependency.maven.numberUniqueMavenDependencies)
- **Short name**: numberUniqueMavenDependencies
- **Friendly name**: Number unique Maven dependencies

Retrieves the number of unique Maven dependencies.

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.maven.allOptionalMavenDependencies](#trans.rascal.dependency.maven.allOptionalMavenDependencies)
- **Short name**: allOptionalMavenDependencies
- **Friendly name**: All optional Maven dependencies

Retrieves all the optional Maven dependencies.

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.maven.isUsingTycho](#trans.rascal.dependency.maven.isUsingTycho)
- **Short name**: isUsingTycho
- **Friendly name**: Is using Tycho

Checks if the current project is a Tycho project.

- <u>Depends-on</u>: - <u>Returns</u>: `bool`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.maven.numberMavenDependencies](#trans.rascal.dependency.maven.numberMavenDependencies)
- **Short name**: numberMavenDependencies
- **Friendly name**: Number Maven dependencies

Retrieves the number of Maven dependencies.

- <u>Depends-on</u>: - <u>Returns</u>: `int`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [trans.rascal.dependency.maven.allMavenDependencies](#trans.rascal.dependency.maven.allMavenDependencies)
- **Short name**: allMavenDependencies
- **Friendly name**: All Maven dependencies

Retrieves all the Maven dependencies.

- <u>Depends-on</u>: - <u>Returns</u>: `set[loc]`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Docker Dependencies](#transient-metric-providers-for-docker-dependencies)

This metric is related to Docker dependencies declared in Dockerfiles.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.configuration.docker.dependencies](#org.eclipse.scava.metricprovider.trans.configuration.docker.dependencies)
- **Short name**: trans.configuration.docker.dependencies
- **Friendly name**: Dependencies declared in Dockerfiles

Retrieves the names of the dependencies that are declared in the Dockerfiles of a project and additional information such as their version and type.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `DockerDependency` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| dependencyName	| `String`			|
	| dependencyVersion	| `String `	|
	| type	| `String `	|
	| subType	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Puppet Dependencies](#transient-metric-providers-for-puppet-dependencies)

This metric is related to Puppet dependencies declared in Puppet manifests.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.configuration.puppet.dependencies](#org.eclipse.scava.metricprovider.trans.configuration.puppet.dependencies)
- **Short name**: trans.configuration.puppet.dependencies
- **Friendly name**: Dependencies declared in Puppet manifests

Retrieves the names of the dependencies that are declared in the Puppet manifests of a project and additional information such as their version and type.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `PuppetDependency` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| dependencyName	| `String`			|
	| dependencyVersion	| `String `	|
	| type	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Docker Smells](#transient-metric-providers-for-docker-smells)

This metric is related to Docker smells detected in Dockerfiles.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.configuration.docker.smells](#org.eclipse.scava.metricprovider.trans.configuration.docker.smells)
- **Short name**: trans.configuration.docker.smells
- **Friendly name**: Smells detected in Dockerfiles

Detects the smells in the Dockerfiles of a project and additional information such as their reason, the file and the line that each smells is detected.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `Smell` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| smellName	| `String`			|
	| reason	| `String `	|
	| code	| `String `	|
	| fileName	| `String `	|
	| line	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Puppet Smells](#transient-metric-providers-for-puppet-smells)

These metrics are related to Puppet smells detected in Puppet manifests.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.configuration.puppet.designsmells](#org.eclipse.scava.metricprovider.trans.configuration.puppet.designsmells)
- **Short name**: trans.configuration.puppet.designsmells
- **Friendly name**: Design smells detected in Puppet manifests

Detects the design smells in the Puppet manifests of a project and additional information such as their reason and the file that each smells is detected.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `Smell` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| smellName	| `String`			|
	| reason	| `String `	|
	| fileName	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.configuration.puppet.implementationsmells](#org.eclipse.scava.metricprovider.trans.configuration.puppet.implementationsmells)
- **Short name**: trans.configuration.puppet.implementationsmells
- **Friendly name**: Implementation smells detected in Puppet manifests

Detects the implementation smells in the Puppet manifests of a project and additional information such as their reason, the file and the line that each smells is detected.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `Smell` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| smellName	| `String`			|
	| reason	| `String `	|
	| fileName	| `String `	|
	| line	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Docker Antipatterns](#transient-metric-providers-for-docker-antipatterns)

This metric is related to Docker antipatterns detected in Dockerfiles.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.configuration.docker.antipatterns](#org.eclipse.scava.metricprovider.trans.configuration.docker.antipatterns)
- **Short name**: trans.configuration.docker.antipatterns
- **Friendly name**: Antipatterns detected in Dockerfiles

Detects the antipatterns in the Dockerfiles of a project and additional information such as their reason, the file and the line that each antipattern is detected and the commit and date that this antipattern is related.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `DockerAntipattern` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| smellName	| `String`			|
	| reason	| `String `	|
	| code	| `String `	|
	| fileName	| `String `	|
	| line	| `String `	|
	| commit	| `String `	|
	| date	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Puppet Antipatterns](#transient-metric-providers-for-puppet-antipatterns)

These metrics are related to Puppet antipatterns detected in Puppet manifests.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.configuration.puppet.designantipatterns](#org.eclipse.scava.metricprovider.trans.configuration.puppet.designantipatterns)
- **Short name**: trans.configuration.puppet.designantipatterns
- **Friendly name**: Design antipatterns detected in Puppet manifests

Detects the design antipatterns in the Puppet manifests of a project and additional information such as their reason, the file that each antipattern is detected and the commit and date that this antipattern is related.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `DesignAntipattern` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| smellName	| `String`			|
	| reason	| `String `	|
	| fileName	| `String `	|
	| commit	| `String `	|
	| date	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.configuration.puppet.implementationantipatterns](#org.eclipse.scava.metricprovider.trans.configuration.puppet.implementationantipatterns)
- **Short name**: trans.configuration.puppet.implementationantipatterns
- **Friendly name**: Implementation antipatterns detected in Puppet manifests

Detects the implementation antipatterns in the Puppet manifests of a project and additional information such as their reason, the file and the line that each antipattern is detected and the commit and date that this antipattern is related.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `Smell` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| smellName	| `String`			|
	| reason	| `String `	|
	| fileName	| `String `	|
	| line	| `String `	|
	| commit	| `String `	|
	| date	| `String `	|
org.eclipse.scava.metricprovider.trans.configuration.projects.relations
[<img src="./arrow_drop_up.svg">Back to top](#top)

------

## [Transient Metric Providers for Indexing](#transient-metric-providers-for-indexing)

These metrics facilitate data indexing unto the platform.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for Projects Relations](#transient-metric-providers-for-projects-relations)

This metric is related to the relations between projects that are analysed at the platform.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.configuration.projects.relations](#org.eclipse.scava.metricprovider.trans.configuration.projects.relations)
- **Short name**: trans.configuration.projects.relations
- **Friendly name**: Relations between projects

Detects the relations between projects that are already analysed at the platform by determining if a project is used as dependency by another project.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `ProjectRelation` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| relationName	| `String`			|
	| dependencyType	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for New Versions](#transient-metric-providers-for-new-versions)

These metrics are related to the new version of the dependencies of the projects that are analysed at the platform.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newversion.docker](#org.eclipse.scava.metricprovider.trans.newversion.docker)
- **Short name**: trans.newversion.docker
- **Friendly name**: New versions of Docker dependencies

Detects the new versions of dependencies of Docker based projects.

- <u>Depends-on</u>: `org.eclipse.scava.metricprovider.trans.configuration.docker.dependencies`

- <u>Returns</u>: `NewDockerVersion` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| packageName	| `String`			|
	| oldVersion	| `String `	|
	| newVersion	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newversion.puppet](#org.eclipse.scava.metricprovider.trans.newversion.puppet)
- **Short name**: trans.newversion.puppet
- **Friendly name**: New versions of Puppet dependencies

Detects the new versions of dependencies of Puppet based projects.

- <u>Depends-on</u>: `org.eclipse.scava.metricprovider.trans.configuration.puppet.dependencies`

- <u>Returns</u>: `NewPuppetVersion` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| packageName	| `String`			|
	| oldVersion	| `String `	|
	| newVersion	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newversion.osgi](#org.eclipse.scava.metricprovider.trans.newversion.osgi)
- **Short name**: trans.newversion.osgi
- **Friendly name**: New versions of OSGi dependencies

Detects the new versions of dependencies of OSGi based projects.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `NewOsgiVersion` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| packageName	| `String`			|
	| oldVersion	| `String `	|
	| newVersion	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.newversion.maven](#org.eclipse.scava.metricprovider.trans.newversion.maven)
- **Short name**: trans.newversion.maven
- **Friendly name**: New versions of Maven dependencies

Detects the new versions of dependencies of Maven based projects.

- <u>Depends-on</u>: `None`

- <u>Returns</u>: `NewMavenVersion` which contains:

	| Variable		| Type				|
	| ---------------------- | --------------------------- |
	| packageName	| `String`			|
	| oldVersion	| `String `	|
	| newVersion	| `String `	|

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.indexing.preparation](#org.eclipse.scava.metricprovider.trans.indexing.preparation)
- **Short name**: index preparation transmetric
- **Friendly name**: index preparation

This identifies the metric(s) that have been chosen to be executed by the user in preparation for indexing (note: This is required to enable the indexing capabilities of the platform to be dynamic.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`IndexPrepTransMetric` which contains:

	| Variable | Type									|
	| -------- | --------------------- |
	| executedMetricProviders		 | `List<ExecutedMetricProviders>` |

<u>*Additional Information*</u> :

- ExecutedMetricProviders :
	- `List<String>`	metricIdentifiers

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.indexing.bugs](#org.eclipse.scava.metricprovider.indexing.bugs)
- **Short name**: bug indexing metric
- **Friendly name**: bug tracking system indexer

This metric prepares and indexes documents relating to bug tracking systems.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`

- <u>Returns</u> :	`BugsIndexingMetric`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.indexing.commits](#org.eclipse.scava.metricprovider.indexing.commits)
- **Short name**: metricprovider.indexing.commits
- **Friendly name**: Commits indexer

This metric prepares and indexes documents relating to commits.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`

- <u>Returns</u> :	`CommitsIndexingMetric`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.indexing.communicationchannels](#org.eclipse.scava.metricprovider.indexing.communicationchannels)
- **Short name**: communication channels indexing metric
- **Friendly name**: communication channels indexer

This metric prepares and indexes documents relating to communication channels.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`

- <u>Returns</u> :	`CommunicationChannelsIndexingMetric`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.indexing.documentation](#org.eclipse.scava.metricprovider.indexing.documentation)
- **Short name**: metricprovider.indexing.documentation
- **Friendly name**: Documentation indexer

This metric prepares and indexes documents relating to documentation.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.indexing.preparation`, `org.eclipse.scava.metricprovider.trans.documentation`

- <u>Returns</u> :	`DocumentationIndexingMetric`

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Transient Metric Providers for API](#transient-metric-providers-for-api)

These transient metrics are related to the analysis and evolution of API

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.metricprovider.trans.migrationissuesmaracas](#org.eclipse.scava.metricprovider.trans.migrationissuesmaracas)
- **Short name**: trans.migrationissuesmaracas
- **Friendly name**: Migration Issues Detection using Maracas

This metric convert the changes found by Maracas into Regex useful for other metrics.

- <u>Depends-on</u> : `trans.rascal.api.changedMethods`

- <u>Returns</u> :	`MigrationIssueMaracasTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| maracasMeasurements		 | `List<MaracasMeasurement>` |

<u>*Additional Information*</u> :

- MaracasMeasurement :
  - `List<String>`	regex
  - `String`	change
  - `int`	lastUpdateDate


[<img src="./arrow_drop_up.svg">Back to top](#top)

------

## [Factoids](#factoids)

Factoids are plugins used to present data that has been mined and analysed using one or more historic and/or transient metric providers.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Factoids for Bug Trackers](#factoids-for-bug-trackers)

These factoids are related to bug tracking systems.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.channelusage](#org.eclipse.scava.factoid.bugs.channelusage)
- **Short name**: factoid.bugs.channelusage
- **Friendly name**: Bug Tracker Usage data

This plugin generates the factoid regarding usage data for bug trackers. For example, the total number of new bugs, comments or patches per year.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.bugs.newbugs`, `org.eclipse.scava.metricprovider.historic.bugs.comments`, `org.eclipse.scava.metricprovider.historic.bugs.patches`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*number of bugs or comments* > *working days in a year (250)*.
	- `3 star`	*2* x *number of bugs or comments* > *working days in a year (250)*.
	- `2 star`	*4* x *number of bugs or comments* > *working days in a year (250)*.
	- `1 star`	*otherwise*

- Note :
	- If the analyses is not up to a year (*365* days), the proportion of working days is used. We consider that *250* working days exist within a year.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.emotion](#org.eclipse.scava.factoid.bugs.emotion)
- **Short name**: factoid.bugs.emotion
- **Friendly name**: Bug Tracker Emotions

This plugin generates the factoid regarding emotions for bug trackers. For example, the percentage of positive, negative or surprise emotions expressed. There are 6 emotion labels (anger, fear, joy, sadness, love, surprise). Anger, fear and sadness are considered negative while joy and love are considered positive.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.bugs.newbugs`, `org.eclipse.scava.metricprovider.historic.bugs.comments`, `org.eclipse.scava.metricprovider.historic.bugs.patches`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*positive emotion percentage* > *80* OR *negative emotion percentage* < *35*.
	- `3 star`	*positive emotion percentage* > *65* OR *negative emotion percentage* < *50*.
	- `2 star`	*positive emotion percentage* > *50* OR *negative emotion percentage* < *65*.
	- `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.hourly](#org.eclipse.scava.factoid.bugs.hourly)
- **Short name**: factoid.bugs.hourly
- **Friendly name**: Bug Tracker hourly data

This plugin generates the factoid regarding hourly statistics for bug trackers. For example, the percentage of bugs, comments etc.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.hourlyrequestsreplies`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*maximum percentage of hourly comments* > *2* x *uniform percentage of comments per hour (100/24)*.
	- `3 star`	*maximum percentage of hourly comments* > *4* x *uniform percentage of comments per hour (100/24)*.
	- `2 star`	*maximum percentage of hourly comments* > *6* x *uniform percentage of comments per hour (100/24)*.
	- `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.responsetime](#org.eclipse.scava.factoid.bugs.responsetime)
- **Short name**: factoid.bugs.responsetime
- **Friendly name**: Bug Tracker Response Time

This plugin generates the factoid regarding response time for bug trackers. This could be a cummulative average, yearly average etc.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.bugs.responsetime`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*Zero(0)* < *yearly average response time* < *eight hours milliseconds (8 x 60 x 60 x 1000)*.
	- `3 star`	*Zero(0)* < *yearly average response time* < *day milliseconds (3 x eight hour milliseconds)*.
	- `2 star`	*Zero(0)* < *yearly average response time* < *week milliseconds (7 x week milliseconds)*.
	- `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.sentiment](#org.eclipse.scava.factoid.bugs.sentiment)
- **Short name**: factoid.bugs.sentiment
- **Friendly name**: Bug Tracker Sentiment

This plugin generates the factoid regarding sentiment for bug trackers. For example, the average sentiment in all bug trackers associated to a project. Sentiment score could be closer to -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment)

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.bugs.sentiment`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*average sentiment* > *0.5* OR *thread end sentiment* - *thread begining sentiment* > *0.25* AND *thread begining sentiment* > *0.15*.
	- `3 star`	*average sentiment* > *0.25* OR *thread end sentiment* - *thread begining sentiment* > *0.125* AND *thread begining sentiment* > *0.0*.
	- `2 star`	*average sentiment* > *0* OR *thread end sentiment* - *thread begining sentiment* > *0*.
	- `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.severity](#org.eclipse.scava.factoid.bugs.severity)
- **Short name**: factoid.bugs.severity
- **Friendly name**: Bug Tracker Severity

This plugin generates the factoid regarding severity for bug trackers. For example, the number of bugs per severity level, the average sentiment for each severity etc. There are 8 severity  levels (blocker, critical, major, minor, enhancement, normal, trivial, unknown). A bug severity is considered `unknown` if there is not enough information for the classifier to make a decision. Also,  `blocker`, `critical` and `major` are regarded as serious bugs.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.bugs.severity`, `org.eclipse.scava.metricprovider.historic.bugs.severitybugstatus`, `org.eclipse.scava.metricprovider.historic.bugs.severityresponsetime`, `org.eclipse.scava.metricprovider.historic.bugs.severitysentiment`

<u>*Additional Information*</u> :

- Star rating information :
  - `1 star`	*percentage of serious bugs* > *50*.
  - `2 star`	*percentage of serious bugs* > *25*.
  - `3 star`	*percentage of serious bugs* > *12.5*.
  - `4 star`	*otherwise* (i.e., fewer percentage of serious bugs).

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.size](#org.eclipse.scava.factoid.bugs.size)
- **Short name**: factoid.bugs.size
- **Friendly name**: Bug Tracker Size

This plugin generates the factoid regarding bug size for bug trackers. For example, the cumulative number of bug comments or patches.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.bugs.newbugs`, `org.eclipse.scava.metricprovider.historic.bugs.comments`, `org.eclipse.scava.metricprovider.historic.bugs.patches`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*number of bugs or parches* > *1000* OR *number of comments* > *10000*.
	- `3 star`	*2* x *number of bugs or parches* > *1000* OR *2* x *number of comments* > *10000*.
	- `2 star`	*4* x *number of bugs or parches* > *1000* OR *4* x *number of comments* > *10000*.
	- `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.status](#org.eclipse.scava.factoid.bugs.status)
- **Short name**: factoid.bugs.status
- **Friendly name**: Bug Tracker Status

This plugin generates the factoid regarding bug status for bug trackers. For example, the number of fixed bugs, duplicate bugs etc. There are 7 bug status labels (resolved, nonResolved, fixed, worksForMe, wontFix, invalid and duplicate).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.bugs.status`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*perventage of resolved bug* > *75*.
	- `3 star`	*perventage of resolved bug* > *50*.
	- `2 star`	*perventage of resolved bug* > *25*.
	- `1 star`	*otherwise* (i.e., very few resolved bugs)

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.threadlength](#org.eclipse.scava.factoid.bugs.threadlength)
- **Short name**: factoid.bugs.threadlength
- **Friendly name**: Bug Tracker Thread Length

This plugin generates the factoid regarding bug thread length for bug trackers. For example, the average length of discussion associated to bugs.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.bugs.bugs`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*Zero(0)* < *average comments* < *5*.
	- `3 star`	*Zero(0)* < *average comments* < *10*.
	- `2 star`	*Zero(0)* < *average comments* < *20*.
	- `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.users](#org.eclipse.scava.factoid.bugs.users)
- **Short name**: factoid.bugs.users
- **Friendly name**: Bug Tracker Users

This plugin generates the factoid regarding users for bug trackers. For example, the average number of users associated to a project in a bug tracking system.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.bugs.users`, `org.eclipse.scava.metricprovider.historic.bugs.bugs`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*daily new users in last month* > *8* x *0.25* OR *daily active users in last month* > *8* x *2.5* OR *daily new users in last year* > *4* x *0.25* OR daily active users in last year* > *4* x *2.5*.
	- `3 star`	*daily new users in last month* > *4* x *0.25* OR *daily active users in last month* > *4* x *2.5* OR *daily new users in last year* > *2* x *0.25* OR daily active users in last year* > *2* x *2.5*.
	- `2 star`	*daily new users in last month* > *2* x *0.25* OR *daily active users in last month* > *2* x *2.5* OR *daily new users in last year* > *0.25* OR *daily active users in last year* > *2.5*.
	- `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.bugs.weekly](#org.eclipse.scava.factoid.bugs.weekly)
- **Short name**: factoid.bugs.weekly
- **Friendly name**: Bug Tracker Weekly

This plugin generates the factoid regarding weekly user engagements for bug trackers. For example, the average number of bug comments per week. This can be used to present the most and least busy week in terms of engagement for a particular project.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.dailyrequestsreplies`

<u>*Additional Information*</u> :

- Star rating information :
	- `4 star`	*maximum percentage of weekly comments* < *2* x *uniform percentage of comments per week (100/7)*.
	- `3 star`	*maximum percentage of weekly comments* < *3* x *uniform percentage of comments per week (100/7)*.
	- `2 star`	*maximum percentage of weekly comments* < *4* x *uniform percentage of comments per week (100/7)*.
	- `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Factoids for Newsgroups and Forums](#factoids-for-newsgroups-and-forums)

These factoids are related to communication channels.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.channelusage](#org.eclipse.scava.factoid.newsgroups.channelusage)

- **Short name**: factoid.newsgroups.channelusage
- **Friendly name**: Newsgroup Channel Usage

This plugin generates the factoid regarding usage data for newsgroups. For example, the total number of new articles or threads per year.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.newsgroups.articles`, `org.eclipse.scava.metricprovider.historic.newsgroups.newthreads`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*number of articles* OR *threads* > *working days in a year (250*).
  - `3 star`	*2* x *number of articles* OR *threads* > *working days in a year (250)*.
  - `2 star`	*4* x *number of articles* OR *threads* > *working days in a year (250)*.
  - `1 star`	*otherwise*

- Note :
	- If the analyses is not up to a year (*365* days), the proportion of working days is used. We consider that *250* working days exist within a year.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.emotion](#org.eclipse.scava.factoid.newsgroups.emotion)

- **Short name**: factoid.newsgroups.emotion
- **Friendly name**: Newsgroup Channel Emotion

This plugin generates the factoid regarding emotions for newsgroups, such as the percentage of positive, negative or surprise emotions expressed. There are 6 emotion labels (anger, fear, joy, sadness, love, surprise). Anger, fear and sadness are considered negative while joy and love are considered positive.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.emotions`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*positive emotion percentage* > *80* OR *negative emotion percentage* < *35*.
  - `3 star`	*positive emotion percentage* > *65* OR *negative emotion percentage* < *50*.
  - `2 star`	*positive emotion percentage* > *50* OR *negative emotion percentage* < *65*.
  - `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.hourly](#org.eclipse.scava.factoid.newsgroups.hourly)

- **Short name**: factoid.newsgroups.hourly
- **Friendly name**: Newsgroup Channel hourly data

This plugin generates the factoid regarding hourly data for newsgroups, such as the percentage of articles, threads etc.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.hourlyrequestsreplies`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*maximum percentage of hourly articles* > *2* x *uniform percentage of articles per hour (100/24)*.
  - `3 star`	*maximum percentage of hourly articles* > *4* x *uniform percentage of articles per hour (100/24)*.
  - `2 star`	*maximum percentage of hourly articles* > *6* x *uniform percentage of articles per hour (100/24)*.
  - `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.responsetime](#org.eclipse.scava.factoid.newsgroups.responsetime)

- **Short name**: factoid.newsgroups.responsetime
- **Friendly name**: Newsgroup Channel Response Time

This plugin generates the factoid regarding response time for newsgroups. This could be a cummulative average, yearly average etc.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.newsgroups.responsetime`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*Zero(0)* < *yearly average response time* < *eight hours in milliseconds (8 x 60 x 60 x 1000)*.
  - `3 star`	*Zero(0)* < *yearly average response time* < *day in milliseconds (3 x eight hours in milliseconds)*.
  - `2 star`	*Zero(0)* < *yearly average response time* < *week in milliseconds (7 x day in milliseconds)*.
  - `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.sentiment](#org.eclipse.scava.factoid.newsgroups.sentiment)

- **Short name**: factoid.newsgroups.sentiment
- **Friendly name**: Newsgroup Channel Sentiment

This plugin generates the factoid regarding sentiments for newsgroups. For example, the average sentiment in all newsgroup channel associated to a project. Sentiment score could be closer to -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment)

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.newsgroups.sentiment`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*average sentiment* > *0.5* OR *thread end sentiment* - *thread begining sentiment* > *0.25* AND *thread begining sentiment* > *0.15*.
  - `3 star`	*average sentiment* > *0.25* OR *thread end sentiment* - *thread begining sentiment* > *0.125* AND *thread begining sentiment* > *0.0*.
  - `2 star`	*average sentiment* > *0* OR *thread end sentiment* - *thread begining sentiment* > *0*.
  - `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.severity](#org.eclipse.scava.factoid.newsgroups.severity)

- **Short name**: factoid.newsgroups.severity
- **Friendly name**: Newsgroup Channel Severity

This plugin generates the factoid regarding severity for newsgroups. For example, the number of articles per severity level, the average sentiment for each severity etc. There are 7 severity  levels (blocker, critical, major, minor, enhancement, normal, trivial). Note:  `blocker`, `critical` and `major` are regarded as serious bugs.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.newsgroups.severityresponsetime`, `org.eclipse.scava.metricprovider.historic.newsgroups.severity`, `org.eclipse.scava.metricprovider.historic.newsgroups.severitysentiment`

<u>*Additional Information*</u> :

- Star rating information :
  - `1 star`	*percentage of serious bugs* > *50*.
  - `2 star`	*percentage of serious bugs* > *25*.
  - `3 star`	*percentage of serious bugs* > *12.5*.
  - `4 star`	*otherwise* (i.e., fewer percentage of serious bugs).

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.size](#org.eclipse.scava.factoid.newsgroups.size)

- **Short name**: factoid.newsgroups.size
- **Friendly name**: Newsgroup Channel Size

This plugin generates the factoid regarding thread or article size for newsgroups. For example, the cummulative number of threads.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.newsgroups.articles`, `org.eclipse.scava.metricprovider.historic.newsgroups.newthreads`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*number of threads* > *1000* OR *number of articles* > *10000*.
  - `3 star`	*2* x *number of threads* > *1000* OR *2* x *number of articles* > *10000*.
  - `2 star`	*4* x *number of threads* > *1000* OR *4* x *number of articles* > *10000*.
  - `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.status](#org.eclipse.scava.factoid.newsgroups.status)

- **Short name**: factoid.newsgroups.status
- **Friendly name**: Newsgroup Channel Status

This plugin generates the factoid regarding thread or article status for newsgroups. For example, the number of requests and replies, unanswered threads etc.  

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.newsgroups.unansweredthreads`, `org.eclipse.scava.metricprovider.historic.newsgroups.requestsreplies`, `org.eclipse.scava.metricprovider.historic.newsgroups.requestsreplies.average`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*perventage of replies* > *75*.
  - `3 star`	*perventage of replies* > *50*.
  - `2 star`	*perventage of replies* > *25*.
  - `1 star`	*otherwise* (i.e., very few replies)

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.threadlength](#org.eclipse.scava.factoid.newsgroups.threadlength)

- **Short name**: factoid.newsgroups.threadlength
- **Friendly name**: Newsgroup Channel Thread Length

This plugin generates the factoid regarding thread length for newsgroups. For example, the average length of discussion per day, month etc.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.newsgroups.threads`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*Zero(0)* < *average comments* < *5*.
  - `3 star`	*Zero(0)* < *average comments* < *10*.
  - `2 star`	*Zero(0)* < *average comments* < *20*.
  - `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.users](#org.eclipse.scava.factoid.newsgroups.users)

- **Short name**: factoid.newsgroups.users
- **Friendly name**: Newsgroup Channel Users

This plugin generates the factoid regarding users for newsgroups. For example, the average number of users associated to a project in a newsgroup channel.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.newsgroups.users`, `org.eclipse.scava.metricprovider.historic.newsgroups.threads`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*daily new users in last month* > *8* x *0.25* OR *daily active users in last month* > *8* x *2.5* OR *daily new users in last year* > *4* x *0.25* OR *daily active users in last year* > *4* x *2.5*.
  - `3 star`	*daily new users in last month* > *4* x *0.25* OR *daily active users in last month* > *4* x *2.5* OR *daily new users in last year* > *2* x *0.25* OR *daily active users in last year* > *2* x *2.5*.
  - `2 star`	*daily new users in last month* > *2* x *0.25* OR *daily active users in last month > 2 x 2.5* OR *daily new users in last year* > *0.25* OR *daily active users in last year* > *2.5*.
  - `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.newsgroups.weekly](#org.eclipse.scava.factoid.newsgroups.weekly)

- **Short name**: factoid.newsgroups.weekly
- **Friendly name**: Newsgroup Channel Weekly

This plugin generates the factoid regarding weekly user engagement for newsgroups. For example, the average number of comments per week. This can be used to present the most and least busy week in terms of engagement for a particular project.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.dailyrequestsreplies`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*maximum percentage of weekly articles* < *2* x *uniform percentage of articles per week (100/7)*.
  - `3 star`	*maximum percentage of weekly articles* < *3* x *uniform percentage of articles per week (100/7)*.
  - `2 star`	*maximum percentage of weekly articles* < *4* x *uniform percentage of articles per week (100/7)*.
  - `1 star`	*otherwise*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

### [Factoids for Documentation](#factoids-for-documentation)

These factoids are related to documentation.

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.documentation.entries](#org.eclipse.scava.factoid.documentation.entries)

- **Short name**: factoid.documentation.entries
- **Friendly name**: Documentation Entries

This plugin generates the factoid regarding which sections have been found and which are missing in the documentation. This can help understanding which sections should be added or better indicated to have a better documentation.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.documentation.classification`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*All five types of documentation sections have been found*.
  - `3 star`	*Three or four types of documentation sections have been found*.
  - `2 star`	*Two or one types of documentation sections have been found*.
  - `1 star`	*No sections have been found*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------

#### [org.eclipse.scava.factoid.documentation.sentiment](#org.eclipse.scava.factoid.documentation.sentiment)

- **Short name**: factoid.documentation.sentiment
- **Friendly name**: Documentation Sentiment

This plugin generates the factoid regarding sentiment for documentation.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.historic.documentation.sentiment.DocumentationSentimentHistoricMetricProvider`

<u>*Additional Information*</u> :

- Star rating information :
  - `4 star`	*Average sentiment greater than 0.5*.
  - `3 star`	*Average sentiment between 0.25 and 0.5*.
  - `2 star`	*Average sentiment between 0 and 0.25*.
  - `1 star`	*Average sentiment equal or lesser than 0*

[<img src="./arrow_drop_up.svg">Back to top](#top)

------
