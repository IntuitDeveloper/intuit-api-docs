---
layout: default
---

{% Old header pieces; removing so that this page is hidden %}
{% title: Introspection %}
{% nav_order: 3 %}
{% parent: GraphQL Concepts %}

# Get schema info with introspection

Introspection is a unqie feature of GraphQL that lets you query the server any time to see the current schema. 

When you make an introspection query, the server returns the entire schema. This includes all possible fields, data types, and their relationships. It also tells you what operations the server supports.

Introspection is useful for creating and keeping queries up-to-date. Whenever you need to validate your code, simply use introspection to check the current schema. 

## How to create an introspection query

Use this query any time to get the current Intuit Ecosystem API schema:

```
query {
  __schema {
    types {
      name
      fields {
        name
      }
    }
  }
}
```
The server will return what's currently available for Intuit Ecosystem API. Keep in mind, [your app's scopes](../../getting-started/scopes/) determine what data you can access.

Learn more about [introspection from GraphQL.org](https://graphql.org/learn/introspection/).
