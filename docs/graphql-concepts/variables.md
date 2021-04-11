---
layout: default
title: Variables
nav_order: 4
parent: GraphQL Concepts
---

## Variables

Using variables can simplify your queries and mutations using arguments as you don’t need separate operations for every argument possible. Variables in GraphQL allow clients to separate dynamic input from otherwise static operations. A GraphQL variable object is a JSON object containing the fields that your operation can accept. 

```
query queryName ($variable : type) {
  fieldName1
  fieldName2 (filter: {field1 {in : $variable}}) {
    field1
    field2
  }
}
```

Variables:
```
{
  variable: “value”
}
```

