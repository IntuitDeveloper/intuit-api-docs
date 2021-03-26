---
layout: default
title: Best Practices
nav_order: 4
parent: FAQ
---

## Best Practices


By properly integrating the following best practices, your implementation and its associated API structure can be more powerful, efficient, and practical.

  

#### Request only for data that you need

Apps should only request for fields they needed right now, you can always request additional fields later as you utilize them.

  

#### Updating to latest Version of the API

Ecosystem API base url will be versioned for schema updates. Make sure to upgrade your apps to the latest version of the API to benefit from the enhancements to the schema with each new versioned release for Ecosystem API.

Note: We will have more details around versioning of the Ecosystem API and how developers will be notified later on.(TBD)

#### Logging

Logging every execution will have a performance impact on your app. We recommend logging during development or if you see any errors. The Ecosystem API response header contains a field called intuit_tid. Be sure to log this field as it will help to investigate the issue quickly when any issue occurs.

#### Global IDs

Ecosystem API provides IDs to elegantly handle caching and re-fetching data with the node field on the root query object. The ID to be used for re-fetching is provided in an id field on the result. Please note that this is currently not supported for Payslip use cases.

#### Introspection

Querying which resources are available in the Ecosystem API schema using introspection will help to see the queries, types, fields, and directives it supports.  [Read more on using introspection here](../../graphql-concepts/introspection)

#### Using Aliases

We recommend using aliases or operation names to avoid confusion when multiple queries are passed at once. Use aliases also if you have more than one top-level field in the same query with different arguments.

#### Pagination

The GraphQL type system allows for some fields to return lists of values and also allows pagination. If you expect to get a large number of results for a query, we recommend using pagination to fetch only a subset of records at a time.  [Read more about pagination here](../../graphql-concepts/other-concepts/#pagination)

#### API Throttling

Limits for each partner will be enforced manually for the beta phase.

#### Using Fragments

Instead of specifying a list of field names we recommend creating a fragment as a best practice once and reuse it everywhere. This makes your queries modular and easy to understand.  [Read more about fragments here](../../graphql-concepts/other-concepts/#fragments)