---
layout: default
title: Other Concepts
nav_order: 4
parent: GraphQL Concepts
---

## Variables

Using variables can simplify your queries and mutations using arguments as you don’t need separate operations for every argument possible. Variables in GraphQL allow clients to separate dynamic input from otherwise static operations. A GraphQL variable object is a JSON object containing the fields that your operation can accept. 

```
query queryName ($variable : type) {
  fieldName1
  fieldName2 (filter: {field1 {in : $variable}}) {
    field1
    field2
  }
}
```

Variables:
```
{
  variable: “value”
}
```

## Fragments

Fragments are sets of fields. Instead of specifying a list of field names whenever you use them, create a fragment once and reuse it everywhere. 

```
query queryName {
  fieldName1
  fieldName2 {
    ...fragmentName
  }
}

fragment fragmentName on FieldName {
  field1
  field2
  field3
}
```

## Directives

Directives are a way to conditionally control which fields are returned by a query. You can either include or skip a certain field or fields based on the argument passed to the directive. 

```
query queryName($condition: Boolean) {
  fieldName1
  fieldName2 @include(if: $condition) {
    field1
    field2
  }
}
```

## Pagination

When you don’t want to fetch all of the records at once, use cursor-based pagination to get a subset at a time. The pageInfo object shows you information about what data was returned and how much more there still is.

Note: You can reference the schema docs or do an Introspection query to determine which fields support pagination.

```
query queryName {
  fieldName1
  fieldName2(pagination: {first: numOfRecords, after: cursorValue}) }) {
    pageInfo {
      hasNextPage
      startCursor
      endCursor
      hasPreviousPage
    }
    field1
    field2
  }
}
```

## Learn more 

- GraphQL official documentation: [https://graphql.org/](https://graphql.org/){:target="_blank"}
- Explore GraphQL: [https://www.graphql.com/](https://www.graphql.com/){:target="_blank"}
- Course: [https://www.edx.org/course/exploring-graphql-a-query-language-for-api](https://www.edx.org/course/exploring-graphql-a-query-language-for-api){:target="_blank"}
