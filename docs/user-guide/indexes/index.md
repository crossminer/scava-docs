# Indexing Metrics Guide

This guide describes the indexing metric providers available in Scava platform. It provides the mapping so that users can query the index.

------
#### [org.eclipse.scava.metricprovider.indexing.bugs](#org.eclipse.scava.metricprovider.indexing.bugs)
- **Short name**: bug indexing metric
- **Friendly name**: Bugs tracking system indexer

This metric prepares and indexes analyses documents relating to bug tracking system.

**Mapping Information**:

- <u>bug.comment</u>

| Properties | Type |
|------------|------|
| comment_Id | `keyword`|
| body       | `text`|
| emotional_dimension * | `keyword`|
| sentiment | `keyword`|
| plain_text| `text`|
| request_reply_classification| `keyword`|
| content_class| `keyword`|
| contains_code| `boolean`|
| bug_Id | `keyword`|
| project_name| `keyword`|
| creator | `keyword` |
| created_at | `date`|
| uid| `keyword` |
| referring_to <br />	bugs *<br />	commits * | `Object`<br />`text` <br />`text` |

- <u>bug.post</u>

| Properties | Type  |
|------------|------|
| created_at | `date`   |
| bug_summary       | `text`   |
| severity          | `keyword`   |
| bug_id | `keyword`   |
| project_name       | `text`   |
| creator          | `keyword`   |
| uid | `keyword`   |
| migration_issue<br />	found<br />	problematic_changes<br />		change *<br />		type | `Object`<br />`boolean`<br />`Object`<br />`text`<br />`double` |

**Additional Note**: 

1. Asterisk (`*`) is used to indicate entries that are stored as an array.
2. Type `Object` is used to indicate an entry with a nested JSON object passed as its value. The depth of nesting is shown with Indentation at each node/level.    

------
#### [org.eclipse.scava.metricprovider.indexing.commits](#org.eclipse.scava.metricprovider.indexing.commits)
- **Short name**: metricprovider.indexing.commits
- **Friendly name**: Commits indexer

This metric prepares and indexes documents related to commits.

**Mapping Information**:

- <u>commits</u>

| Properties | Type |
|------------|------|
| created_at | `date`   | `Date` |
| project_name       | `keyword`   | `String` |
| uid          | `text`   | `String` |
| repository | `keyword`   | `String` |
| revision       | `keyword`   | `String` |
| author          | `keyword`   | `String` |
| author_email | `keyword`   | `String` |
| body | `text`   | `String` |
| plain_text       | `text`   | `String` |
| commits_references *        | `text`   | `List<String>` |
| bugs_references * | `text`   | `List<String>` |

**Additional Note**: 

Asterisk (`*`) is used to indicate entries that are stored as an array.

------
#### [org.eclipse.scava.metricprovider.indexing.communicationchannels](#org.eclipse.scava.metricprovider.indexing.communicationchannels)
- **Short name**: communication channels indexing metric
- **Friendly name**: communication channels indexer

This metric prepares and indexes documents relating to communication channels.

**Mapping Information**:

- <u>article</u>

| Properties | Type  |
|------------|------|
| article_Id | `date`   | `Date` |
| communication_channel_id       | `keyword`   | `String` |
| uid          | `keyword`   | `String` |
| thread_id * | `keyword`   | `List<Integer>` |
| project_name       | `keyword`   | `String` |
| message_body          | `text`   | `String` |
| subject | `text`   | `String` |
| creator | `keyword`   | `String` |
| created_at       | `date`   | `Date` |
| emotional_dimension *        | `keyword`   | `List<String>` |
| sentiment | `keyword`   | `String` |
| plain_text | `text`   | `String` |
| request_reply_classification       | `keyword`   | `String` |
| content_class          | `keyword`   | `String` |
| contains_code | `boolean`   | `boolean` |

- <u>thread</u>

| Properties | Type|
|------------|------|
| communication_channel_id       | `keyword`   |
| uid          | `keyword`   |
| thread_id | `keyword`   |
| project_name       | `keyword`   |
| subject | `text`   |
| migration_issue<br />	found<br />	problematic_changes<br />		change *<br />		matching_score | `Object`<br />`boolean`<br />`Object`<br />`text`<br />`double` |

**Additional Note**: 

1. Asterisk (`*`) is used to indicate entries that are stored as an array.
2. Type `Object` is used to indicate an entry with a nested JSON object passed as its value. The depth of nesting is shown with Indentation at each node/level.  

------
#### [org.eclipse.scava.metricprovider.indexing.documentation](#org.eclipse.scava.metricprovider.indexing.documentation)
- **Short name**: communication channels indexing metric
- **Friendly name**: communication channels indexer

This metric prepares and indexes documents relating to communication channels.

**Mapping Information**:

- <u>documentation_entry</u>

| Properties | Type |
|------------|------|
| created_at       | `date`   |
| project_name          | `keyword`   |
| uid | `keyword`   |
| documentation_id       | `keyword`   |
| documentation_entry_id | `keyword`   |
| communication_channel_id       | `keyword`   |
| body          | `text`   |
| original_format_mime | `keyword`   |
| original_format_name | `text`   |
| plain_text | `text`   |
| sentiment       | `keyword`   |
| readability | `keyword`   |
| documentation_type *     | `keyword`   |
| licence_found | `boolean`   |
| licence<br />	group<br />	name<br />	header_found<br />	score<br />	is_deprecated_license<br />	is_fsf_libre<br />	is_osi_approved<br />	license_comments | `Object`<br />`keyword`<br />`keyword`<br />`boolean`<br />`double`<br />`boolean`<br />`boolean`<br />`boolean`<br />`text` |

- <u>documentation</u>

| Properties | Type|
|------------|------|
| last_update       | `date`   | `Date` |
| project_name          | `keyword`   | `String` |
| uid | `text`   | `String` |
| documentation_id       | `keyword`   | `String` |
| documentation_entries * | `keyword`   | `List<String>` |

**Additional Note**: 

1. Asterisk (`*`) is used to indicate entries that are stored as an array.
2. Type `Object` is used to indicate an entry with a nested JSON object passed as its value. The depth of nesting is shown with Indentation at each node/level.  

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

### Example 6

With the indexes it is possible to do aggregations and how many times a field value defined as a keyword, such as documentation_id, appears in an index.

```
POST documentation.documentation.entry.nlp/_search
{
  "size": 0, 
  "aggs": {
    "doc_id": {
      "terms": {
        "field": "documentation_id",
        "size": 100
      }
    }
  }
}
``` 

------
