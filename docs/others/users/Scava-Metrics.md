
# Metrics computed by Scava 

## Metric-platform

**OSGi metrics** are defined in:

* https://github.com/crossminer/scava/blob/master/metric-platform/metric-providers/org.eclipse.scava.metricprovider.trans.rascal.dependency.osgi/src/OSGi.rsc

List of metrics:

* allOSGiBundleDependencies -- Retrieves all the OSGi bunlde dependencies (i.e. Require-Bundle dependencies).
* allOSGiPackageDependencies -- Retrieves all the OSGi package dependencies (i.e. Import-Package and DynamicImport-Package dependencies).
* allOSGiDynamicImportedPackages -- Retrieves all the OSGi dynamically imported packages. If returned value != {} a smell exists in the Manifest file.
* numberOSGiPackageDependencies -- Retrieves the number of OSGi package dependencies (i.e. Import-Package and DynamicImport-Package dependencies).
* numberOSGiBundleDependencies -- Retrieves the number of OSGi bunlde dependencies (i.e. Require-Bundle dependencies).
* unusedOSGiImportedPackages -- Retrieves the set of unused OSGi imported packages. If set != {} then developers are importing more packages than needed (smell).
* ratioUnusedOSGiImportedPackages -- Retrieves the ratio of unused OSGi imported packages with regards to the whole set of imported and dynamically imported OSGi packages.
* ratioUsedOSGiImportedPackages -- Retrieves the ratio of used imported packages. If ratio == 0.0 all imported packages have been used in the project code.
* numberOSGiSplitImportedPackages -- Retrieves the number of split imported packages. If returned value > 0 there is a smell in the Manifest.
* numberOSGiSplitExportedPackages -- Retrieves the number of split exported packages. If returned value > 0 there is a smell in the Manifest..
* unversionedOSGiRequiredBundles -- Retrieves the set of unversioned OSGi required bundles (declared in the Require-Bundle header.
* ratioUnversionedOSGiRequiredBundles -- Retrieves the ratio of unversioned OSGi required bundles.
* unversionedOSGiImportedPackages -- Retrieves the set of unversioned OSGi imported packages (declared in the Import-Package header). If returned value != {} there is a smell in the Manifest.
* ratioUnversionedOSGiImportedPackages -- Retrieves the ratio of unversioned OSGi imported packages.
* unversionedOSGiExportedPackages -- Retrieves the set of unversioned OSGi exported packages (declared in the Export-Package header). If returned value != {} there is a smell in the Manifest.
* ratioUnversionedOSGiExportedPackages -- Retrieves the ratio of unversioned OSGi exported packages.

**Maven metrics** are defined in 

* https://github.com/crossminer/scava/blob/master/metric-platform/metric-providers/org.eclipse.scava.metricprovider.trans.rascal.dependency.maven/src/Maven.rsc

List of metrics: 

* allMavenDependencies -- Retrieves all the Maven dependencies.
* allOptionalMavenDependencies -- Retrieves all the optional Maven dependencies.
* numberMavenDependencies -- Retrieves the number of Maven dependencies.
* numberUniqueMavenDependencies -- Retrieves the number of unique Maven dependencies.
* ratioOptionalMavenDependencies -- Retrieves the ratio of optional Maven dependencies.
* isUsingTycho -- Checks if the current project is a Tycho project.


## IDE plugin

All metrics are defined in [metrics_definition_ide_plugin.docx](/resources/metrics_definition_ide_plugin.docx)

* scava-lib-usage -- Level of using CROSSMINER library change function.
* scava-search-usage -- Level of using CROSSMINER search function.
* scava-search-success -- Level of successfull free text serach using CROSSMINER plug-in.
* modifictaion-rate -- Rate of changes applied to document.
* gui-usage-rate -- Rate of activly using the GUI of Eclipse.
* testing-rate -- Count of executing tests.
* working-time -- Average working time for Java source files.
* file-access-rate -- Average count of Java source files open and brought to top.


## Natural Language Processing

All metrics are defined in [metrics_definition_nlp.docx](/resources/metrics_definition_nlp.docx).

**Issue tracking** metrics:

* Number of bugs: It indicates how many bugs, through the time, are in total all the issue tracking systems related to a project.
* Number of comments: This metric indicates, through the time, the evolution in the quantity of comments for all the bugs related to a project.
* Emotions: This metric expresses, grosso modo, the emotions found in the issue tracker for a given project.
* Number new bugs: It indicates how many bugs are created every delta through a lapse of time.
* Number of new users: How many users are new in the bug tracking system.
* Open time: This metric shows the average open time of an issue.
* Number of patches: It indicates the number of patches located in the issue tracking system.
* Number of request and replies: From all the comments in the issue tracking system, how many of them are replies and how many are requests.
* Response time: It presents the average time to reply a comment in an issue tracker.
* Sentiments: Which sentiments are found in a issue tracking system for a project.
* Severity: The severity level of the bugs found in the issue tracker. This metric classifies a bug report into 1 of 7 severity levels such as Blocker, Critical, Major, Normal, Minor, Trivial or Enhancement.
* Status: It indicates the issues status, like open or closed.
* Topics: Using clustering methods, this metric indicates the topics that are discussed through the time.
* Unasnwered bugs: It indicates how many issues do not have any reply.
* Users: How many users are found in a issue tracker system.

**Newsgroup** metrics

* Number of articles; It determines the number of articles found in a newsgroup.
* Emotions: Which emotions are found in the newgroup.
* Number of threads: How many threads a newsgroup contains. In other words, how many different branches have been created since the first email was sent to the newsgroup.
* Number of new users: How many users make use of the newsgroup.
* Number of request and replies: From the total number of emails belonging to the newsgroup, how many of them are request and how many are replies.
* Response time: The average time to reply a message.
* Sentiments: The sentiments found in the newsgroup.
* Severity: The severity level of the messages exchanges in the newsgroup. The severity is measured in terms of how severe an issue is.
* Number of new threads: How many threads are created per delta.
* Topics: Using the clustering algorithm, we determine which are the most frequent topics discussed in the newsgroup.
* Number of unanswered topics: How many messages haven’t been answered.
* Number of users: Number of users that make use of the newsgroup.

**Forums** metrics

* Number of posts: For every topic (i.e. forum thread), how many posts in total exist.
* Emotions: Which are the emotions located in the forum.
* Number of topics: How many forum threads contain the forum.
* Number of request and replies: From all the posts in the forum, how many are request and how many are reply.
* Sentiments: Which are the sentiments that can be found in a forum.
* Severity: In the case the forums are used to express issues, we can determine their severity.
* Number of new topics: Number of new forum threads created.
* Topics: Number of content topics, i.e. subjects, are discussed in the forum. 
* Number of unanswered topics: Number of forums threads which do not have a reply.


## Configuration analysis metrics

Metrics of Puppet are defined in detail in [Deliverable 4.2](https://github.com/crossminer/internal-material/blob/master/Workpackages/WP4/D4.2/D4.2.docx).

**Puppet Design** Metrics:

* numberOfMultifacetedSmells --  The number of Multifaceted Abstraction smells
* numberOfUnnecessarySmells -- The number of Unnecessary Abstraction smells
* numberOfImperativeSmells -- The number of Imperative Abstraction smells
* numberOfMissAbSmells -- The number of Missing Abstraction smells
* numberOfInsufficientSmells -- The number of Insufficient Modularization smells
* numberOfUnstructuredSmells -- The number of Unstructured Module smells
* numberOfTightSmells -- The number of Tightly-coupled Module smells
* numberOfBrokenSmells -- The number of Broken Hierarchy smells
* numberOfMissingDepSmells -- The number of Missing Dependency smells
* numberOfHairballSmells -- The number of Hairball Structure smells
* numberOfDeficientSmells -- The number of Deficient Encapsulation smells
* numberOfWeakenSmells -- The number of Weaken Modularity smells
* cumulativeNumberOfDesignSmells -- The number of design smells

**Puppet Implementation** Metrics:

* numberOfMissingDefaultCaseSmells -- Smell exists when a default case is missing in a case or selector statement.
* numberOfInconsistentNamingConventionSmells -- Smell exists when the used naming convention deviates from the recommended naming convention.
* numberOfComplexExpressionSmells -- Smell exists when a program contains a difficult to understand complex expression.  
* numberOfDuplicateEntitySmells -- Smell exists duplicate parameters are present in the configuration code.
* numberOfMisplacedAttributeSmells -- Smell exists when attribute placement within a resource or a class has not followed a recommended order.
* numberOfImproperAlignmentSmells -- Smell exists when the code is not properly aligned or tabulation characters are used 
* numberOfInvalidPropertyValueSmells -- Smell exists when an invalid value of a property or attribute is used.
* numberOfIncompleteTasksSmells -- Smell exists when the code has “fixme” and “todo” tags indicating incomplete tasks.
* numberOfDeprecatedStatementUsageSmells -- Smell exists when the configuration code uses one of the deprecated statements.
* numberOfImproperQuoteUsageSmells -- Smell exists when single and double quotes are not used properly.
* numberOfLongStatementSmells -- Smell exists when the code contains long statements.
* numberOfIncompleteConditionalSmells -- Smell exists when an “if..elseif” construct used without a terminating “else” clause.
* numberOfUnguardedVariableSmells -- Smell exists when a variable is not enclosed in braces when being interpolated in a string.

Docker Metrics are based on the following [rules](https://github.com/hadolint/hadolint#rules).

**Docker** Metrics:

* numberOfUpgradeSmells -- Smell exists when apt-get or apk commands are used problematically.
* numberOfPinVersionSmells -- Smell exists when version of packages is not explicitly declared.
* numberOfUntaggedImageSmells -- Smell exists when version of images is not explicitly declared.
* numberOfSudoSmells -- Smell exists when sudo command and root user are used inappropriately.
* numberOfCopySmells -- Smell exists when COPY instruction is not used properly.
* numberOfFromSmells -- Smell exists when FROM instruction is not used properly.
* numberOfCmdSmells -- Smell exists when CMD and ENTRYPOINT instruction is not used properly.
* numberOfAddSmells -- Smell exists when ADD instruction is not used properly.
* numberOfMeaninglessCommandsSmells -- Smell exists when there are commands that makes no sense running them in a Docker container.
* numberOfInvalidPortsSmells -- Smell exists when invalid UNIX ports range is used.
* numberOfShellSmells -- Smell exists when SHELL instruction is not used when it should.

All of the above metrics have their corresponding allOfSmells metrics (e.g. numberOfMultifacetedSmells -> allOfMultifacetedSmells) that lists the actual smells.

**Pattern and Anti-pattern** Metrics:

* puppetPatternIntroduction: The metric will list the smells that removed between two consecutive versions of a puppet file.
* puppetAntipatternIntroduction: The metric will list the smells that introduced between two consecutive versions of a puppet file.
* dockerPatternIntroduction: The metric will list the smells that removed between two consecutive versions of a Dockerfile.
* dockerAntipatternIntroduction: The metric will list the smells that introduced between two consecutive versions of a Dockerfile.

**Components** metrics:

* allDockerLibraries: Retrieves all the libraries that are installed with the use of apt-get install or apk install in Dockerfiles
* numberOfDockerLibraries: Retrieves the number of the above libraries
* allDockerImages: Retrieves all the images that are used with the use of FROM instruction in Dockerfiles
* numberOfDockerImages: Retrieves the number of the above images

**New versions** Metrics:

* newVersionFound: The metric will list the new versions (if any) of libraries that are used in the project.



