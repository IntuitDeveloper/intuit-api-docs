---
layout: default
title: Directives
nav_order: 5
parent: GraphQL Concepts
---

# Use directives to control server responses 

Directives let you conditionally control which fields and values the server returns in it's response. 

Instead of adjusting queries to add or remove fields, use directives to only see the data you currently need. You include or skip fields based on the argument you pass to the directive.    

## How to create directives 
For Intuit Ecosystem API, use the core GraphQL **@include** and **@ski** directives. Both use Boolean arguments.

Here's an example query with **@include** for `fieldName2`.

```
query 
  queryName($condition: Boolean) {
    fieldName1
    fieldName2 @include(if: $condition) {
     field1
     field2
    }
  }
```
The server will include `fieldName2` in the response if the **$condition** is met.

Learn more about [directives from GraphQL.org](https://graphql.org/learn/queries/#directives). 