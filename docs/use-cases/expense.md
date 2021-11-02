---
layout: default
title: Expense
nav_order: 10
parent: Use Cases
---

## Expense

The APIs related to the Expense entity allow you to manage expenses for your payees.
A payee can currently be either a customer or a vendor.
The Expense API provides support for create, read, update and delete operations.

### Operations for Expense entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the expense scope **[com.intuit.quickbooks.accounting]** for the authorization header 

### Sample query body

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the Expense entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an Expense by Id):
```
query fetchExpense($id: String) {
  company {
    expenses(filter: {id: {equals: $id}}) {
      nodes {
        id
        metadata {
          entityVersion
        }
        class {
          id
        }
        project {
          id
          name
          customer {
            id
            displayName
          }
          completedDate
          description
          status
        }
        transactionDate
        referenceNumber
        permitNumber
        amount
        memo
        permitNumber
        currency {
          name
          currency
          symbol
          exchangeRate
        }
        payee {
          __typename
          ... on Customer {
            id
            displayName
            email
            phone
            fax
            firstName
            lastName        
            companyName
          }
          ... on Vendor {
            id
            displayName
            email
            phone
            fax
            firstName
            lastName        
            companyName
          }
        }
        account {
          id
          name
          fullyQualifiedName
        }
        payment {
          paymentMethod {
            id
            name
            type
          }
        }
        location {
          id
          name
        }
        customFields {
          fieldId
          fieldName
          value
          fieldDefinition {
            id
            name
            inactive
            associatedEntityTypes {
              type
              subtype
            }
          }
        }        
        itemLines {
          sequence
          amount
          billable
          markup {
            amount
            account {
              id
              name
            }
            percent
          }
          tax {
            taxAmount
            taxable
            taxGroup {
              id
              name
              code
              description
              status
              saleRates {
                taxRate {
                  id
                  name
                  description
                  status
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
                  status
                  startDate
                  endDate
                  rate
                }
              }
            }
          }
          description
          item {
            id
          }
          quantity
          unitPrice
          class {
            id
          }
          customer {
            id
            displayName
            firstName
            lastName
          }
        }
        accountLines {
          sequence
          description
          amount
          class {
            id
            name
          }
          customer {
            id
            displayName
          }
          account {
            id
            name
          }
        }
        tax {
          totalTaxAmount
          taxDetails {
            taxRate {
              id
              name
              description
              status
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
            code
            description
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
      }
      pageInfo {
        hasNextPage
        hasPreviousPage
        startCursor
        endCursor
      }
    }
  }
}
```

Variables:

```
{
	"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:38"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "expenses": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:38",
            "metadata": {
              "entityVersion": "0"
            },
            "class": null,
            "project": null,
            "transactionDate": "2021-08-24",
            "referenceNumber": null,
            "permitNumber": null,
            "amount": 45.00,
            "memo": null,
            "currency": {
              "name": null,
              "currency": "USD",
              "symbol": "$",
              "exchangeRate": 1.00
            },
            "payee": {
              "__typename": "Customer",
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
              "displayName": "Alisha Kamat",
              "email": "test@intuit.com",
              "phone": "(123) 456-7890",
              "fax": null,
              "firstName": "Alisha",
              "lastName": "Kamat",
              "companyName": null
            },
            "account": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:6",
              "name": "Cash",
              "fullyQualifiedName": "Cash"
            },
            "payment": {
              "paymentMethod": null
            },
            "location": null,
            "customFields": [],
            "itemLines": [],
            "accountLines": [
              {
                "sequence": "1",
                "description": null,
                "amount": 45.00,
                "class": null,
                "customer": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                  "displayName": "Alisha Kamat"
                },
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:75",
                  "name": "Website ads"
                }
              }
            ],
            "tax": {
              "totalTaxAmount": null,
              "taxDetails": [],
              "taxGroup": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU5MjRiN2U1YjI:3",
                "name": "8dccb28d4e8c2ee980e28d4b1d3ab5d8812b411d3603c564d4bd09e7b3f395e7",
                "code": "8dccb28d4e8c2ee980e28d4b1d3ab5d8812b411d3603c564d4bd09e7b3f395e7",
                "description": "CA-Santa Clara-Santa Clara",
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
            }
          }
        ],
        "pageInfo": {
          "hasNextPage": false,
          "hasPreviousPage": false,
          "startCursor": "c2ltcGxlLWN1cnNvcjA=",
          "endCursor": "c2ltcGxlLWN1cnNvcjA="
        }
      }
    }
  }
}
```

## Filter support:

