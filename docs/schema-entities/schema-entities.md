---
layout: default
title: Schema Entities
nav_order: 19
has_children: true
permalink: /docs/schema-entities/
---

# See basic API documentation to help you follow the below steps to release and APP

If you already know what you want to develop, [create custom queries](../graphql-concepts/query/) to build a bespoke experience. 

If you need inspiration, we've got you covered. Or if you don't see what you are looking for, check over in our more detailed [use-cases section.](../use-cases) You can use these guides as a foundation for your app.

## Step 1: Create your app in the Intuit Developer Portal

If you haven’t already, [create your app](../getting-started/authentication/) on the developer portal.

## Step 2: Set your app's scopes

The Intuit Ecosystem API [uses scopes](../getting-started/scopes/) to limit the type of data your app can access. You'll set scopes when you create your app. 

### If you want your app to read or write data

To read QuickBooks Online Payroll data, and write in how much individual employees request for deductions, use the scopes associated with each use-case:


## Step 3: Get your app's credentials

1. [Sign in](https://developer.intuit.com/) to your developer account.
2. Select the **Dashboard** link on the toolbar. 
3. Select and open your app. 
4. In the **Production** section, select **Keys & OAuth**. 
5. Copy the **Client ID** and **Client Secret**. 

## Step 4: Authorize your app

If you haven't already, use your Client ID, Client Secret, and scopes to [set up OAuth 2.0](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0). 


## Step 5: Create and execute queries for your app 

Use the sample queries provided in the respective sections as guides. Introspection can also be very helpful to build queries, with the help of tools such as Insomnia. More information can be found on [this](../graphql-concepts/introspection/) page.

### Endpoints

The endpoint for all queries are listed here : [API endpoints](../getting-started/endpoints/)

## Step 6: Go live with your app

Follow these steps when you're ready to [publish your app](https://developer.intuit.com/app/developer/qbo/docs/go-live). 