# Indexing Metrics Guide

This guide describes the indexing metric providers available in Scava platform. It provides the mapping so that users can query the index. 

------
#### [org.eclipse.scava.metricprovider.indexing.bugs](#org.eclipse.scava.metricprovider.indexing.bugs)
- **Short name**: bug indexing metric
- **Friendly name**: Bugs tracking system indexer

This metric prepares and indexes analyses documents relating to bug tracking system.

**Mapping Information**:

- <u>bug.comment</u>
	- `String`	comment_Id
	- `String`	body
	- `List<String>`	emotional_dimension
	- `String`	sentiment
	- `String`	plain_text
	- `String`	request_reply_classification
	- `String`	content_class
	- `boolean`	contains_code
	- `String`	bug_Id
	- `String`	project_name
	- `String`	creator
	- `Date`	created_at
	- `String`	uid
	- `List<String>`	commits
	- `List<String>`	referring_to

- <u>bug.post</u>
	- `Date`	created_at
	- `String`	bug_summary
	- `String`	severity
	- `String`	bug_id
	- `String`	project_name
	- `String`	creator
	- `String`	uid
	- `boolean`	migration_issue
	- `List<String>`		problematic_changes
	- `double`	matching_score

------
#### [org.eclipse.scava.metricprovider.indexing.commits](#org.eclipse.scava.metricprovider.indexing.commits)
- **Short name**: metricprovider.indexing.commits
- **Friendly name**: Commits indexer

This metric prepares and indexes documents related to commits.

**Mapping Information**:

- <u>commits</u>
	- `Date`	created_at
	- `String`	project_name
	- `String`	uid
	- `String`	repository
	- `String`	revision
	- `String`	author
	- `String`	author_email
	- `String`	body
	- `String`	plain_text
	- `List<String>`	commits_references
	- `List<String>`	bugs_references

------
#### [org.eclipse.scava.metricprovider.indexing.communicationchannels](#org.eclipse.scava.metricprovider.indexing.communicationchannels)
- **Short name**: communication channels indexing metric
- **Friendly name**: communication channels indexer

This metric prepares and indexes documents relating to communication channels.

**Mapping Information**:

- <u>article</u>
	- `Long`	article_Id
	- `String`	communication_channel_id
	- `String`	uid
	- `List<Integer>`	thread_id
	- `String`	project_name
	- `String`	message_body
	- `String`	subject
	- `String`	creator
	- `Date`	created_at
	- `List<String>`	emotional_dimension
	- `String`	sentiment
	- `String`	plain_text
	- `String`	request_reply_classification
	- `String`	content_class
	- `boolean`	contains_code
- <u>thread</u>
	- `String`	communication_channel_id
	- `String`	uid
	- `int`	thread_id
	- `String`	project_name
	- `String`	subject
	- `boolean`	migration_issue
	- `List<String>`	problematic_changes
	- `double`	matching_score

------
#### [org.eclipse.scava.metricprovider.indexing.documentation](#org.eclipse.scava.metricprovider.indexing.documentation)
- **Short name**: communication channels indexing metric
- **Friendly name**: communication channels indexer

This metric prepares and indexes documents relating to communication channels.

**Mapping Information**:

- <u>documentation_entry</u>
	- `Date`	created_at
	- `String`	project_name
	- `String`	uid
	- `String`	documentation_id
	- `String`	documentation_entry_id
	- `String`	body
	- `String`	original_format_mime
	- `String`	sentiment
	- `String`	plain_text
	- `double`	readability
	- `List<String>`	documentation_type
	- `boolean`	licence_found
	- `String`	licence
- <u>documentation</u>
	- `Date`	last_update
	- `String`	uid
	- `String`	project_name
	- `String`	documentation_id
	- `List<String>`	documentation_entries

------
# Query Example

The query below retrieves entries that has the API documentation. Further information about Elasticsearch query can be found at https://www.elastic.co/guide/en/elasticsearch/reference/current/search.html


```
GET documentation.documentation.entry.nlp/_search
{
  "query" : {
    "match": {
      "documentation_types" : "API"
    }

  }

}
```

------
