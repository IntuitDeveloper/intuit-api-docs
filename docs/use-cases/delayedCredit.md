---
layout: default
title: Delayed Credit
nav_order: 5
parent: Use Cases
---

## Delayed Credit

The APIs related to the Delayed Credit entity allow you to manage delayed credits for your customer that they can use in the future.
Instead of a refund, you can give your customer a credit that they can use to reduce the balance on their next invoice.
The DelayedCredit API provides support for create, read, update and delete operations.

### Operations for DelayedCredit entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the accounting scope **[com.intuit.quickbooks.accounting]** for the authorization header 

### Sample query body

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the delayedCredit entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an DelayedCredit by Id):
```
query fetchDelayedCredit($id: String!) {
  company {
    delayedCredits(filter: {id: {equals: $id}}) {
      pageInfo {
        hasNextPage
        hasPreviousPage
        startCursor
        endCursor
      }
      nodes {
        id
        metadata {
          entityVersion
        }
        amount
        class {
          id
          name
        }
        currency {
          name
          currency
          symbol
          exchangeRate
        }
        customer {
          id
          displayName
        }
        customerMemo
        itemLines {
          sequence
          description
          serviceDate
          item {
            id
            name
          }
          class {
            id
            name
          }
          amount
          account {
            id
            name
            fullyQualifiedName
          }
          quantity
          unitPrice
          tax {
            taxAmount
            taxable
            taxGroup {
              id
              name
              code
              description
              saleRates {
                taxRate {
                  id
                  name
                  description
                  rate
                  startDate
                  endDate
                }
              }
              purchaseRates {
                taxRate {
                  id
                  name
                  description
                  rate
                  startDate
                  endDate
                }
              }
            }
          }
        }
        location {
          id
          name
        }
       
        privateMemo
        referenceNumber
       
        transactionDate
        voided
      }
    }
  }
}
```

Variables:

```
{
  "id": "djQuMTo5MTMwMzUzOTY3NzQ0NjY2OjgwMjcxZWRkOGE:209"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "delayedCredits": {
        "pageInfo": {
          "hasNextPage": false,
          "hasPreviousPage": false,
          "startCursor": "c2ltcGxlLWN1cnNvcjA=",
          "endCursor": "c2ltcGxlLWN1cnNvcjA="
        },
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:209",
            "metadata": {
              "entityVersion": "0"
            },
            "amount": -100.00,
            "class": null,
            "currency": {
              "name": null,
              "currency": "USD",
              "symbol": "$",
              "exchangeRate": 1.00
            },
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:31",
              "displayName": "My sample project"
            },
            "customerMemo": null,
            "itemLines": [
              {
                "sequence": "1",
                "description": "test item description",
                "serviceDate": "2021-09-08",
                "item": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4",
                  "name": "Test service"
                },
                "class": null,
                "amount": 100.00,
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
                  "name": "Services",
                  "fullyQualifiedName": null
                },
                "quantity": 2,
                "unitPrice": null,
                "tax": {
                  "taxAmount": null,
                  "taxable": false,
                  "taxGroup": null
                }
              }
            ],
            "location": null,
            "privateMemo": "test private memo",
            "referenceNumber": null,
            "transactionDate": "2021-09-10",
            "voided": false
          }
        ]
      }
    }
  }
}
```

## Filter support:

You can choose to **query by id** (as shown above) or query for all delayed credits by removing the filter.

### Create mutation
 
Mutation:
 
```
mutation createDelayedCredit($input: CreateDelayedCreditInput!) {
  createDelayedCredit(delayedCredit: $input) {
    id
    __typename
    id
    metadata {
      entityVersion
    }
    amount
    class {
      id
      name
    }
    currency {
      name
      currency
      symbol
      exchangeRate
    }
    customer {
      id
      displayName
    }
    customerMemo
    itemLines {
      sequence
      description
      serviceDate
      item {
        id
        name
      }
      class {
        id
        name
      }
      amount
      account {
        id
        name
        fullyQualifiedName
      }
      quantity
      unitPrice
      tax {
        taxAmount
        taxable
        taxGroup {
          id
          name
          code
          description
          saleRates {
            taxRate {
              id
              name
              description
              rate
              startDate
              endDate
            }
          }
          purchaseRates {
            taxRate {
              id
              name
              description
              rate
              startDate
              endDate
            }
          }
        }
      }
    }
    location {
      id
      name
    }
    privateMemo
    referenceNumber
    transactionDate
    voided
  }
}
```
 
Sample Variables: 
``` 
{
  "input": {
    "transactionDate": "2021-09-10",
    "customer": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:31"
    },
    "customerMemo": "test customer memo",
    "privateMemo": "test private memo",
    "itemLines": [
      {
        "serviceDate": "2021-09-08",
        "amount": "100.00",
        "account": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5"
        },
        "item": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4"
        },
        "description": "test item description",
        "quantity": "2"
      }
    ]
  }
}
```    

