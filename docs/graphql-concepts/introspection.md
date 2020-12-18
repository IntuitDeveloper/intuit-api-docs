---
layout: default
title: Introspection
nav_order: 3
parent: GraphQL Concepts
---

## Introspection

Introspection allows you to query the schema for information about itself. That means the response of an introspection query contains the entire schema structure, including all the field names, types, and relationships. This is useful as you build your queries but it is especially useful to find out about updates to the schema. 
Note: Developers can query the full Ecosystem API schema but will have access to only certain parts of it based on the scopes their app is authorized for.

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
