---
layout: default
title: Customer
nav_order: 3
parent: Use Cases
---

# Customer entity

The Customer entity lets apps create and read customer info in QuickBooks Online. It's exposed against a new endpoint.

**Note**: Apps require onboarding before using the Customer API. 

## Operations for the Customer entity

* **Read** - Query (POST)
* **Create** - Mutation (POST)

## Endpoints

Send POST requests to one of these endpoints:

* For production apps: **https://public.api.intuit.com/2020-04/graphql**
* For sandbox environments and testing: **https://public-e2e.api.intuit.com/2020-04/graphql**

## Sample query and mutation header 

* Content-type: `application/json`
* Use the `com.intuit.quickbooks.accounting` scope to generate OAuth tokens for mutations and queries. Put the token in the authorization header

## Use mutations to create customers

Apps can new customers in QuickBooks. The `displayName` field in the mutation should have a unique value.

**Tip**: Do [an introspection query](../../graphql-concepts/introspection/) to see the latest entity schema. 

## Sample mutation body

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

### Variables

Each customer has two addresses: `BILLING` and `SHIPPING`. 

If both addresses are the same, include them twice against `contactMethods` with the respective `type`. 

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

### Sample server response

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


## Use queries to read customers

Here’s are example queries using every possible field. Remember, with GraphQL you only need to query for the fields you need.

Apps can query the Customer entity by `id` or `displayName`.

## Sample query body by ID

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

### Variables

```
{
  "id": "djQuMTo5MTMwMzUzMDk0NjEyODE2OjlkNjk5ZTk2MDg:0020719710b14487b54c4cb8e00baa9b3cfa55"
}
```

### Sample server response

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

## Sample query body by displayName

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

### Variables

```
{
  "displayName": "Obi-Wan Kenobi"
}
```

### Sample server response

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
