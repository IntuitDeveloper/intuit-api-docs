---
layout: default
title: GraphQL Concepts
nav_order: 3
has_children: true
permalink: /docs/graphql-concepts/
---

# GraphQL Concepts

The following pages describe some GraphQL concepts, like queries and mutations.

## What is GraphQL?

GraphQL is a query language for APIs, which allows clients to ask for the data they need (and nothing more), in the format they want, across multiple resources, in a single request. All requests are served through a single endpoint, so the request body is responsible for expressing the actions for a server to execute on resources.

> “At its simplest, GraphQL is about asking for specific fields on objects.” [[https://graphql.org](https://graphql.org){:target="_blank"}]

Some of its design principles are that it is:

- __Customizable__: GraphQL allows you to query as many fields from the API as you actually need. There’s no over-fetching or under-fetching.
- __Strongly typed__: A GraphQL server defines the application’s type system. This makes it easy for tools to validate that a given query is valid and can be executed. 
- __Introspective__: Information about the schema is available by querying the schema. This provides a way to understand all of the fields and operations available and ensures that clients are always kept up-to-date with changes to the schema. 
- __Hierarchical__: A GraphQL query is structured just like the data it returns. It naturally follows relationships between fields and helps to present this data in a user interface.
- __Language-independent__: GraphQL can be used with any backend framework or programming language implementation.
