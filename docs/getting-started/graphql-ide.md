---
layout: default
title: Test queries
nav_order: 4
parent: Getting Started
---

## Test queries with Insomnia or GraphiQL 

Use an Integrated Developer Environment (IDE) to test and validate queries during development.

There are a couple IDEs we recommend for Intuit Ecosystem API: Insomnia and GraphiQL. In particular, we prefer Insomnia for it's collection and built-in authorization features. Here's how to set up and use IDEs to test queries. 

## Set up and test with Insomnia 

You can [start with the free version of Insomnia](https://insomnia.rest/products/insomnia). This gives you basic features that cover most testing requirements. If you need more features, you can always upgrade later on.

Insomnia lets you keep collections of sample GraphQL queries you can use over and over for testing. It also uses OAuth syntax and lets you use variables to update things like access tokens. 

**Tip**: You can also follow the [install guide from Insomnia](https://support.insomnia.rest/article/23-installation). 
 
### Step 1: Set up your app in the Intuit Developer Portal

If you haven't already, [get a QuickBooks Online sandbox company](../authentication/) for testing and [create your app](../authentication/) on the Intuit Developer Portal. 
 
### Step 2: Get your app's credentials

1. [Sign in](https://developer.intuit.com/app/developer/myapps) to your developer account.
2. Select the **Dashboard** link on the toolbar. 
3. Select and open your app. 
4. In the **Development** section, select **Keys & OAuth**. Info in this section is only for your [sandbox test company](https://developer.intuit.com/app/developer/qbo/docs/develop/sandboxes/manage-your-sandboxes).
5. Copy the **Client ID** and **Client Secret**. 
 

### Step 3: Add the Insomnia redirect URI

1. [Sign in](https://developer.intuit.com/app/developer/myapps) to your developer account.
2. Select the **Dashboard** link on the toolbar. 
3. Select and open your app. 
4. In the **Development** section, select **Keys & OAuth**.
5. In the **Redirect URIs** section, select **Add URI**. 
5. Enter the insomnia redirect URI: **https://insomnia.rest**. 
 
### Step 4: Set up Insomnia
1. [Download the latest version](https://insomnia.rest/download) of Insomnia.
2. Launch and install Insomnia.
3. Select the **Manage environments** option.
4. Paste this configuration into the window:

```
{
"AccessTokenUrl": "https://oauth.platform.intuit.com/oauth2/v1/tokens/bearer",
"Authurl": "https://appcenter.intuit.com/connect/oauth2",
"ClientId": "[Your app's ClientID]",
"ClientSecret": "[Your app's ClientSecret]",
"RedirectUrl": "https://insomnia.rest",
"url": "https://public.api.intuit.com/2020-04/graphql"
}
```
This configures and connects Insomnia to your app and Intuit Ecosystem API. 

### Step 5: Start a test query in Insomnia
1. Select the **(+)** icon and then **New Request**. 
2. Name the request. 
3. Select the **POST** method from the dropdown. 
4. Select the **URL** environment variable. You set up the environment in Step 2.
5. Select **GraphQL query** as the query type.
6. Select **Create**. 

This opens a query window. Use this basic test query to get `company` data for your sandbox test company:

```
query company {
  company {
    id
    legalName
    industryType	
  }
}
```
The server should return details about your sandbox test company.

### Step 6: Set up authorization in Insomnia
In the query window, set the OAuth2.0 environment variables: 

1. Select the **OAuth 2.0** tab. 
2. From the **Grant type** dropdown, select **Authorization code**.
3. In the Authorization URL field, enter **Authurl**.
4. In the Access Token URL field, enter **AccessTokenUrl**.
5. In the Client ID field, enter **ClientId**.
6. In the Client Secret field, enter **ClientSecret**.
7. In the Redirect URL field, enter **RedirectUrl**.
8. Select the **Enabled** checkbox. 

![](/intuit-api-docs/assets/images/oauth2.png)

### Step 7: Send a test query

Everything is ready to go. Select **Send** to send the test query. 

The first time you send a query, Insomnia will ask you to sign in to your sandbox QuickBooks Online company. Follow the on-screen steps to connect them.

You'll see access tokens in the **OAuth 2.0** tab. Use these to test code and queries in Insomnia.

<br>

## Set up and test with GraphiQL 

### Step 1: Get GraphiQL

Go to GitHub to [download and install GraphiQL](https://github.com/skevy/graphiql-app).

### Step 2: Set up OAuth2.0
If you haven't already, [set up OAuth 2.0](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization) for your app. This gives you access tokens to make API calls with GraphiQL.

### Step 3: Create a test query in GraphiQL

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