Sample response:
```
{
  "data": {
    "createDelayedCredit": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:222",
      "__typename": "DelayedCredit",
      "metadata": {
        "entityVersion": "0"
      },
      "amount": -100.00,
      "class": null,
      "currency": {
        "name": null,
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:31",
        "displayName": "Project created from API new9"
      },
      "customerMemo": null,
      "itemLines": [
        {
          "sequence": "1",
          "description": "test item description",
          "serviceDate": "2021-09-08",
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4",
            "name": "Test service"
          },
          "class": null,
          "amount": 100.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
            "name": "Services",
            "fullyQualifiedName": null
          },
          "quantity": 2,
          "unitPrice": null,
          "tax": {
            "taxAmount": null,
            "taxable": false,
            "taxGroup": null
          }
        }
      ],
      "location": null,
      "privateMemo": "test private memo",
      "referenceNumber": null,
      "transactionDate": "2021-09-10",
      "voided": false
    }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updateDelayedCredit($input: UpdateDelayedCreditInput!) {
  updateDelayedCredit(delayedCredit: $input) {
    id
    __typename
    id
    metadata {
      entityVersion
    }
    amount
    class {
      id
      name
    }
    currency {
      name
      currency
      symbol
      exchangeRate
    }
    customerMemo
    customer {
      id
      displayName
      firstName
      lastName
    }
    customerMemo
    discount {
      amount {
        percentage
        value
      }
      applyTaxAfterDiscount
    }
    emailDeliveryInfo {
      to
      cc
      bcc
    }
    itemLines {
      sequence
      description
      serviceDate
      item {
        id
        name
      }
      class {
        id
        name
      }
      amount
      account {
        id
        name
        fullyQualifiedName
      }
      quantity
      unitPrice
      tax {
        taxAmount
        taxable
        taxGroup {
          id
          name
          code
          description
          saleRates {
            taxRate {
              id
              name
              description
              rate
              startDate
              endDate
            }
          }
          purchaseRates {
            taxRate {
              id
              name
              description
              rate
              startDate
              endDate
            }
          }
        }
      }
    }
    location {
      id
      name
    }
    payment {
      paymentMethod {
        id
        name
        type
      }
    }
    privateMemo
    referenceNumber
    shipping {
      shipDate
      shipVia
      shipAddress {
        freeFormAddressLine
      }
      shippingAmount
      shipFromAddress {
        freeFormAddressLine
      }
      trackingNumber
      tax {
        taxAmount
      }
    }
    tax {
      totalTaxAmount
      taxable
      taxDetails {
        taxRate {
          id
          name
          description
          startDate
          endDate
          rate
        }
        taxAmount
        taxableAmount
      }
      taxGroup {
        id
        name
        description
        code
        saleRates {
          taxRate {
            id
            name
            description
            startDate
            endDate
            rate
          }
        }
        purchaseRates {
          taxRate {
            id
            name
            description
            startDate
            endDate
            rate
          }
        }
      }
    }
    transactionDate
    voided
  }
}
```

Required fields:
- id: ID of an existing delayedCredit
- metadata: you need to provide the entity version returned from a previous create/update/read operation. 

Variables:

```
{
	"input": {
		"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:124",
		"metadata": {
			"entityVersion": "0"
		},
		"transactionDate": "2021-09-10",
		"customer": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:31"
		},
		"customerMemo": "test customer memo",
		"privateMemo": "test private memo",
		"itemLines": [
			{
				"serviceDate": "2021-09-08",
				"amount": "100.00",
				"account": {
					"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5"
				},
				"item": {
					"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4"
				},
				"description": "test item description",
				"quantity": "2"
			}
		]
	}
}
```

Response:
```
{
  "data": {
    "updateDelayedCredit": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:124",
      "__typename": "DelayedCredit",
      "metadata": {
        "entityVersion": "1"
      },
      "amount": -100.00,
      "class": null,
      "currency": {
        "name": null,
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:31",
        "displayName": "Project created from API new9"
      },
      "customerMemo": null,
      "discount": null,
      "emailDeliveryInfo": null,
      "itemLines": [
        {
          "sequence": "2",
          "description": "test item description",
          "serviceDate": "2021-09-08",
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4",
            "name": "Test service"
          },
          "class": null,
          "amount": 100.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
            "name": "Services",
            "fullyQualifiedName": null
          },
          "quantity": 2,
          "unitPrice": null,
          "tax": {
            "taxAmount": null,
            "taxable": false,
            "taxGroup": null
          }
        }
      ],
      "location": null,
      "payment": {
        "paymentMethod": null
      },
      "privateMemo": "test private memo",
      "referenceNumber": null,
      "shipping": null,
      "tax": {
        "totalTaxAmount": null,
        "taxable": null,
        "taxDetails": [],
        "taxGroup": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU5MjRiN2U1YjI:3",
          "name": "8dccb28d4e8c2ee980e28d4b1d3ab5d8812b411d3603c564d4bd09e7b3f395e7",
          "description": "CA-Santa Clara-Santa Clara",
          "code": "8dccb28d4e8c2ee980e28d4b1d3ab5d8812b411d3603c564d4bd09e7b3f395e7",
          "saleRates": [
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:3",
                "name": "California State",
                "description": "ST",
                "startDate": "1970-01-01",
                "endDate": null,
                "rate": "6.25%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:4",
                "name": "California, Santa Clara County",
                "description": "ST",
                "startDate": "1970-01-01",
                "endDate": null,
                "rate": "1%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:5",
                "name": "California, Santa Clara County District",
                "description": "ST",
                "startDate": "1970-01-01",
                "endDate": null,
                "rate": "1.875%"
              }
            }
          ],
          "purchaseRates": []
        }
      },
      "transactionDate": "2021-09-10",
      "voided": false
    }
  }
}
```

### Delete Mutation

Mutation:

``` 
mutation deleteDelayedCredit($input: ID!) {
  deleteDelayedCredit(id: $input){
    id
    success
  }
}
```

Required fields:
- id: ID of an existing delayedCredit

Variables:
``` 
{
  "input": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:124"
}
```

Response:
```
{
  "data": {
    "deleteDelayedCredit": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:124",
      "success": true
    }
  }
}
```