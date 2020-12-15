---
layout: default
title: Insomnia Setup
nav_order: 1
parent: GraphQL IDE
grand_parent: Getting Started
---

Insomina is the recommend tool to work with GraphQL, the free version is free for ever in great to get started with
* Save and run queries
* Browse schema 
* Import/Export queries for sharing
* [Paid version](https://insomnia.rest/pricing/) has lot more capabilites

## Setup

### Install
[Download the latest version](https://insomnia.rest/download/)

## Setup Environment

Add following environment definition. It will make your requests for readable and allow you manage configuration from one please. You can name this evironment wahtever you like.


```json
{
  "AccesTokenUrl": "https://oauth.platform.intuit.com/oauth2/v1/tokens/bearer",
  "Authurl": "https://appcenter.intuit.com/connect/oauth2",
  "ClientId": <>,
  "ClientSecret": "v7KVeub7Las7CAzmYbry3xq1qXJTYkYvRNeZbGZM",
  "RedirectUrl": "https://insomnia.rest",
  "url": "https://public.api.intuit.com/2020-04/graphql"
}
```
