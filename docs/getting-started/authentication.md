---
layout: default
title: Authenticate your app
nav_order: 1
parent: Getting Started
---

# Set up and authorize your app

Let's get started. Intuit Ecosystem API gives you incredible flexibility to build creative solutions around key business problems. You can create client or server apps from the ground up, or [start with common use cases](../../use-cases/). 

Here's what you need to get up and running.

## Step 1: Get to know the QuickBooks API platform
Already familiar with Intuit Ecosystem API and GraphQL? Feel free to skip this section. 

If you're new, check out these resources so you can develop with confidence:

* [Learn about Intuit Ecosystem API](../../faq/graphql-vs-rest/)
* [Learn about GraphQL](../../graphql-concepts/)
* [Learn basic accounting concepts](https://developer.intuit.com/app/developer/qbo/docs/concepts)

## Step 2: Set up your developer account 

Go to the Intuit Developer Portal and [create a developer account](https://developer.intuit.com/app/developer/myapps). 

## Step 3: Create a sandbox  company

If you don't have one already, create a sandbox QuickBooks Online company to test code as you develop. 
 
Your test company may need specific features. Will your app use Payroll data? Or fetch payment info? Reach out to your Intuit point of contact so we can get you these features.

## Step 4: Create your app on the Intuit Developer Portal

1. [Sign in to](https://developer.intuit.com/) your developer account.
2. Select the **Dashboard** tab on the toolbar. 
3. Select **+ Create an app**. 
4. Follow the on-screen steps. 

When you're done, reach out to your Intuit point of contact so we can onboard it to the Intuit Ecosystem API platform.

## Step 5: Get familiar with data scopes

Intuit Ecosystem API lets developers limit the scope of data. Instead of broad permissions, you set granular permissions so apps only focus on specific data-sets. This minimizes payloads and potentially improves performance. 
 
[Review the current scopes](https://intuitdeveloper.github.io/intuit-api-docs/docs/getting-started/scopes/). Pick the ones that are relevant for your users. You'll set the scopes when you authorize your app.

## Step 6: Authorize your app
All apps need access tokens to connect to our API servers. Intuit uses the [OAuth 2.0 protocol](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0). 

To start, you need to get your app's credentials: 
1. [Sign in to (or sign up for)](https://developer.intuit.com/) your developer account.
2. Select the **Dashboard** tab on the toolbar.
3. Select and open your app. 
4. If you're starting with a sandbox environment, go to the **Development** section and select **Keys & OAuth**. If you're authorizing a production app, go to the **Production** section and select **Keys & OAuth**.
5. Copy the **Client ID** and **Client Secret**. 

Use the Client ID and Client Secret to [set up OAuth2.0](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0). 

> **Tip**: Want to try the authentication process with demo code? Check out the [OAuth 2.0 playground](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0-playground).

## Step 7: Get tools to test GraphQL queries

We suggest using a [GraphQL Integrated Developer Environment (IDE)](https://intuitdeveloper.github.io/intuit-api-docs/docs/getting-started/graphql-ide/), like Insomnia or GraphiQL, to test queries during development.

## Step 8: Develop your app

Your app is onboarded and authorized. You have everything you need to build and test queries!

Check out [GraphQL best practices](../../faq/best-practices/) to develop fast, robust, and reliable apps.
