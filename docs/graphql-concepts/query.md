---
layout: default
title: Query
nav_order: 1
parent: GraphQL Concepts
---

## Query

Query is the GraphQL concept used to fetch data.  Here is an example GraphQL query:

```
query getCompanyName {
  company {
    companyName
    companyType
  }
}
```

With GraphQL, you specify the exact data fields your use case requires, no more and no less.  In this basic query, we are simply going to fetch the `companyName` and `companyType` fields.

This is one of the main advantages of GraphQL.  Not only is the response clean and specific for your use case, but it can often be more performant, as the Intuit API does not need to fetch and process fields that won't even be used by the client (a term called "over-fetching").

Feel free to play around with different queries.  Many GraphQL IDEs have an autocomplete feature, to make forming queries easier!

Next, learn about modifying data with [Mutations](../mutation).