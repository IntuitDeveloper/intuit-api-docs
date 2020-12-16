
---
layout: default
title: Insomnia Setup
nav_order: 1
parent: GraphQL IDE
grand_parent: Getting Started
---

Insomina is the recommended tool to work with GraphQL.  You can start with the free version and upgrade to the [paid version](https://insomnia.rest/pricing/) as your needs grow. The free version provides all the basic features listed below (or upgrade to the paid version for stronger collaboration):
* Save and run queries
* Browse schema 
* Import/Export queries for sharing
* Integrate with oAuth2

## Setup

## Asumptions

* This tutorial assumes you are working with a production trial company.
* :red_circle: You have created an app in [developer.intuit.com](https://developer.intuit.com) and worked with your partner in Intuit for access to GraphQL APIs

### Install Insomnia
[Download the latest version](https://insomnia.rest/download/). Version *2020.5.2* or higher.

### Setup Environment
Launch Insomnina and configure the following environment definition. This step will setup the URLs to access the APIs and Auth. You will need your application's *clientId* and *clientSecret* from the [developer portal](https://developer.intuit.com/app/developer/qbo/docs/build-your-first-app) to complete this step. Select the "[Manage environments](https://support.insomnia.rest/article/18-environment-variables)" option to setup this config.

```json
{
  "AccesTokenUrl": "https://oauth.platform.intuit.com/oauth2/v1/tokens/bearer",
  "Authurl": "https://appcenter.intuit.com/connect/oauth2",
  "ClientId": "clientId", <---YOUR APP's ClIENTID
  "ClientSecret": "clientSecret", <--YOUR APP's CLIENTSECRET
  "RedirectUrl": "https://insomnia.rest",
  "url": "https://public.api.intuit.com/2020-04/graphql"
}
```

### Create first query
* Launch Insomnia
* Add new request from the left panel
* Use POST method and select the *url* environment variable as value
* Select "GraphQL Query" as query type for first tab.
* Paste following query to retrieve details of the company you are connected to
```json
{
query company {
  company {
    id
    legalName
    industryType	
  }
}
}
```
* Setup Auth. Select OAuth2 tab and setup following configuration.  Values refer to names from environment variables setup above.
```
GRANT TYPE : "Authorization Code"
AUTHORIZATION URL : Authurl
Access Token URL : AccessTokenUrl
CLIENT ID : ClientId
CLIENT SECRET :  ClientSecret
Redirect URL : RedirectUrl
Enabled : <Checked> 
```
After you complete this task the setup will look like this 

![](/intuit-api-docs/assets/images/oauth2.png)

You are now ready to run the query.

### Send first query

* Click "Send" button to run the query. On the first time, you will see these additional prompts
* Insomnia will ask you to login to your QBO company (enter trial company credentials)
* After a successful login, you will be directed to the connection screen, follow the prompt to establish a connection. You are in the process of establishing a connection between your app and a trial QBO connection.
* After successful connection, you will see tokens in the oAuth2 tab of your request in Insomnia

Congratulations!
