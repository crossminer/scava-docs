# SCAVA Testing recommendations

## Knowledge Base

This builds needs some configuration to run successfully. 

In the application.properties files:
* `/knowledge-base/org.eclipse.scava.knowledgebase/src/main/resources/application.properties`
* `/knowledge-base/org.eclipse.scava.knowledgebase/src/test/resources/application.properties`

Edit the following parameters:
```
lucene.index.folder=/tmp/scava_lucene/
egit.github.token=3f5accc2f8f4cXXXXXXXXX73b201692fc1df57
```

To generate the GitHub access token you need to go to [your own GitHub account](https://github.com/settings/tokens) and create a new one. Once it's done simply restart the tests, they should pass.

