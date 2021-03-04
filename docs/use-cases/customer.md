---
layout: default
title: Customer
nav_order: 7
parent: Use Cases
---

## Customer

### API URL

The Customer API allows creation and read operations, and is exposed against a new endpoint. Make a POST request to the endpoint below.

**Endpoint:**

Prod: `https://public.api.intuit.com/2020-04/graphql`

**Required Headers:**

Content-Type: `application/json`

Authorization: OAuth2 authorization header using scope `com.intuit.quickbooks.accounting`.


### Scopes

The Customer API is protected against the existing scope **_com.intuit.quickbooks.accounting_**. This is applicable to `mutation` as well as `query`.

Note: Apps require an onboarding before using the Customer API. 

### API request

_Note: Before making the API call, make sure to generate an OAuth token by sending the scope com.intuit.quickbooks.accounting and send the token in the request header._


### Mutation

This section describes the ability to create a Customer within the Intuit Ecosystem. The `displayName` should have a unique value.

Mutation Query:

```
mutation createCustomer($input: CreateCustomerInput!) {
  createCustomer(customerDetails: $input) {
    id
    firstName
    lastName
    displayName
    companyName
    notes
    website
    email
    phone
    mobile
    fax
    contactMethods {
      type
      primary
      address {
        streetAddress1
        streetAddress2
        city
        state
        country
        zipCode
      }
    }
  }
}
```

Variables:

A Customer has 2 addresses i.e. `BILLING` and `SHIPPING`. If both addresses are the same, include them twice against `contactMethods` with the respective `type`. 

```
{
  "input": {
    "firstName": "Obi-Wan",
    "lastName": "Kenobi",
    "displayName": "Obi-Wan Kenobi",
    "companyName": "Jedi Order",
    "notes": "some notes here",
    "website": "https://intuit.com",
    "email": "obi-wankenobi@intuit.com",
    "phone": "4084129211",
    "mobile": "4084121234",
    "fax": "4084125678",
    "contactMethods": [
      {
        "type": "BILLING",
        "address": {
          "streetAddress1": "2535 Garcia Ave",
          "streetAddress2": null,
          "city": "Mountain View",
          "state": "CA",
          "country": "USA",
          "zipCode": "94043"
        }
      },
      {
        "type": "SHIPPING",
        "address": {
          "streetAddress1": "2525 Garcia Ave",
          "streetAddress2": null,
          "city": "Mountain View",
          "state": "CA",
          "country": "USA",
          "zipCode": "94043"
        }
      }
    ]
  }
}
```

Sample Response:

```
{
  "data": {
    "createCustomer": {
      "id": "djQuMTo5MTMwMzUzMDk0NjEyODE2OjlkNjk5ZTk2MDg:020719710b14487b54c4cb8e00baa9b3cfa55",
      "firstName": "Obi-Wan",
      "lastName": "Kenobi",
      "displayName": "Obi-Wan Kenobi",
      "companyName": "Jedi Order",
      "notes": "some notes here",
      "website": "https://intuit1234.com",
      "email": "obi-wankenobi@intuit.com",
      "phone": "4084129211",
      "mobile": "4084121234",
      "fax": "4084125678",
      "contactMethods": [
        {
          "type": "BILLING",
          "primary": true,
          "address": {
            "streetAddress1": "2535 Garcia Ave",
            "streetAddress2": null,
            "city": "Mountain View",
            "state": "CA",
            "country": "US",
            "zipCode": "94043"
          }
        },
        {
          "type": "SHIPPING",
          "primary": false,
          "address": {
            "streetAddress1": "2525 Garcia Ave",
            "streetAddress2": null,
            "city": "Mountain View",
            "state": "CA",
            "country": "US",
            "zipCode": "94043"
          }
        }
      ]
    }
  }
}
```


### Query

Customer entity can be queried by `id` or `displayName`.


#### Query by ID

Query:

```
query fetchCustomer($id: String!) {
  company {
    customers (filter: {id: {equals: $id}}) {
      nodes {
        id
        firstName
        displayName
        lastName
        notes
        companyName
        website
        email
        phone
        mobile
        fax
        contactMethods {
          type
          primary
          address {
            streetAddress1
            streetAddress2
            city
            state
            country 
            zipCode
          }
        }
      }
    }
  }
}
```

Variables:

```
{
  "id": "djQuMTo5MTMwMzUzMDk0NjEyODE2OjlkNjk5ZTk2MDg:0020719710b14487b54c4cb8e00baa9b3cfa55"
}
```

Sample Response:

```
{
  "data": {
    "company": {
      "customers": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzUzMDk0NjEyODE2OjlkNjk5ZTk2MDg:0020719710b14487b54c4cb8e00baa9b3cfa55",
            "firstName": "Obi-Wan",
            "displayName": "Obi-Wan Kenobi",
            "lastName": "Kenobi",
            "notes": "some notes here",
            "companyName": "Jedi Order",
            "website": "https://intuit1234.com",
            "email": "obi-wankenobi@intuit.com",
            "phone": "4084129211",
            "mobile": "4084121234",
            "fax": "4084125678",
            "contactMethods": [
              {
                "type": "BILLING",
                "primary": true,
                "address": {
                  "streetAddress1": "2535 Garcia Ave",
                  "streetAddress2": null,
                  "city": "Mountain View",
                  "state": "CA",
                  "country": "US",
                  "zipCode": "94043"
                }
              },
              {
                "type": "SHIPPING",
                "primary": false,
                "address": {
                  "streetAddress1": "2525 Garcia Ave",
                  "streetAddress2": null,
                  "city": "Mountain View",
                  "state": "CA",
                  "country": "US",
                  "zipCode": "94043"
                }
              }
            ]
          }
        ]
      }
    }
  }
}
```

#### Query by Name


Query:

```
query fetchCustomerByName($displayName: String!) {
  company {
    customers (filter: {displayName: {equals: $displayName}}) {
      nodes {
        id
        firstName
        displayName
        lastName
        companyName
        notes
        website
        email
        phone
        mobile
        fax
        contactMethods {
          type
          primary
          address {
            streetAddress1
            streetAddress2
            city
            state 
            country
            zipCode 
          }
        }
      }
    }
  }
}
```

Variables:

```
{
  "displayName": "Obi-Wan Kenobi"
}
```


Sample Response:

```
{
  "data": {
    "company": {
      "customers": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzUzMDk0NjEyODE2OjlkNjk5ZTk2MDg:0020719710b14487b54c4cb8e00baa9b3cfa55",
            "firstName": "Obi-Wan",
            "displayName": "Obi-Wan Kenobi",
            "lastName": "Kenobi",
            "notes": "some notes here",
            "companyName": "Jedi Order",
            "website": "https://intuit1234.com",
            "email": "obi-wankenobi@intuit.com",
            "phone": "4084129211",
            "mobile": "4084121234",
            "fax": "4084125678",
            "contactMethods": [
              {
                "type": "BILLING",
                "primary": true,
                "address": {
                  "streetAddress1": "2535 Garcia Ave",
                  "streetAddress2": null,
                  "city": "Mountain View",
                  "state": "CA",
                  "country": "US",
                  "zipCode": "94043"
                }
              },
              {
                "type": "SHIPPING",
                "primary": false,
                "address": {
                  "streetAddress1": "2525 Garcia Ave",
                  "streetAddress2": null,
                  "city": "Mountain View",
                  "state": "CA",
                  "country": "US",
                  "zipCode": "94043"
                }
              }
            ]
          }
        ]
      }
    }
  }
}
```