---
title: Ask Queries
keywords: graql, query, ask
last_updated: August 10, 2016
tags: [graql]
summary: "Graql Ask Queries"
sidebar: documentation_sidebar
permalink: /documentation/graql/ask-queries.html
folder: documentation
---

An ask query will return whether the given [match query](graql_match.html) has any results.

```sql
match dragon isa pokemon-type
ask
```
```java
qb.match(id("dragon").isa("pokemon-type")).ask().execute();
```


{% include links.html %}

## Document Changelog  

<table>
    <tr>
        <td>Version</td>
        <td>Date</td>
        <td>Description</td>        
    </tr>
    <tr>
        <td>v1</td>
        <td>17/08/2016</td>
        <td>New page for developer portal.</td>        
    </tr>

</table>