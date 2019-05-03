# Metrics Reference Guide

This guide contains the historic and trans metric providers for for bug trackers and newsgroups (including eclipse forum).

## Historic Metric Providers

Historic metrics maintain a record of various heuristics associated with a specific open source project over its lifetime. They typically depend on the results from one or more transient metrics.

### Bug Trackers

The following Historic Metric Providers are associated with Issue trackers

------

#### org.eclipse.scava.metricprovider.historic.bugs.bugs
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.comments
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.emotions
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.newbugs
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.newusers
- **Short name**: historic.bugs.newusers
- **Friendly name**: Number of new users per day per bug tracker

This metric computes the number of new users per day  for each bug tracker seperately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.activeusers`

- <u>Returns</u> :	`BugsNewUsersHistoricMetric` which contains:

	| Variable									 | Type												|
	| -------------------------- | --------------------------- |
	| bugTrackers								| `List<DailyBugTrackerData>` |
	| numberOfNewUsers					 | `int`											 |
	| cumulativeNumberOfNewUsers | `int`											 |

<u>*Additional Information*</u> :	

- DailyBugTrackerData : 
	- `String`	bugTrackerId
	- `int`	numberOfNewUsers
	- `int` 	cumulativeNumberOfNewUsers

------
#### org.eclipse.scava.metricprovider.historic.bugs.opentime
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

------
#### org.eclipse.scava.metricprovider.historic.bugs.patches
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

------
#### org.eclipse.scava.metricprovider.historic.bugs.requestsreplies
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.requestsreplies.average
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.responsetime
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.sentiment
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

<u>*Additional Information*</u> :	

- The sentiment related variables above all represent a <u>***Polarity***</u> value. A polarity value closer to: <u>-1</u> indicates negative sentiment, closer to <u>0</u> indicates neutral sentiment and closer to <u>1</u> indicates positive sentiment.

------

#### org.eclipse.scava.metricprovider.historic.bugs.severity
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.severitybugstatus
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.severityresponsetime
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.severitysentiment
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


- The sentiment related variables above all represent a <u>***Polarity***</u> value. A polarity value closer to: <u>-1</u> indicates negative sentiment, closer to <u>0</u> indicates neutral sentiment and closer to <u>1</u> indicates positive sentiment.

------

#### org.eclipse.scava.metricprovider.historic.bugs.status
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

------

#### org.eclipse.scava.metricprovider.historic.bugs.topics
- **Short name**: historic.bugs.topics
- **Friendly name**: Labels of topics in bug comments per bug tracker 

This metric computes the labels of topics (thematic clusters) in bug comments submitted by the community (users), per bug tracker.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.topics` 

- <u>Returns</u> :	`BugsTopicsHistoricMetric` which contains:

	| Variable	| Type						 |
	| --------- | ---------------- |
	| bugTopics | `List<BugTopic>` |

<u>*Additional Information*</u> :	

- SeverityLevel : 
	- `String`	bugTrackerId
	- `String`	label
	- `float`	numberOfDocuments

------

#### org.eclipse.scava.metricprovider.historic.bugs.unansweredbugs
- **Short name**: historic.bugs.unansweredbugs
- **Friendly name**: Number of unanswered bugs per day 

This metric computes the number of unanswered bugs per day.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.bugs.requestsreplies`

- <u>Returns</u> :	`BugsUnansweredBugsHistoricMetric` which contains:

	| Variable							 | Type	|
	| ---------------------- | ----- |
	| numberOfUnansweredBugs | `int` |

------

#### org.eclipse.scava.metricprovider.historic.bugs.users
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

------

### News Groups and Forums

The following Historic Metric Providers are associated with newsgroups.

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.articles
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
	
------

#### org.eclipse.scava.metricprovider.historic.newsgroups.emotions
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
	
------

#### org.eclipse.scava.metricprovider.historic.newsgroups.newthreads
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

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.newusers
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

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.requestsreplies
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

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.requestsreplies.average
- **Short name**: historic.newsgroups.requestsreplies.average
- **Friendly name**: Average number of articles, requests and replies per day 

This metric computes the average number of newsgroup articles, including the number of requests and replies within the newsgroup articles per day.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.activeusers`

