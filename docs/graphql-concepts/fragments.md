---
layout: default
title: Fragments
nav_order: 6
parent: GraphQL Concepts
---

# Create fragments for sets of fields

Fragments are reusable sets of fields you can use across queries.

In GraphQL, you can define and group sets of fields into fragments. Instead of repeating individual fields, simply call the fragment to utilize all the fields and related data at once. 

This lets you organize code into modular, bite-sized "chunks."  

## How to create and use fragments 

For Intuit Ecosystem API, fragments are useful for queries that constantly reuse the same sets of fields.

Here's an example of defining a fragment and using it in a query: 

```
query 
  queryName {
    fieldName1
    fieldName2 {
      ...fragmentName
    }
  }
```
We put `fragmentName` in `fieldName2`. 

Now define the fragment and corresponding set of fields: 

```
fragment 
  fragmentName on FieldName {
    field1
    field2
    field3
  }
```
Now, instead of entering each individual field, you can just use `fragmentName`. 

Learn more about [fragments from GraphQL.org](https://graphql.org/learn/queries/#variables). 
