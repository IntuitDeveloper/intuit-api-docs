---
layout: default
title: GraphQL Concepts
nav_order: 3
has_children: true
permalink: /docs/graphql-concepts/
---

# Learn about GraphQL

Intuit Ecosystem API uses the [GraphQL API framework](https://graphql.org/). Here's a brief overview of GraphQL.

## What's GraphQL?

GraphQL is an API query language that simplifies client-side requests. Apps can do a lot with a single query: it can query data across multiple resources and entities, request data in a specific format, or get the server to perform several operations. 

> “At its simplest, GraphQL is about asking for specific fields on objects.” [GraphQL.org](https://graphql.org){:target="_blank"}]

All queries go to a single endpoint on the server. The server parses queries and only returns the requested data in the requested format. 

## What are some of GraphQL's advantages?

- **Get only the data you need**: GraphQL queries are highly customizable. You specify the fields and values you want the server to return. Apps only get the data it queries for - there’s no over-fetching or under-fetching.
- **Develop with any language**: GraphQL is language-independent. You can use it with any backend framework or programming language implementation.
- **Validate queries as you work**: GraphQL servers define the type system. That means everything about it is part of the schema. You can validate queries as you create them with [testing tools](https://intuitdeveloper.github.io/intuit-api-docs/docs/getting-started/graphql-ide/) or [introspection](https://intuitdeveloper.github.io/intuit-api-docs/docs/graphql-concepts/introspection/). You can also let the server validate requests against the current schema.
- **Always have the current schema**: GraphQL is self-documenting. You can [make an introspection query](https://intuitdeveloper.github.io/intuit-api-docs/docs/graphql-concepts/introspection/) any time you want to see all possible fields and operations for the latest version. 
- **Create simple data hierarchies**: GraphQL requests and responses are structured the same way and naturally follow relationships between attributes.

Check out [GraphQL.org](https://graphql.org/){:target="_blank"} for a deepr dive.

Also check out: [courses from edx.org](https://www.edx.org/course/exploring-graphql-a-query-language-for-apis){:target="_blank"}.