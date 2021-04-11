---
layout: default
title: Introspection
nav_order: 3
parent: GraphQL Concepts
---

## Use directives to control server responses 

Directives let you conditionally control which keys and values the server returns in it's response. 

Instead of adjusting queries to add or remove fields, use directives to only see the data you currently need. You conditionally include or skip fields based on the argument passed to the directive.    


How to create directives 
For Intuit Ecosystem API, you can use the core GraphQL @include and @skip directives. These both use Boolean arguments. 
Here's an example query with @include for fieldName2.

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
