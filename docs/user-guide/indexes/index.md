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
# Query Examples

Here we present a series of examples of how you can use ElasticSearch queries for finding specific data or doing some aggregations.

More information about ElasticSearch queries can be found at https://www.elastic.co/guide/en/elasticsearch/reference/6.3/search.html

### Example 1

 Retrieve the documentation entries that have been determined containing a *Getting Started* guide.

```
GET documentation.documentation.entry.nlp/_search
{
  "query": {
	"match" : {
	  "documentation_types": "Started"

	}
  }
}
```
As *documentation_types* is an array, we need to use a *match* within the query.

## Example 2

Retrieve the documentation entries that have at least one of the following characteristics:
- Are a *Getting Started* guide
- Are a *Development* guide
- Have a neutral sentiment

```
GET documentation.documentation.entry.nlp/_search
{
  "query": {
    "bool": {
      "should": [
          {
            "match" : {
              "documentation_types": "Started"
          	}
          },
          {
            "match" : {
              "documentation_types": "Development"
            }
          },
          {
            "term":{
              "sentiment" : "__label__neutral"
            }
          }
      ]
    }
  }
}
```

In this case, the field sentiment is not an array, thus, for looking inside of it we should use a *term* query, while a *match* query for fields that are arrays. Furthermore, as we have multiple queries that are linked through OR, we need to declare a query of type *bool* and *should*. If the query would be to find the documentation entries that have a *Getting Started*, a *Development* guide and have a neutral sentiment, instead of using a *should* operation, it need to be used a *must*.

```
GET documentation.documentation.entry.nlp/_search
{
  "query": {
    "bool": {
      "must": [
          {
            "match" : {
              "documentation_types": "Started"
          	}
          },
          {
            "match" : {
              "documentation_types": "Development"
            }
          },
          {
            "term":{
              "sentiment" : "__label__neutral"
            }
          }
      ]
    }
  }
}
```

### Example 3

Searching for GitHub Issues comments containing the word *issue* in the field *plain_text*:

```
GET github.bug.comment.nlp/_search
{
  "query": {
    "match": {
      "plain_text": "issue"
    }
  }
}
```

### Example 4

 Searching in all the indexes the string *Astérix*:

```
GET _search
{
 "query": {
   "query_string": {
     "query": "Astérix"
   }
 }
}
```
In this case, as we are not quering any particular field, we use the *query_string*.

If we would like to search either for *Astérix* or *Obélix*, we can use boolean operators:

```
GET _search
{
 "query": {
   "query_string": {
     "query": "Astérix OR Obélix"
   }
 }
}
```

If both names must appear, instead of using OR, we can use AND.

```
GET _search
{
 "query": {
   "query_string": {
     "query": "Astérix AND Obélix"
   }
 }
}
```
Query strings such as *Astérix Obélix* will be considered to have an implicit OR, i.e. *Astéric OR Obélix*.

```
GET _search
{
 "query": {
   "query_string": {
     "query": "Astérix Obélix"
   }
 }
}
```

If the we are looking for the exact combination of words, such as *Astérix and Obélix*, we can use parenthesis to indicate ElasticSearch that the words should be split.

```
GET _search
{
 "query": {
   "query_string": {
     "query": "(Astérix and Obélix) OR (Felix the Cat)"
   }
 }
}
```

### Example 5

ElasticSearch can do some statistics regarding the output of queries. In this example, we want extended statistics about the field readability in the documentation entries:

```
GET documentation.documentation.entry.nlp/_search
{
  "size": 0,
  "aggs" : {
        "readability_stats" : {
			"extended_stats" : {
				"field" : "readability"
			}
		}
    }
}
```

The option *size=0*, indicates that only the aggregation with the statistics must be returned, otherwise the query will return the elements that also match the searching query.

If instead of wanting some statistics, we want to autogenerate histograms, then we can use the following query:

```
POST documentation.documentation.entry.nlp/_search
{
  "size": 0,
  "aggs": {
    "histogram_analysis": {
      "histogram" : {
            	"field" : "readability",
                "interval" : 2
      }
    }
  }
}
```

------
