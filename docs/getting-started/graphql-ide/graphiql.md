---
layout: default
title: GraphiQL
nav_order: 1
parent: Testing GraphQL
grand_parent: Getting Started
permalink: /docs/getting-started/graphql-ide/graphiql
---

## Set up and test with GraphiQL 

### Step 1: Set up your app in the Intuit Developer Portal

If you haven't already, [get a QuickBooks Online sandbox company](../authentication/) for testing and [create your app](../authentication/) on the Intuit Developer Portal. 
 
### Step 2: Get your app's credentials

[Sign in](https://developer.intuit.com/app/developer/myapps) to your developer account and [get your sandbox company's **Client ID** and **Client Secret**](../authentication/). 

### Step 3: Get GraphiQL

Go to GitHub to [download and install GraphiQL](https://github.com/skevy/graphiql-app).

### Step 4: Set up OAuth2.0
If you haven't already, [set up OAuth 2.0](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization) for your app. This gives you access tokens to make API calls with GraphiQL.

### Step 5: Create a test query in GraphiQL

After you install GraphiQL and set up OAuth 2.0, use this basic test query to get the `companyName` of your [sandbox test company](https://developer.intuit.com/app/developer/qbo/docs/develop/sandboxes/manage-your-sandboxes). 

**Query header**
```
Authorization: <OAuth 2.0 bearer token>
```
**Query body**
```
query 
getCompanyName {
  company {
    companyName
    companyType
  }
}
```
You're now ready to test queries in GraphiQL.