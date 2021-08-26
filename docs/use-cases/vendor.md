---
layout: default
title: Vendor
nav_order: 5
parent: Use Cases
---

## Vendor

The Vendor entity represents the seller from whom your company purchases any service or product.
The Vendor API provides support for create, read, update and delete operations.

### Operations for Vendor entity

-   Read - Query (POST)
-   Create - Mutation (POST)
-   Update - Mutation (POST)
-   Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   User the vendor scope **[com.intuit.quickbooks.accounting]** for the authorization header 

### Sample query body

Do an [introspection query](../../graphql-concepts/introspection)  to see the current schema for the vendor entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read by Id):

```
query fetchVendor($id: String!) {
  company {
    id
    companyName
    vendors(filter: { id: { equals: $id } }) {
      nodes {
        id
        metadata {
          entityVersion
        }
        firstName
        displayName
        lastName
        active
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
          active
          address {
            streetAddress1
            streetAddress2
            city
            zipCode
            state
            county
            country
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
	"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:00207154e0ecf1179b48fe89eeb3bc27d988bf"
}
```

Response:

```
{
  "data": {
    "createVendor": {
      "id": "djQuMTo5MTMwMzUzOTY3NzQ0NjY2OjlkNjk5ZTk2MDg:002071113eaac04abc4492b31de9910f9ca726",
      "active": true,
      "metadata": {
        "entityVersion": "0"
      },
      "firstName": "Obiwan",
      "lastName": "Kenobi",
      "displayName": "obiwan-kenobi",
      "companyName": "Intuit",
      "notes": "some notes here",
      "website": "https://intuit.com",
      "email": "okenobi@test.com",
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
            "zipCode": "94043",
            "country": "US"
          }
        }
      ]
    }
  }
```

### Filter support:

You can choose to **query by id** (as shown above) or by **displayName** by changing the filter for the query as follows -

Sample query (Read by displayName):

``` 
query fetchVendor($displayName: String!) {
  company {
    id
    companyName
    vendors (filter: { displayName: { equals: $displayName } }) {
      nodes {
        id
        metadata {
          entityVersion
        }
        firstName
        displayName
        lastName
        active
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
          active
          address {
            streetAddress1
            streetAddress2
            city
            zipCode
            state
            county
            country
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
	"displayName": "LukeSkywalker-1"
}
```

Response:

``` 
{
  "data": {
    "company": {
      "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjI5NjA1NzY1ZDc:9130352325758296",
      "companyName": "hubspot e2e",
      "vendors": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071113eaac04abc4492b31de9910f9ca726",
            "metadata": {
              "entityVersion": "1"
            },
            "firstName": "Luke",
            "displayName": "LukeSkywalker-1",
            "lastName": "Skywalker",
            "active": true,
            "companyName": "Jedi Order",
            "notes": null,
            "website": "https://intuit.com",
            "email": "luke-skywalker@intuit.com",
            "phone": "4084129211",
            "mobile": "4084121234",
            "fax": "4084125678",
            "contactMethods": [
              {
                "type": "BILLING",
                "primary": true,
                "active": null,
                "address": {
                  "streetAddress1": "2000 Garcia Ave",
                  "streetAddress2": null,
                  "city": "Mountain View",
                  "zipCode": "94043",
                  "state": "CA",
                  "county": "Santa Clara County",
                  "country": "US"
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
### Create mutation

Mutation:

```
mutation createVendor($input: CreateVendorInput!) {
 createVendor(vendorDetails: $input) {
   id
   active
   metadata {
     entityVersion
   }
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
       zipCode
       country
     }
   }
 }
}
```

Variables: 

```
{
  "operationName": "createVendor",
  "variables": {
    "input": {
      "firstName": "Luke",
      "lastName": "Skywalker",
      "displayName": "LukeSkywalker-1",
      "companyName": "Jedi Order",
      "notes": "some notes here",
      "website": "https://intuit.com",
      "email": "luke-skywalker@intuit.com",
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
            "zipCode": "94043",
            "state": "CA",
            "country": "USA"
          }
        }
      ]
    }
  }
}
```

Sample response:

``` 
{
  "data": {
    "createVendor": {
      "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071113eaac04abc4492b31de9910f9ca726",
      "active": true,
      "metadata": {
        "entityVersion": "0"
      },
      "firstName": "Luke",
      "lastName": "Skywalker",
      "displayName": "LukeSkywalker-1",
      "companyName": "Jedi Order",
      "notes": "some notes here",
      "website": "https://intuit.com",
      "email": "luke-skywalker@intuit.com",
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
            "zipCode": "94043",
            "country": "US"
          }
        }
      ]
    }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updateVendor($input: UpdateVendorInput!) {
  updateVendor(vendorDetails: $input) {
    id
    metadata {
      entityVersion
    }
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
    active
    contactMethods {
      type
      primary
      address {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
  }
}

```
Variables: 

```
{
	"input": {
		"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071113eaac04abc4492b31de9910f9ca726",
		"metadata": {
			"entityVersion": "0"
		},
		"active": true,
		"contactMethods": [
			{
				"type": "BILLING",
				"address": {
					"streetAddress1": "2000 Garcia ave",
					"streetAddress2": null,
					"city": "Mountain View",
					"zipCode": "94043",
					"state": "CA",
					"country": "USA"
				}
			}
		]
	}
}
```

Response:

```
{
  "data": {
    "updateVendor": {
      "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071113eaac04abc4492b31de9910f9ca726",
      "metadata": {
        "entityVersion": "1"
      },
      "firstName": "Luke",
      "lastName": "Skywalker",
      "displayName": "LukeSkywalker-1",
      "companyName": "Jedi Order",
      "notes": "some notes here",
      "website": "https://intuit.com",
      "email": "luke-skywalker@intuit.com",
      "phone": "4084129211",
      "mobile": "4084121234",
      "fax": "4084125678",
      "active": true,
      "contactMethods": [
        {
          "type": "BILLING",
          "primary": true,
          "address": {
            "streetAddress1": "2000 Garcia Ave",
            "streetAddress2": null,
            "city": "Mountain View",
            "state": "CA",
            "zipCode": "94043",
            "country": "US"
          }
        }
      ]
    }
  }
}
```

### Delete Mutation

Mutation:
``` 
mutation updateVendor($input: UpdateVendorInput!) {
  updateVendor(vendorDetails: $input) {
    id
    metadata {
      entityVersion
    }
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
    active
    contactMethods {
      type
      primary
      address {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
  }
}
```

Variables:

``` 
{
	"input": {
		"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071113eaac04abc4492b31de9910f9ca726",
		"metadata": {
			"entityVersion": "1"
		},
		"active": false
	}
}
```

Response:

``` 
{
  "data": {
    "updateVendor": {
      "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071113eaac04abc4492b31de9910f9ca726",
      "metadata": {
        "entityVersion": "2"
      },
      "firstName": "Luke",
      "lastName": "Skywalker",
      "displayName": "LukeSkywalker-1 (deleted)",
      "companyName": "Jedi Order",
      "notes": "some notes here",
      "website": "https://intuit.com",
      "email": "luke-skywalker@intuit.com",
      "phone": "4084129211",
      "mobile": "4084121234",
      "fax": "4084125678",
      "active": false,
      "contactMethods": [
        {
          "type": "BILLING",
          "primary": true,
          "address": {
            "streetAddress1": "2000 Garcia Ave",
            "streetAddress2": null,
            "city": "Mountain View",
            "state": "CA",
            "zipCode": "94043",
            "country": "US"
          }
        }
      ]
    }
  }
}
```