- <u>Returns</u> :	`NewsgroupsRequestsRepliesHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| averageArticlesPerDay		 | `float` |
	| averageRequestsPerDay		 | `float` |
	| averageRepliesPerDay		 | `float` |

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.responsetime
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

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.sentiment
- **Short name**: historic.newsgroups.sentiment
- **Friendly name**: Overall sentiment of newsgroup articles 

This metric computes the overall sentiment per newsgroup repository up to the processing date. The overall sentiment score could be -1 (negative sentiment), 0 (neutral sentiment) or +1 (positive sentiment). In the computation, the sentiment score of each thread contributes equally, irrespective of its size. 

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.sentiment`

- <u>Returns</u> :	`SentimentClassificationTransMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| overallAverageSentiment		 | `float` |
	| overallSentimentAtThreadBegining		 | `float` |
	| overallSentimentAtThreadEnd		 | `float` |

- The sentiment related variables above all represent a <u>***Polarity***</u> value. A polarity value closer to: <u>-1</u> indicates negative sentiment, closer to <u>0</u> indicates neutral sentiment and closer to <u>1</u> indicates positive sentiment.

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.severity
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

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.severityresponsetime
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

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.severitysentiment
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

- The sentiment related variables above all represent a <u>***Polarity***</u> value. A polarity value closer to: <u>-1</u> indicates negative sentiment, closer to <u>0</u> indicates neutral sentiment and closer to <u>1</u> indicates positive sentiment.

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.threads
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

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.topics
- **Short name**: historic.newsgroups.topics
- **Friendly name**: Labels of newsgroup topics per newsgroup

This metric computes the labels of topics (thematic clusters) in articles submitted by the community (users), for each newsgroup seperately.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.topics`

- <u>Returns</u> :	`NewsgroupTopicsHistoricMetric` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| newsgroupTopic		 | `List<NewsgrpTopic>` |

<u>*Additional Information*</u> :	

- NewsgroupTopic : 
	- `String`	newsgroupName
	- `String`	label
	- `int`	numberOfDocuments

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.unansweredthreads
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

------

#### org.eclipse.scava.metricprovider.historic.newsgroups.users
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

------


## Transient Metric Providers

Transient metrics are used to calculate heuristics that are associated with a particular period in time, i.e. a single day. Transient Metrics are stored temporarily within the knowledge base and their output is passed as parameters in the calculation of other transient and historic metrics. Depending on the complexity, a transient metric can depend on the output from other tools, other transient metircs or have no dependencies at all.

### Bug Trackers

The following Transient Metric Providers are associated with Issue trackers.

------

#### org.eclipse.scava.metricprovider.trans.bugs.activeusers
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

------

#### org.eclipse.scava.metricprovider.trans.bugs.bugmetadata
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
	- `String`	resolution
	- `String`	operatingSystem
	- `String`	priority
	- `String`	creationTime
	- `String`	lastClosedTime
	- `String`	startSentiment
	- `String`	endSentiment
	- `float`	averageSentiment
- CommentData : 
	- `String`	bugTrackerId
	- `String`	bugId
	-	`String`	commentId
	-	`String`	creationTime
	-	`String`	creator
	-	`String`	contentClass
	-	`String`	requestReplyPrediction

------

#### org.eclipse.scava.metricprovider.trans.bugs.comments
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

------

#### org.eclipse.scava.metricprovider.trans.bugs.contentclasses
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

------

#### org.eclipse.scava.metricprovider.trans.bugs.dailyrequestsreplies
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

------

