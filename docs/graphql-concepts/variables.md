---
layout: default
title: Variables
nav_order: 4
parent: GraphQL Concepts
---

# Use variables to simplify queries and mutations

Variables let you create dynamic code. 

Instead of entering static values for every argument, define and use a variable. You can update the variable anytime to push changes for that value everywhere in your code.

This simplifies code and makes it much easier to maintain. 

## How to define and enter variables 
In GraphQL, variables are JSON objects. You can use variables for both [queries](https://intuitdeveloper.github.io/intuit-api-docs/docs/graphql-concepts/query/) and [mutations](https://intuitdeveloper.github.io/intuit-api-docs/docs/graphql-concepts/mutations/). 

Here's an example. First, we'll replace the static value in the query with $**variable**. 

```
query queryName ($variable : type) {
  fieldName1
  fieldName2 (filter: {field1 {in : $variable}}) {
    field1
    field2
  }
}
```
We replaced the value for the `in` field in `fieldName2` with the **$variable**. 

Then declare the variable and its value in a separate variable dictionary:

```
{
  variable: “value”
}
```
Now, any time you update the `variable`'s value, the change is reflected wherever you used the variable. 

Learn more about [variables from GraphQL.org](https://graphql.org/learn/queries/#variables). 
