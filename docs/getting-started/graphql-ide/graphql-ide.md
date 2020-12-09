---
layout: default
title: GraphQL IDE
nav_order: 3
has_children: true
parent: Getting Started
permalink: /docs/getting-started/graphql-ide
---

## GraphQL IDE

Although not strictly necessary, you'll likely want a GraphQL IDE to easily form and test GraphQL queries.  Here are a few examples of GraphQL IDEs you can use:

1. [Insomnia](https://insomnia.rest/graphql/) - for detailed Insomnia setup, [click here](./insomnia-setup)
2. [GraphiQL](https://github.com/skevy/graphiql-app)

Once you install a GraphQL IDE, you should now be set to fire your first GraphQL query!

### Firing your first GraphQL Query

As an example, you can try a very basic query like the following to get the name of your QuickBooks company, using the OAuth 2.0 bearer token retrieved in the previous section.

```
query getCompanyName {
  company {
    companyName
    companyType
  }
}
```
Headers required:
```
Authorization: <OAuth 2.0 bearer token>
```

### Next Steps

- Want to learn more about GraphQL concepts, like queries and mutations?  [Click here](../../graphql-concepts)!

- Want to learn about Intuit use cases, like 401k or user roles?  [Click here](../../use-cases) to see sample queries and documentation about common use cases!