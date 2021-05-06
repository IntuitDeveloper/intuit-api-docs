---
layout: default
title: Query
nav_order: 1
parent: GraphQL Concepts
---

# Create queries to request data

In GraphQL, queries can fetch data for single or multiple fields, apply filters, and get conditional data. If you're familiar with REST API, this is very similar to the GET operation. However, queries in GraphQL are always **POST** operations. 

GraphQL queries are very efficient. When apps send requests with queries, the server only returns the requested data. The response will be the same shape and format as the query. 

Server responses are clean, specific, and easy to work with. This also boosts app performance. Servers don't slow down to fetch unusable or extraneous data.

## How to create queries

For Intuit Ecosystem API, use queries to get data for accounts, transactions, and other resources. Specify the exact fields you want the server to return in the query body.
 
Here's a simple query to get company information:

```
query getCompanyName {
  company {
    companyName
    companyType
  }
}
```
The server will return values for the `companyName` and `companyType` fields. 

Learn more about queries [from GraphQL.org](https://graphql.org/learn/queries/). 
