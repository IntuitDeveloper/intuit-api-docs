---
layout: default
title: Testing
nav_order: 4
has_children: true
permalink: /docs/getting-started/graphql-ide/
parent: Getting Started
---

# Testing queries using a GraphQL IDE

Use a GraphQL Integrated Developer Environment (IDE) to test and validate queries during development. 

Here are the basic steps to set up, download a GraphQL IDE, and send a test query to get the `companyName` for your [sandbox test company](https://developer.intuit.com/app/developer/qbo/docs/develop/sandboxes/manage-your-sandboxes).

## Step 1: Set up your app in the Intuit Developer Portal

If you haven't already, [get a QuickBooks Online sandbox company](../authentication/) for testing, [create your app](../authentication/), and get your sandbox company's [**Client ID** and **Client Secret**](../authentication/). 

## Step 2: Get a GraphQL IDE

There are many GraphQL IDEs available. Use the one you prefer. 

Here are a couple we recommend. In particular, we prefer Insomnia for its collection and built-in authorization features. 

* [Set up and test with Insomnia](./insomnia)
* [Set up and test with GraphiQL](./graphiql)

## Step 3: Send a test query

After you install a GraphQL IDE, use this basic query to get the `companyName` for your [sandbox test company](https://developer.intuit.com/app/developer/qbo/docs/develop/sandboxes/manage-your-sandboxes). 

**Query header**
```
Authorization: <OAuth 2.0 bearer token>
```
**Query body**
```
query getCompanyName {
  company {
    companyName
    companyType
  }
}
```
The server should return details about your sandbox test company.
