---
layout: default
title: Authentication
nav_order: 1
parent: Getting Started
---

## Authentication

To make API calls, you'll need:

1. A QuickBooks company
2. An Intuit application
3. An OAuth 2.0 access token

### 1. QuickBooks company

Depending on your use case (will you be making Payroll API calls?), you'll need a QuickBooks company setup appropriately (with Payroll, for example).  Partners should reach out to their Intuit point-of-contact to get a company set up.

### 2. An Intuit application

You can create an Intuit application at [developer.intuit.com](https://developer.intuit.com).  Partners should work with their Intuit point-of-contact to make sure the application is correctly onboarded to the new Intuit Ecosystem API.

### 3. OAuth 2.0 Access Token

Intuit uses the standard OAuth 2.0 protocol.  For details on OAuth 2.0 at Intuit, refer to [this document](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0).  The [OAuth 2.0 playground](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0-playground) may also be helpful to learn about the OAuth flow.

#### Scopes

In the new Intuit Ecosystem API, there are new additional scopes, beyond the previous high-level "accounting" and "payment" scopes.  For a list of scopes in the new Intuit Ecosystem API, [check here](../scopes).  You'll need to find the scopes relevant for your use case, and make sure to request them when generating the OAuth 2.0 Access Token.