You can choose to **query by id** (as shown above) or query for all expenses by removing the filter.

### Create mutation
 
Mutation:
 
```
mutation createExpense($input0: CreateExpenseInput!) {
  createExpense(expense: $input0) {
    id
    metadata {
      entityVersion
    }
    class {
      id
    }
    project {
      id
      name
      customer {
        id
        displayName
      }
      completedDate
      description
      status
    }
    transactionDate
    referenceNumber
    permitNumber
    amount
    memo
    permitNumber
    currency {
      name
      currency
      symbol
      exchangeRate
    }
    payee {
      __typename
      ... on Customer {
        id
        displayName
        email
        phone
        fax
        firstName
        lastName
        companyName
      }
      ... on Vendor {
        id
        displayName
        email
        phone
      }
    }
    account {
      id
      name
      fullyQualifiedName
    }
    payment {
      paymentMethod {
        id
        name
        type
      }
    }
    location {
      id
      name
    }
    customFields {
      fieldId
      fieldName
      value
      fieldDefinition {
        id
        name
        inactive
        associatedEntityTypes {
          type
          subtype
        }
      }
    }
    itemLines {
      sequence
      amount
      billable
      markup {
        amount
        account {
          id
          name
        }
        percent
      }
      tax {
        taxAmount
        taxable
        taxGroup {
          id
          name
          code
          description
          status
          saleRates {
            taxRate {
              id
              name
              description
              status
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
              status
              startDate
              endDate
              rate
            }
          }
        }
      }
      description
      item {
        id
      }
      quantity
      unitPrice
      class {
        id
      }
      customer {
        id
        displayName
        firstName
        lastName
      }
    }
    accountLines {
      sequence
      description
      amount
      class {
        id
        name
      }
      customer {
        id
        displayName
      }
      account {
        id
        name
      }
    }
    tax {
      totalTaxAmount
      taxDetails {
        taxRate {
          id
          name
          description
          status
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
        code
        description
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
  }
}
```
 
Sample Variables: 
``` 
{
	"input0": {
		"transactionDate": "2021-05-26",
		"referenceNumber": "SomeExpenseNumber1",
		"class": {
			"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115"
		},
		"payee": {
			"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:16"
		},
		"account": {
			"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjUxY2VkODUzNmM:45"
		},
		"location": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:1"
		},
		"payment": {
			"paymentMethod": {
				"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjVlNGYwZjQ5Y2Q:2",
				"name": "Check",
				"type": null
			}
		},
		"currency": {
			"name": "USD",
			"currency": "USD",
			"exchangeRate": 1
		},
		"customFields": [
			{
				"fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
				"value": "test cf"
			}
		],
		"permitNumber": "1234",
		"amount": 450,
		"itemLines": [
			{
				"description": "Dummy description",
				"billable": true,
				"markup": {
					"percent": "35%"
				},
				"quantity": 10,
				"unitPrice": 15,
				"amount": 150,
				"item": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjExMmRlNzQ2OTk:4"
				},
				"customer": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071f733ad5d5b53466f913281ea6447128f"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115"
				}
			}
		],
		"accountLines": [
			{
				"description": "Test description",
				"amount": 300,
				"billable": true,
				"markup": {
					"percent": "40%"
				},
				"account": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjUxY2VkODUzNmM:33"
				},
				"customer": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071eb5fc9386d9f48c39544b74cfa2d56e4"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115"
				}
			}
		],
		"memo": "Test Private Memo"
	}
}
```    

