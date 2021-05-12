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

### Only query for data your app needs

In GraphQL, less is more. Create queries that only request the specific fields and data required for your QuickBooks integration to be fully functional. You can change queries later and add more fields as needed. 
 
### Log frequently during development

Take the time to properly log your app development process. It saves time in the long-run. Logging every execution may impact app performance, so prioritize what matters most.

<table>
<tr>
<td><strong>Tip</strong>: Always [log value of the `intuit_tid` field](../../faq/error-handling/) in the server response. It will help our support team quickly find and address any reported issues.
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

[Pagination](/pagination/) lets you quickly navigate large datasets. If you expect a query to return lots of data, use pagination to fetch specific subsets. 


## Intuit Ecosystem API best practices

### Learn about API throttling
We're manually setting limits for partners during the beta phase. Currently, the limit is 500 requests/sec.

### Keep up with the latest version of Intuit Ecosystem API

The Intuit Ecosystem API base URL is versioned for schema updates. Meaning, the base URL updates each time the schema changes. 

We'll release notes about updates when they become available. Update your apps to the latest version to get the latest enhancements with each new version.

Note: We'll have more details around versioning in the future.


## Advantages of GraphQL

#### Single endpoints

Imagine a use-case where you want to get all the invoices created within a date range along with the items sold and the name and address of the customer for each invoice. You’d need to make several calls to different endpoints to achieve this. One for the Invoice, one for each Customer, and one for each Item. GraphQL has one endpoint for everything, all of this data can be obtained by making one call to a single endpoint.

#### Get only the data you need

Each call would give you all the information about the entity you’ve queried. You may not need the account information or the payment status on the invoice, for example. With a GraphQL query, specify which fields you want and only data for those fields gets returned. 

GraphQL queries are highly customizable. You specify the fields and values you want the server to return. Apps only get the data it queries for - there’s no over-fetching or under-fetching.

### Develop with any language
GraphQL is language-independent. You can use it with any backend framework or programming language implementation.

### Validate queries as you work

Because GraphQL is a type system and everything about it is part of its schema, it’s easy to check if your request is valid or not while it’s being created. You don’t have to wait until runtime to know if your request is invalid. There are multiple ways to validate a request: use a GraphQL tool (which has a built-in parser), use introspection queries to check the schema, or let the server validate the request against the schema version on the server.

GraphQL servers define the type system. That means everything about it is part of the schema. You can validate queries as you create them with testing tools or introspection. You can also let the server validate requests against the current schema.

### Everything is documented

Accurate and up-to-date documentation is always available along with the schema. You can make an introspection query any time you want to see all possible fields and operations for the latest version.

### Simple data hierarchies

GraphQL requests and responses are structured the same way and naturally follow relationships between attributes.