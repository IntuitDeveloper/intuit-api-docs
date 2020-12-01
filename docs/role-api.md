<!-- Copy and paste the converted output. -->

<!-----
NEW: Check the "Suppress top comment" option to remove this info from the output.

Conversion time: 0.68 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β29
* Tue Dec 01 2020 13:22:42 GMT-0800 (PST)
* Source doc: Role API (copy)
* Tables are currently converted to HTML tables.
----->



### Role API:

This document provides technical details for using the new Role API to retrieve user role information in the context of a given company.


### API URL:

Role API is exposed under a new endpoint. Make a POST request to the endpoint below.

**Endpoint:**

Prod: [https://public.api.intuit.com/2020-04/graphql](https://public.api.intuit.com/2020-04/graphql)   

E2E: [https://public-e2e.api.intuit.com/2020-04/graphql](https://public-e2e.api.intuit.com/2020-04/graphql)   

**Required Headers:**

Content-Type: application/json

Authorization: OAuth2 authorization header using new scope.


### Scopes:

User role data is protected under a new scope **_com.intuit.identity.user.roles.read_**. For apps that are already using the internal Role API, we will honor the tokens that were generated using **_com.intuit.identity.accounts.restricted_** scope to support their existing customers.



*   For existing customers - Continue to use the tokens generated using **_com.intuit.identity.accounts.restricted_** scope.
*   For new customers - Use the following scope **_com.intuit.identity.user.roles.read_.**

Note: App’s also should be onboarded to the new scope before they can start using it. 


### API request:

_Note: Before making the API call, make sure to generate Oauth token by sending the scope com.intuit.identity.user.roles.read and send the token in the request header._


#### Queries:


##### Request user role for a realm
```
 {

  user{

  role (realmId: "9130349878530396") {

    type

    status

    hasPayroll

  }

  }

}
```

Sample Response

```
{

  "data": {

    "user": {

      "role": {

        "type": "ADMIN",

        "status": "ACTIVE",

        "hasPayroll": true

      }

    }

  }

}
```


##### Request user role for an invalid realm

```
 {

  user{

  role (realmId: "9130349878530397") {

    type

    status

    hasPayroll

  }

  }

}
```

Sample Response

```
{

 "errors": [

   {

     "message": "User id not part of the realm!",

     "locations": [

       {

         "line": 3,

         "column": 3

       }

     ],

     "path": [],

     "extensions": {

       "code": "VAL-1002",

       "innerMessage": "User id not part of the realm!",

       "classification": "VALIDATION_ERROR"

     }

   }

 ]

}
```


### Description of Fields:

*Note: Can share schema file if needed.*


<table>
  <tr>
   <td>
   </td>
   <td><strong>Field</strong>
   </td>
   <td><strong>DataType</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>role
   </td>
   <td>realmId
<p>
(required)
   </td>
   <td>String
   </td>
   <td>Company id for which the user role is needed
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>type
   </td>
   <td>Enum - ADMIN, EMPLOYEE
   </td>
   <td>Indicates the role type for the user such as ADMIN or EMPLOYEE
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>status
   </td>
   <td>Enum - ACTIVE, INACTIVE
   </td>
   <td>Indicates user’s status within the company such as ACTIVE or INACTIVE
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>hasPayroll
   </td>
   <td>Boolean
   </td>
   <td>Indicates if user has payroll access
   </td>
  </tr>
</table>