Sample response:
```
{
  "data": {
    "createExpense": {
      "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:3672",
      "metadata": {
        "entityVersion": "0"
      },
      "class": null,
      "project": null,
      "transactionDate": "2021-05-26",
      "referenceNumber": "SomeExpenseNumber1",
      "permitNumber": "1234",
      "amount": 450.00,
      "memo": "Test Private Memo",
      "currency": {
        "name": "United States Dollar",
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "payee": {
        "__typename": "Vendor",
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:16",
        "displayName": "Jack Black",
        "email": "jblack@gmail.com",
        "phone": "(650) 123-4569"
      },
      "account": {
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjUxY2VkODUzNmM:45",
        "name": "Checking",
        "fullyQualifiedName": null
      },
      "payment": {
        "paymentMethod": {
          "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjVlNGYwZjQ5Y2Q:2",
          "name": "Check",
          "type": null
        }
      },
      "location": {
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OmJmN2IzNDhiNzk:1",
        "name": "Mountain view"
      },
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
          "fieldName": "newCFUI",
          "value": "test cf",
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
            "name": "newCFUI",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "SALE",
                  "SALE_ESTIMATE",
                  "SALE_REFUND",
                  "PURCHASE",
                  "PURCHASE_BILL",
                  "PURCHASE::CHECK",
                  "PURCHASE_CREDIT",
                  "PURCHASE::CREDIT_CARD_CREDIT",
                  "PURCHASE_ORDER",
                  "SALE_CREDIT"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059398",
          "fieldName": "testCF",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059398",
            "name": "testCF",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "PURCHASE"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059399",
          "fieldName": "newCF",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059399",
            "name": "newCF",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "PURCHASE",
                  "SALE_ESTIMATE",
                  "SALE",
                  "SALE_INVOICE"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
          "fieldName": "Sales rep",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
            "name": "Sales rep",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "PURCHASE_ORDER",
                  "PURCHASE"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000062923",
          "fieldName": "expenseCF",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000062923",
            "name": "expenseCF",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "PURCHASE"
                ]
              }
            ]
          }
        }
      ],
      "itemLines": [
        {
          "sequence": "1",
          "amount": 150.00,
          "billable": true,
          "markup": {
            "amount": 150.00,
            "account": {
              "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjUxY2VkODUzNmM:31",
              "name": "Inventory"
            },
            "percent": "35%"
          },
          "tax": {
            "taxAmount": null,
            "taxable": false,
            "taxGroup": null
          },
          "description": "Dummy description",
          "item": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjExMmRlNzQ2OTk:4"
          },
          "quantity": 10,
          "unitPrice": 15.00,
          "class": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115"
          },
          "customer": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:5",
            "displayName": "HubSpot Customer 2",
            "firstName": "SomeFisrtName",
            "lastName": "SomeLastName"
          }
        }
      ],
      "accountLines": [
        {
          "sequence": "2",
          "description": "Test description",
          "amount": 300.00,
          "class": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115",
            "name": "Class1"
          },
          "customer": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:3",
            "displayName": "Saurabh Jaiswal"
          },
          "account": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjUxY2VkODUzNmM:33",
            "name": "Purchases"
          }
        }
      ],
      "tax": {
        "totalTaxAmount": null,
        "taxDetails": [],
        "taxGroup": null
      }
    }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updateExpense($input0: UpdateExpenseInput!) {
  updateExpense(expense: $input0) {
    id
    metadata {
      entityVersion
    }
    class {
      id
    }
    project {
      id
      name
      customer {
        id
        displayName
      }
      completedDate
      description
      status
    }
    transactionDate
    referenceNumber
    permitNumber
    amount
    memo
    permitNumber
    currency {
      name
      currency
      symbol
      exchangeRate
    }
    payee {
      __typename
      ... on Customer {
        id
        displayName
        email
        phone
        fax
        firstName
        lastName
        companyName
      }
      ... on Vendor {
        id
        displayName
        email
        phone
      }
    }
    account {
      id
      name
      fullyQualifiedName
    }
    payment {
      paymentMethod {
        id
        name
        type
      }
    }
    location {
      id
      name
    }
    customFields {
      fieldId
      fieldName
      value
      fieldDefinition {
        id
        name
        inactive
        associatedEntityTypes {
          type
          subtype
        }
      }
    }
    itemLines {
      sequence
      amount
      billable
      markup {
        amount
        account {
          id
          name
        }
        percent
      }
      tax {
        taxAmount
        taxable
        taxGroup {
          id
          name
          code
          description
          status
          saleRates {
            taxRate {
              id
              name
              description
              status
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
              status
              startDate
              endDate
              rate
            }
          }
        }
      }
      description
      item {
        id
      }
      quantity
      unitPrice
      class {
        id
      }
      customer {
        id
        displayName
        firstName
        lastName
      }
    }
    accountLines {
      sequence
      description
      amount
      class {
        id
        name
      }
      customer {
        id
        displayName
      }
      account {
        id
        name
      }
    }
    tax {
      totalTaxAmount
      taxDetails {
        taxRate {
          id
          name
          description
          status
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
        code
        description
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
  }
}
```

Required fields:
- id: ID of an existing expense
- metadata: you need to provide the entity version returned from a previous create/update/read operation. 

