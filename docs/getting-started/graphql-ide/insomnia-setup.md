---
layout: default
title: Insomnia Setup
nav_order: 1
parent: GraphQL IDE
grand_parent: Getting Started
---

Insomina is the recommend tool to work with GraphQL, you can start with the free version and upgrade to [Paid version](https://insomnia.rest/pricing/) as you needs expand. The free version provide enough to start
* Save and run queries
* Browse schema 
* Import/Export queries for sharing
* Integrate with oAuth2

## Setup

### Install
[Download the latest version](https://insomnia.rest/download/)

## Setup Environment

Add following environment definition. You will need to download the clientId and clientSecret for your production application from the developortal and replace before saving. Instructions avialable from [here](https://developer.intuit.com/app/developer/qbo/docs/build-your-first-app). This tutorial assume you are working with a production trial company.

```json
{
  "AccesTokenUrl": "https://oauth.platform.intuit.com/oauth2/v1/tokens/bearer",
  "Authurl": "https://appcenter.intuit.com/connect/oauth2",
  "ClientId": "clientId", <---NEEDS REPLACEMENT
  "ClientSecret": "clientSecret", <--NEEDS REPLACEMENT
  "RedirectUrl": "https://insomnia.rest",
  "url": "https://public.api.intuit.com/2020-04/graphql"
}
```

## Create query

* Make sure environment create above is selected
* Add new request
* Use POST method and select the url environment variable as value
* Select GraphQL Query as query time
* Paste following query get deatils of the company you are connected to

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
* Setup auth. select oAuth2 and setup following configuration.  Values refer to names from environment variable
```
GRANT TYPE : "Authorization Code"
AUTHORIZATION URL : Authurl
Access Token URL : AccessTokenUrl
CLIENT ID : ClientId
CLIENT SECRENT :  ClientSecret
Redirect URL : RedirectUrl
Enabled : <Select> 
```

After you complete this task the setup will look like this 

![Insomnia oAuth2 tab](/assets/images/oauth2.png)

You are now ready to run the query , Click the "Send" button to run.
Insomnia will ask you to login to your QBO company (enter trial company credentials)
after a successful login, you will be directed to the connection screen, follow the prompt to establish connection.
After successful connection you will see tokens in the oAuth2 tab of your request in Insomnia

Congratulations! you are now ready to run the request.

Clone the request above for new requests.


