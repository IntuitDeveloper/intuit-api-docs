---
layout: default
title: Mutation
nav_order: 2
parent: GraphQL Concepts
---

## Mutation

Mutation is the GraphQL concept used to modify data on the server.  This includes creates, updates, or deletion of data.  Think of it as a POST, PUT or DELETE operation in the REST API world, **but remember - GraphQL requests are always POST calls**. 

As an example, here is a simple GraphQL mutation that would create an employer deduction:

```
mutation {
  createEmployerDeduction (
    deduction: {
      name: "My plan deduction"
      statutoryDeductionPolicy: "Annual max is 10k"
    }
  ) {
    id
    name
  }
}
```

Mutations typically take an input data type (in this case, the "deduction" input data), and define fields from the response type to be returned (in this case, return the generated `id` and `name` fields of the created deduction).
