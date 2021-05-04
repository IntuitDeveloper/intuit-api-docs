---
layout: default
title: Pagination
nav_order: 7
parent: GraphQL Concepts
---

# Use pagination to fetch subsets of data

Pagination lets you quickly search and request subsets of data within larger datasets. 

In GraphQL, you can use the **pageInfo** object and cursor-based pagination (`endCursor` and `startCursor`) to set criteria or collect data after a certain point in the response. This typically yields smaller payloads and faster server responses.

## How to use pagination

Pagination can help when there's lots of comingled data. For example, you may only need data from specific subaccounts rather than everything on [the chart of accounts](https://developer.intuit.com/app/developer/qbo/docs/concepts).

Here's an example query to get the number of records following the `cursorValue`.

```
query queryName {
  fieldName1
  fieldName2(pagination: {first: numOfRecords, after: cursorValue}) {
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

In this case, the server will only count records following the `cursorValue`. **Tip**: You can [use introspection](./introspection/) to see which fields support pagination.

Learn more about [pagination from GraphQL.org](https://graphql.org/learn/pagination/).