#### org.eclipse.scava.metricprovider.trans.bugs.emotions
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
	- `String`	emotionLabel (`anger`, `fear`, `joy`, `sadness`, `love`, surprise`)
	- `int`	numberOfComments
	- `int`	cumulativeNumberOfComments
	- `float`	percentage
	- `float`	cumulativePercentage

------

#### org.eclipse.scava.metricprovider.trans.bugs.hourlyrequestsreplies
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
	- `type`	bugTrackerId
	- `type`	hour
	- `type`	numberOfComments
	- `type`	numberOfRequests
	- `type`	numberOfReplies
	- `type`	percentageOfComments
	- `type`	percentageOfRequests
	- `type`	percentageOfReplies

------

#### org.eclipse.scava.metricprovider.trans.bugs.newbugs
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

------
#### org.eclipse.scava.metricprovider.trans.bugs.patches
- **Short name**: trans.bugs.patches
- **Friendly name**: Number of patches per bug

This metric computes the number of patches submitted by the community (users) for each bug.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`PatchesTransMetricProvider` which contains:

	| Variable			 | Type	 |
	| -------------- | ------ |
	| bugTrackerData | `type` |

<u>*Additional Information*</u> :	

- BugTrackerData : 
	- `String`	bugTrackerId
	- `int`	numberOfPatches
	- `int`	cumulativeNumberOfPatches

------

#### org.eclipse.scava.metricprovider.trans.bugs.references
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
	
	
------

#### org.eclipse.scava.metricprovider.trans.bugs.requestsreplies
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

------

### Commits

------

#### org.eclipse.scava.metricprovider.trans.commits.messagereferences
- **Short name**: trans.commits.messagereferences
- **Friendly name**: Commits Messages References

This metrics search for references of commits or bugs within the messages of commits. In order to work, it is necessary to use at the same time one Bug Tracker, as the retrieval of references are based on patterns defined by bug trackers. If multiple or zero Bug Trackers are defined in the project, then this metric do not run.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`CommitsMessageReferenceTransMetric` which contains:

	| Variable | Type									|
	| -------- | --------------------- |
	| bugs		 | `List<CommitMessageReferringTo>` |

<u>*Additional Information*</u> :	

- BugReferringTo : 
	- `String`	repository (URL)
	- `String`	revision (Commit SHA)
	- `List<String>`	bugsReferred 	(URLs)
	- `List<String>`	commitsReferred (URLs)

<u>*Note*</u> :
	When this metric is used on GitHub, it should be noted that some references of bugs will be in fact pull requests. The reason is that GitHub considers pull requests equally as issues.
	

------

### Communication Channels (newsgroups and forums)

The following Transient Metric Providers are associated with communication channels in general, either newsgroups or forums.
Despite the name of the metrics are newsgroups, all the metrics are valid for communication channels.

------

#### org.eclipse.scava.metricprovider.trans.newsgroups.activeusers 
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

------

#### org.eclipse.scava.metricprovider.trans.newsgroups.articles
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

------

#### org.eclipse.scava.metricprovider.trans.newsgroups.contentclasses
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

------

#### org.eclipse.scava.metricprovider.trans.newsgroups.dailyrequestsreplies
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

------

#### org.eclipse.scava.metricprovider.trans.newsgroups.emotions
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
	- `String`	emotionLabel (`anger`, `fear`, `joy`, `sadness`, `love`, surprise`)
	- `int`	numberOfArticles
	- `int`	cumulativeNumberOfArticles
	- `float`	percentage
	- `float`	cumulativePercentage
	
------

#### org.eclipse.scava.metricprovider.trans.newsgroups.hourlyrequestsreplies
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
	
------

#### org.eclipse.scava.metricprovider.trans.newsgroups.sentiment
- **Short name**: trans.newsgroups.sentiment
- **Friendly name**: Average sentiment in newsgroup threads

The metric computes the average sentiment, including sentiment at the beginning and end of each thread, per newsgroup.

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

- The sentiment related variables above all represent a <u>***Polarity***</u> value.	A polarity value closer to:	<u>-1</u> indicates negative sentiment, closer to <u>0</u> indicates neutral sentiment and closer to <u>1</u> indicates positive sentiment.
	
	------

#### org.eclipse.scava.metricprovider.trans.newsgroups.threads
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
	
------

#### org.eclipse.scava.metricprovider.trans.newsgroups.threadsrequestsreplies
- **Short name**: trans.newsgroups.threadsrequestsreplies
- **Friendly name**: Thread statistics (answered?, response time)

The metric computes for each thread whether it is answered. If so, it computes the response time.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.newsgroups.threads`, `org.eclipse.scava.metricprovider.trans.requestreplyclassification`

- <u>Returns</u> :	`NewsgroupsSentimentTransMetric` which contains:

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
	

------

### Natural Language Processing

The following Transient Metric Providers are associated with Natural Language Processing tools.

------
#### org.eclipse.scava.metricprovider.trans.detectingcode
- **Short name**: trans.detectingcode
- **Friendly name**: Distinguishes between code and natural language

This metric determines the parts of a bug comment or a newsgroup article that contains code or natural language.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.plaintextprocessing`

