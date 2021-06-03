---
layout: default
title: GraphQL best practices
nav_order: 8
parent: GraphQL Concepts
---

# Adopt Intuit Ecosystem API best practices

GraphQL is a powerful and efficient API language. Here are a few ways you can structure and craft your code to build world-class apps.

For more tips, [visit GraphQL.org](https://graphql.org/learn/best-practices/). 

## GraphQL best practices

### Only query for the data your app needs

In GraphQL, less is more. Create queries that only request the specific fields and data required for your QuickBooks integration to be fully functional. You can change queries later and add more fields as needed. 
 
### Log frequently during development

Take the time to properly log your app development process. It saves time in the long-run. Logging every execution may impact app performance, so prioritize what matters most.

<table>
<tr>
<td><strong>Tip</strong>: Always <a href="../../faq/error-handling/">log the value of the <strong>intuit_tid</strong> field</a> in the server response. It will help our support team quickly find and address any reported issues.
</td>
</tr>
</table>

### Rely on Global Object IDs for standardization

GraphQL servers expose object IDs in a standardized way. These are knwon as [Global Object IDs](https://graphql.org/learn/global-object-identification/). This makes handling caching and refetching data easier. 

Query the node field on the root query object (i.e. the field at the root of an object). The value of the `id` field in the server response is the Global Object ID. 

**Note**: Global Object IDs aren't currently supported for the payslips.

### Use aliases to query the same field with different arguments

[Aliases](https://graphql.org/learn/queries/#aliases) let you rename the results of identical object fields so you can query the same field for different arguments. You can pass multiple queries at once and get responses for both fields without conflict. 
 
### Always include operation names to avoid confusion

Consciously [use operation names](https://graphql.org/learn/queries/#operationname) to make your code crystal clear, concrete, and unambiguous. 
 
### Create fragments to speed up code writing

Instead of querying frequently used fields individually, [create and reuse fragments](../fragments/) whenever possible. This makes code modular and easier to scale. 
 
### Take advantage GraphQL's unique features to get more done

[Introspection](../introspection/) is the quickest way to see the latest Intuit Ecosystem API schema.  Simply send an introspection query. The server response includes all possible queries, data types, fields, and operations. 

[Pagination](../pagination/) lets you quickly navigate large datasets. If you expect a query to return lots of data, use pagination to fetch specific subsets. 

## Intuit Ecosystem API best practices

### Learn about API throttling
We're manually setting limits for partners during the beta phase. Currently, the limit is 500 requests/sec.

### Keep up with the latest version of Intuit Ecosystem API

The Intuit Ecosystem API base URL is versioned for schema updates. Meaning, the base URL updates each time the schema changes. 

We'll release notes about updates when they become available. Update your apps to the latest version to get the latest enhancements with each new version.

**Note**: We'll have more details around versioning in the future.


## Advantages of GraphQL

### Single endpoints

Let's say you want to build an invoicing app. It needs to constantly request data for a specific set of invoices. The invoices contain particular items for a specific date range. And, the app needs current business addresses for each customer. 

With REST API, you’d need to make several queries to different endpoints: one for the invoice, one for each customer, and one for each item.

GraphQL only requires a single query, [sent to a single endpoint](../../getting-started/endpoints/). 

### Get only the data you need

GraphQL queries are highly customizable. You specify the exact fields and values you want the server to return. Apps only get the data you query for - there’s no over-fetching or under-fetching.

### Develop with any language
GraphQL is language-independent. You can use it with any backend framework or programming language implementation.

### Validate queries as you work

Since GraphQL is a type system, everything about it is part of its schema. You can validate queries as you create them with [testing tools like GraphiQL](../..graphiql-ide/) (which has a built-in parser) or [by making an introspection query](../introspection/). You can also let the server validate requests against the current schema version.

### Everything is documented

Accurate and up-to-date documentation is always available along with the schema. You can [make an introspection query](../introspection/) any time you want to see all possible fields and operations for the latest version.

### Simple data hierarchies

GraphQL requests and responses are structured the same way. It naturally follows relationships between attributes.