Variables:
```
{
	"input0": {
		"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:3672",
		"metadata": {
			"entityVersion": "0"
		},
		"transactionDate": "2021-08-26",
		"referenceNumber": "updateExpenseNumber1",
		"payee": {
			"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:16"
		},
		"account": {
			"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjUxY2VkODUzNmM:45"
		},
		"location": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1"
		},
		"payment": {
			"paymentMethod": {
				"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjVlNGYwZjQ5Y2Q:2",
				"name": "Check"
			}
		},
		"customFields": [
			{
				"fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
				"value": "updated cf"
			}
		],
		"permitNumber": "1234-Expense",
		"itemLines": [
			{
				"description": "Updated description",
				"quantity": 10,
				"amount": 100,
				"item": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjExMmRlNzQ2OTk:4"
				},
				"customer": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071f733ad5d5b53466f913281ea6447128f"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115"
				}
			}
		],
		"accountLines": [
			{
				"description": "Test description",
				"amount": 300,
				"account": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjUxY2VkODUzNmM:33"
				},
				"customer": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071eb5fc9386d9f48c39544b74cfa2d56e4"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115"
				}
			}
		],
		"currency": {
			"name": "USD",
			"currency": "USD",
			"exchangeRate": 1
		},
		"memo": "Updated Private Memo"
	}
}
```
Response:
```
{
  "data": {
    "updateExpense": {
      "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:3672",
      "metadata": {
        "entityVersion": "1"
      },
      "class": null,
      "project": null,
      "transactionDate": "2021-08-26",
      "referenceNumber": "updateExpenseNumber1",
      "permitNumber": "1234-Expense",
      "amount": 400.00,
      "memo": "Updated Private Memo",
      "currency": {
        "name": "United States Dollar",
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "payee": {
        "__typename": "Vendor",
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:16",
        "displayName": "Jack Black",
        "email": "jblack@gmail.com",
        "phone": "(650) 123-4569"
      },
      "account": {
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjUxY2VkODUzNmM:45",
        "name": "Checking",
        "fullyQualifiedName": null
      },
      "payment": {
        "paymentMethod": {
          "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjVlNGYwZjQ5Y2Q:2",
          "name": "Check",
          "type": null
        }
      },
      "location": {
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OmJmN2IzNDhiNzk:1",
        "name": "Mountain view"
      },
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
          "fieldName": "newCFUI",
          "value": "updated cf",
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
            "name": "newCFUI",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "SALE",
                  "SALE_ESTIMATE",
                  "SALE_REFUND",
                  "PURCHASE",
                  "PURCHASE_BILL",
                  "PURCHASE::CHECK",
                  "PURCHASE_CREDIT",
                  "PURCHASE::CREDIT_CARD_CREDIT",
                  "PURCHASE_ORDER",
                  "SALE_CREDIT"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059398",
          "fieldName": "testCF",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059398",
            "name": "testCF",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "PURCHASE"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059399",
          "fieldName": "newCF",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059399",
            "name": "newCF",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "PURCHASE",
                  "SALE_ESTIMATE",
                  "SALE",
                  "SALE_INVOICE"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
          "fieldName": "Sales rep",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
            "name": "Sales rep",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "PURCHASE_ORDER",
                  "PURCHASE"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000062923",
          "fieldName": "expenseCF",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000062923",
            "name": "expenseCF",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "PURCHASE"
                ]
              }
            ]
          }
        }
      ],
      "itemLines": [
        {
          "sequence": "3",
          "amount": 100.00,
          "billable": null,
          "markup": null,
          "tax": {
            "taxAmount": null,
            "taxable": false,
            "taxGroup": null
          },
          "description": "Updated description",
          "item": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjExMmRlNzQ2OTk:4"
          },
          "quantity": 10,
          "unitPrice": null,
          "class": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115"
          },
          "customer": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:5",
            "displayName": "HubSpot Customer 2",
            "firstName": "SomeFisrtName",
            "lastName": "SomeLastName"
          }
        }
      ],
      "accountLines": [
        {
          "sequence": "4",
          "description": "Test description",
          "amount": 300.00,
          "class": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115",
            "name": "Class1"
          },
          "customer": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:3",
            "displayName": "Saurabh Jaiswal"
          },
          "account": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjUxY2VkODUzNmM:33",
            "name": "Purchases"
          }
        }
      ],
      "tax": {
        "totalTaxAmount": null,
        "taxDetails": [],
        "taxGroup": null
      }
    }
  }
}
```
### Delete Mutation

Mutation:

``` 
mutation deleteExpense($input: ID!) {
  deleteExpense(id: $input){
    id
    success
  }
}
```

Required fields:
- id: ID of an existing expense
- metadata: you need to provide the entity version returned from a previous create/update/read operation. 

Variables:
``` 
{
	"input": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:38"
}
```

Response:
```
{
  "data": {
    "deleteExpense": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:38",
      "success": true
    }
  }
}
```