- <u>Returns</u> :	`DetectingCodeTransMetricProvider` which contains:

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
	
------
#### org.eclipse.scava.metricprovider.trans.emotionclassification
- **Short name**: trans.emotionclassification
- **Friendly name**: Emotion classifier

This metric computes the emotions present in each bug comment, newsgroup article or forum post. There are 6 emotion labels (anger, fear, joy, sadness, love, surprise).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.detectingcode`

- <u>Returns</u> :	`EmotionClassificationTransMetricProvider` which contains:

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
	
------
#### org.eclipse.scava.metricprovider.trans.plaintextprocessing
- **Short name**: trans.plaintextprocessing
- **Friendly name**: Plain text processing

This metric preprocess each bug comment, newsgroup article or forum post into a split plain text format.

- <u>Depends-on</u> : `None`

- <u>Returns</u> :	`PlainTextProcessingTransMetricProvider` which contains:

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

------
#### org.eclipse.scava.metricprovider.trans.requestreplyclassification
- **Short name**: trans.requestreplyclassification
- **Friendly name**: Request/Reply classification

This metric computes if a bug comment, newsgroup article or forum post is a request of a reply.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.plaintextprocessing`, `org.eclipse.scava.metricprovider.trans.detectingcode`

- <u>Returns</u> :	`RequestReplyClassificationTransMetricProvider` which contains:

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

------
#### org.eclipse.scava.metricprovider.trans.sentimentclassification
- **Short name**: trans.sentimentclassification
- **Friendly name**: Sentiment classification

This metric computes the sentiment of each bug comment, newsgroup article or forum post. Sentiment can be -1 (negative sentiment), 0 (neutral sentiment) or 1 (positive sentiment).

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.detectingcode`

- <u>Returns</u> :	`SentimentClassificationTransMetricProvider` which contains:

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

------
#### org.eclipse.scava.metricprovider.trans.severityclassification
- **Short name**: trans.severityclassification
- **Friendly name**: Severity classification

This metric computes the severity of each bug comment, newsgroup article or forum post. Severity could be blocker, critical, major, minor, enhancement,  normal). For bug comments, there is an additional severity level called `unknown`. A bug severity is considered `unknown` if there is not enough information for the classifier to make a decision. For example, an unanswered bug with no user comment to analyse. 

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.detectingcode`, `org.eclipse.scava.metricprovider.trans.newsgroups.threads`

- <u>Returns</u> :	`SeverityClassificationTransMetricProvider` which contains:

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

------
#### org.eclipse.scava.metricprovider.trans.topics
- **Short name**: trans.topics
- **Friendly name**: Topic clustering

This metric computes topic clusters for each bug comment, newsgroup article or forum post in the last 30 days.

- <u>Depends-on</u> : `org.eclipse.scava.metricprovider.trans.detectingcode`

- <u>Returns</u> :	`TopicsTransMetricProvider` which contains:

	| Variable | Type	 |
	| -------- | ------ |
	| bugTrackerComments		 | `List<BugTrackerCommentsData>` |
	| bugTrackerTopics		 | `List<BugTrackerTopic>` |
	| newsgroupArticles		 | `List<NewsgroupArticlesData>` |
	| newsgroupTopics		 | `List<NewsgroupTopic>` |
	| forumPosts		 | `List<ForumPostData>` |
	| forumTopics		 | `List<ForumPostTopic>` |

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

- ForumPostData : 
  - `String`	forumId
  - `String`	topicId
  - `String`	postId
  - `String`	subject
  - `String`	text
  - `String`	date

- BugTrackerTopic : 
  - `String`	bugTrackerId
  - `String`	label
  - `int`	numberOfDocuments

- NewsgroupTopic : 
  - `String`	newsgroupName
  - `String`	label
  - `int`	numberOfDocuments

- ForumPostTopic : 
  - `String`	forumId
  - `String`	label
  - `int`	numberOfDocuments

------