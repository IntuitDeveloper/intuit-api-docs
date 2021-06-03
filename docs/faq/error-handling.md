---
layout: default
title: Error Handling
nav_order: 3
parent: FAQ
---

# Fix Intuit Ecosystem API errors

If you ever encounter an error, the Intuit Ecosystem API server returns an error message. These messages give you clues about the issue's source and cause. 

## Step 1: Capture the intuit_tid value
Server responses for gateway and service errors have an `intuit_tid` field in the header. 

Capture this field's value. It will help our support team quickly find and address reported issues.


## Step 2: Identify the error type 

When requests from apps go to our servers, they first pass through a gateway layer. Then they pass through the GraphQL Service layer. Thus, there are two general types: **gateway** errors and **service** errors. 

Review the HTTP Status Code (xxx). This tells you the error type:

* Service errors: **200** or **400**
* Gateway errors: **All other ###**

## Step 3: Fix errors

### Fix gateway errors
Gateway errors are generated when requests hit our server's gateway layer. They apply to the whole request and follow the gateway error resposne format. 

```
HTTP Status Code 401
{
  "code": "AuthenticationFailed",
  "type": "INPUT",
  "message": null,
  "detail": "Malformed bearer token: too short or too long",
  "moreInfo": null
}
```
In the server response, review the following fields:

* HTTP Status Code - Gives you the error code
* `code` - Tells you what went wrong
* `detail` - Tells you what to fix

Many gateway errors are self-explanatory. Some require a bit more digging. For 403 errors, you may need to [adjust code for user roles](../../use-cases/user-role/). For 401 errors, you may need to [update your app's access or refresh tokens](https://developer.intuit.com/app/developer/appdetail/test/keys?appId=djQuMTo6OGQzYmJlYTI3Yg:91ec0282-dc3b-4e2d-b065-5b89a6822e85). 

#### See all gateway errors
```
Status code - Error details
302 - Resource redirect or resource has moved
401 - Unauthenticated access: application authentication failed due to invalid or expired tokens
403 - Forbidden access: authorization specific, application authorization failed due to insufficient user access role
403 - Resource not found: routing error, access or configuration on the  Gateway, or incorrect endpoint requested
405 - Method not allowed: attempt to request other than GET/POST requests
429 - Too many requests: request is throttled as it exceeded the throttle policy.
500 - Internal Server Error: missing POST body or other exceptions within application, or a service outage
502 - Bad Gateway: Infrastructure misconfiguration, propagates response from downstream, or a service outage
503 - Service unavailable: Outage
504 - Service timeout: Outage

```

### Fix ecosystem errors
Service errors are generated when requests hit our server's service layer.

Service errors only apply to a subset of requests, not the entire request. Responses follow the standard GraphQL service format.

#### See all service errors
```
200 - Authorization errors due to incorrect scope, or partial semantic errors
400 - GraphQL validation errors such as invalid or malformed requests and missing variables, or system errors
```

Most service errors are in response to [malformed queries](../../graphql-concepts/query/), parsing problems, validation issues, or [incorrect scopes](../../gettig-started/scopes/). As a result, the server won't authorize the request.

Here's an example of an HTTP status code 400:
```
{
  "errors": [
	{
  	"message": "Syntax error. Unable to parse incoming request",
  	"locations": [
    	{
      	"line": 4,
      	"column": 1
    	}
  	],
  	"extensions": {
    	"code": "VAL-0100",
    	"innerCode": "GRAPHQL_PARSE_FAILED",
    	"innerMessage": "Syntax Error: Expected Name, found }",
    	"classification": "VALIDATION_ERROR"
  	}
	}
  ]
}
```

Here's an example of an HTTP status code 200:

```
{
  "errors": [
	{
  	"message": "Authorization error is detected for this request. Do you have sufficient scope?",
  	"extensions": {
    	"classification": "AUTHORIZATION",
    	"innerMessage": "Access denied; Insufficient Scope",
    	"code": "AHZ-0010"
  	}
	}
  ]
}
```
Here's an example validation error:
```
"errors": [
    {
      "message":  "VAL-0001 Failed to fetch name for account with id#1",
      "locations": [ { "line": 6, "column": 7 } ],
     "path": [ "company", "account", 1, "name" ]
    "extensions": {
        "classification": "VALIDATION_ERROR"
      }
    }
  ]
```
Review the server response and use it as a guide. Each field gives clues for what failed, where, and how to fix it: 

* **Message** — Description of the error.
* **Locations** — Where the error happened in the request.
* **Path** — How to get to the field that caused the error. It's possible to only have one path. Paths follow this format: root object, node, line num, exact field name within the node.
* **Extensions** — Additional info and error codes:
  * **Code** - Specific error code.
  * **Classification** — Broad error category. 

Then take a closer look at the value of `code` of the `extensions` field. It follows the format **XXX-1234**. 

The first 3 letters of the code indicate the error type. 

|Code|Type|Description|
|---|---|---|
|Val|Validation Error|All syntactic (incorrect payload, format), semantic errors, missing data|
|AHZ|Authorization Error|All syntactic (incorrect payload, format), semantic errors, missing dataUser-level, app-level and system level authorization and insufficient scope|
|SYS|System Error|A known error produced by ecosystem components including authentication errors from downstream related to scopes|
|OTH|Other Error|All other unexpected errors|

The following 4 digits identify the source of the error from the underlying services.

<table>
<tr>
<td><Strong>Note</strong>: You may also see additional Extensions.innerCode and Extensions.innerMessage fields. 
<ul>
<li>Extensions.innerCode — Internal unique identifier returned by downstream services (Example: PAY-000008 - payroll). </li>
<li>Extensions.innerMessage — Original internal message from downstream services. </li>  
</td>
</tr>
</table>

## Get additional help 

Need more support? You can [connect with other developers on our community forum](https://help.developer.intuit.com/s/). Or, you can [reach out to our team](https://help.developer.intuit.com/s/contactsupport) and we'll help you get back to developing.

Please give the support team the following:

* Company ID/Realm ID
* GraphQL request and response
* intuit_tid header value from the response header
* extensions.code
* extensions.innerCode
* extensions.innerMessage
