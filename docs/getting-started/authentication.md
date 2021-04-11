---
layout: default
title: Authentication
nav_order: 1
parent: Getting Started
---

# Set up and authenticate your app

Let's get started. Intuit Ecosystem API gives you incredible flexibility to build creative solutions around key business problems. You can create client or server apps from the ground up, or [start with common use cases](https://intuitdeveloper.github.io/intuit-api-docs/docs/use-cases/). 

Here's what you need to get up and running.

## Step 1: Get to know the QuickBooks API platform
Already familiar with Intuit Ecosystem API and GraphQL? Feel free to skip this section. 

If you're new, check out these resources so you can develop with confidence:

* [Learn about Intuit Ecosystem API](https://intuitdeveloper.github.io/intuit-api-docs/docs/faq/graphql-vs-rest/)
* [Learn about GraphQL](https://intuitdeveloper.github.io/intuit-api-docs/docs/graphql-concepts/)
* [Learn basic accounting concepts](https://developer.intuit.com/app/developer/qbo/docs/concepts)

## Step 2: Get a QuickBooks Online test company

If you don't have one already, create a QuickBooks Online company to test code with as you develop. 
 
Your test company may need specific features. Will your app use Payroll data? Or fetch payment info? Reach out to your Intuit point of contact so we can get you these features.

## Step 3: Get familiar with data scopes

Intuit Ecosystem API lets developers limit the scope of data. Instead of broad permissions, you set granular permissions so apps only focus on specific data-sets. This minimizes payloads and potentially improves performance. 
 
[Review the current scopes](https://intuitdeveloper.github.io/intuit-api-docs/docs/getting-started/scopes/) and pick the ones that are relevant for your users. You'll set the scope later on during the authentication process.

## Step 4: Create your app on the Intuit Developer Portal

1. [Sign in to (or sign up for)](https://developer.intuit.com/) your developer account.
2. Select the **Dashboard** tab on the toolbar. 
3. Select **+ Create an app**. 
4. Follow the on-screen steps. 

This is the first step in the authorization process. When you're done, reach out to your Intuit point of contact so we can onboard it to the Intuit Ecosystem API platform.

## Step 5: Authenticate your app
All apps need access tokens to connect to our API servers. Intuit uses the [OAuth 2.0 protocol](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0). 

Get your app's credentials: 
1. [Sign in to (or sign up for)](https://developer.intuit.com/) your developer account.
2. Select the **Dashboard** tab on the toolbar.
3. Select and open your app. 
4. If you're starting with a sandbox environment, go to the **Development** section and select **Keys & OAuth**. If you're authenticating a production app, go to the **Production** section and select **Keys & OAuth**.
5. Copy the **Client ID** and **Client Secret**. 

Use the Client ID and Client Secret to [set up OAuth2.0](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0). This process grants access tokens so your app can make requests and get responses from our servers.

| **Tip**: Want to try the authentication process with demo code? Check out the [OAuth 2.0 playground](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0-playground). |

## Step 6: Test GraphQL queries

Use a [GraphQL Integrated Developer Environment (IDE)](https://intuitdeveloper.github.io/intuit-api-docs/docs/getting-started/graphql-ide/) to test queries during development. You can use Insomnia or GraphiQL.

## Step 7: Develop your app

Now your app is onboarded and authenticated. You have everything you need to build and test queries!

Check out [GraphQL best practices](https://intuitdeveloper.github.io/intuit-api-docs/docs/faq/best-practices/) to develop fast, robust, and reliable apps.