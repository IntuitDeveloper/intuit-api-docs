---
layout: default
title: User Role
nav_order: 1
parent: Use Cases
---

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

# Build apps around user roles

Your app can call the user role entity to get [basic info about users](https://quickbooks.intuit.com/learn-support/en-us/set-up-users/user-types-in-quickbooks-online/00/186238) who are part of a QuickBooks Online company file. 

The user role entity tells you if users are admins or employees, active or inactive, and have access to features like Intuit or QuickBooks Payroll. 

This also lets you build features around role-specific workflows. Since your app knows each user's role, it also knows if they have permission to do certain tasks, like run payroll. 

---

## Step 1: Set up your app in the Intuit Developer Portal

If you haven't already, [get a QuickBooks Online sandbox company](../../getting-started/authentication/) for testing and [create your app](../../getting-started/authentication/).

<br>

## Step 2: Set your app's scopes

Intuit Ecosystem API [uses scopes to limit the type of data](../../getting-started/scopes/) your app can access. You'll set the scope when you create your app.

For user role features, use these scopes:
* **com.intuit.identity.user.roles.read**

<table>
  <tr>
   <td><strong>Note</strong>: If your app is using the previous user role scope (<strong>com.intuit.identity.accounts.restricted</strong>), you can keep using it. We'll accept tokens for this scope so you can continue supporting your current users.</td>
   </tr>
</table>

**Note**: Apps need to be onboarded to the new scope before they can start using it. 

<br>

## Step 3: Get your app's credentials

1. [Sign in](https://developer.intuit.com/app/developer/myapps) to your developer account.
2. Select the **Dashboard link** on the toolbar. 
3. Select and open your app. 
4. In the **Production** section, select **Keys & OAuth**. 
5. Copy the **Client ID** and **Client Secret**. 

<br>

## Step 4: Authorize your app

If you haven't already, use your Client ID, Client Secret, and scopes to [set up OAuth 2.0](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0). 

<br>

## Step 5: Create a query for user role info

For this query, we'll use the following entities and fields:

* **User role**

<table>
  <tr>
   <td><strong>Field</strong>
   </td>
   <td><strong>DataType</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>realmId
(*Required)
   </td>
   <td>String
   </td>
   <td>The company ID of the QuickBooks company the user belongs to.
   </td>
  </tr>
  <tr>
   <td>type
   </td>
   <td>Enum - ADMIN, EMPLOYEE
   </td>
   <td>The user's level, "Admin" or "Employee"
   </td>
  </tr>
  <tr>
   <td>status
   </td>
   <td>Enum - ACTIVE, INACTIVE
   </td>
   <td>The employee's status, "Active" or "Inactive"
   </td>
  </tr>
  <tr>
   <td>hasPayroll
   </td>
   <td>Boolean
   </td>
   <td>Indicates if the user has payroll access
   </td>
  </tr>
</table>

<br> 

### Endpoints

* For production apps: **[https://public.api.intuit.com/2020-04/graphql](https://public.api.intuit.com/2020-04/graphql)**   
* For sandbox environments and testing: **[https://public-e2e.api.intuit.com/2020-04/graphql](https://public-e2e.api.intuit.com/2020-04/graphql)**   
<br>

### Query header
* `Content-Type`: **application/json**
* `Authorization`: Use the user role scope **[com.intuit.identity.user.roles.read]** to get an access token

After [generating an OAuth token](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0), put it in the request header. 

<br>

### Query body

Here's a basic query to get user role info: 
```
 {
  user {
    role (realmId: "9130349878530396") {
      type
      status
      hasPayroll
    }
  }
}
```
You can include all of these fields, or add fields, depending on your app's needs.

<table>
<tr>
<td><Strong>Note</strong>: The <Strong>realmID</strong> field is the 16 digit company ID of the QuickBooks Online company you're requesting user role info for.  
</td>
</tr>
</table>

### Sample server response

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
The `type` and `status` field values define the user's `role`. You'll only see fields like `hasPayroll` if these features are active for the QuickBooks company. 

<br>

##### Request user role for an invalid realm

If the `realmID` is incorrect, you'll get the following response: 

```
 {
  user {
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
Make sure the `realmID` is for the correct end-users' QuickBooks Online company ID. 

<br>

## Step 6: Go live with your app

Follow these steps when you're [ready to publish your app](https://developer.intuit.com/app/developer/qbo/docs/go-live). You don't need to make it publicly available, but you need to publish it so it's active.  
