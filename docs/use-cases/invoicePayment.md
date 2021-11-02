---
layout: default
title: InvoicePayment
nav_order: 12
parent: Use Cases
---

## InvoicePayment

The APIs related to the InvoicePayment entity allow you to track payments from your customers, if you are not using Sales receipts when your customers pay you.
The InvoicePayment API provides support for create, read, update and delete operations.

### Operations for InvoicePayment entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the invoice payment scope **[com.intuit.quickbooks.accounting]** for the authorization header 

### Sample query body

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the InvoicePayment entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an InvoicePayment by Id):
```
query fetchInvoicePayment($id: String!) {
  company {
    invoicePayments(filter: {id: {equals: $id}}) {
      nodes {
        id
        metadata {
          entityVersion
        }
        amount
        account {
          id
          name
          fullyQualifiedName
        }
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
          firstName
          lastName
          companyName
        }
        emailDeliveryInfo {
          to
          cc
          bcc
        }
        invoices {
          amount
          invoice {
            id
            amount
            customer {
              id
              displayName
            }
          }
        }
        payment {
          paymentMethod {
            id
            name
            type
          }
        }
        privateMemo
        project {
          id
          name
          description
          customer {
            id
            displayName
          }
        }
        transactionDate
        referenceNumber
        voided
      }
      pageInfo {
        hasPreviousPage
        hasNextPage
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
	"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:23"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "invoicePayments": [
        {
          "nodes": [
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:23",
              "metadata": {
                "entityVersion": "0"
              },
              "amount": 20.00,
              "account": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:15",
                "name": "Payments to deposit",
                "fullyQualifiedName": "Payments to deposit"
              },
              "class": null,
              "currency": {
                "name": null,
                "currency": "USD",
                "symbol": "$",
                "exchangeRate": 1.00
              },
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
                "displayName": "SC 1 Project 3",
                "firstName": null,
                "lastName": null,
                "companyName": null
              },
              "emailDeliveryInfo": {
                "to": [
                  "hp@test.com"
                ],
                "cc": [
                  "null"
                ],
                "bcc": [
                  "null"
                ]
              },
              "invoices": [
                {
                  "amount": 10.00,
                  "invoice": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:3",
                    "customer": {
                      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
                      "displayName": "SC 1 Project 3"
                    }
                  }
                },
                {
                  "amount": 10.00,
                  "invoice": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:4",
                    "customer": {
                      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
                      "displayName": "SC 1 Project 3"
                    }
                  }
                },
                {
                  "amount": null,
                  "invoice": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:26",
                    "amount": 400.00,
                    "customer": {
                      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
                      "displayName": "SC 1 Project 3"
                    }
                  }
                },
                {
                  "amount": null,
                  "invoice": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:27",
                    "customer": {
                      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
                      "displayName": "SC 1 Project 3"
                    }
                  }
                },
                {
                  "amount": null,
                  "invoice": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:29",
                    "customer": {
                      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
                      "displayName": "SC 1 Project 3"
                    }
                  }
                },
                {
                  "amount": null,
                  "invoice": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:30",
                    "customer": {
                      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
                      "displayName": "SC 1 Project 3"
                    }
                  }
                }
              ],
              "payment": {
                "paymentMethod": null
              },
              "privateMemo": null,
              "project": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27391835",
                "name": "SC 1 Project 3",
                "description": "Test project 3 for sub customer 1",
                "customer": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:15",
                  "displayName": "Harry Potter"
                }
              },
              "transactionDate": "2021-08-19",
              "referenceNumber": null,
              "voided": false
            }
          ],
          "pageInfo": {
            "hasPreviousPage": false,
            "hasNextPage": false,
            "startCursor": "c2ltcGxlLWN1cnNvcjA=",
            "endCursor": "c2ltcGxlLWN1cnNvcjA="
          }
        }
      ]
    }
  }
}
```

## Filter support:

You can choose to **query by id** (as shown above) or query for all invoice payments by removing the filter.

### Create mutation
 
Mutation:
 
```
mutation createInvoicePayment($input_0: CreateInvoicePaymentInput!) {
  createInvoicePayment(invoicePayment: $input_0) {
    id
    metadata {
      entityVersion
    }
    amount
    account {
      id
      name
      fullyQualifiedName
    }
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
      firstName
      lastName
      companyName
    }
    emailDeliveryInfo {
      to
      cc
      bcc
    }
    invoices {
      amount
      invoice {
        id
        customer {
          id
          displayName
        }
      }
    }
    payment {
      paymentMethod {
        id
        name
        type
      }
    }
    privateMemo
    project {
      id
      name
      description
      customer {
        id
        displayName
      }
    }
    transactionDate
    referenceNumber
    voided
  }
}

```
 
Sample Variables: 
``` 
{
	"input_0": {
		"customer": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17"
		},
		"account": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:15"
		},
		"transactionDate": "2021-05-26",
		"referenceNumber": "RecvPayment24",
		"payment": {
			"paymentMethod": {
				"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjVlNGYwZjQ5Y2Q:2",
				"name": "CHECK"
			}
		},
		"amount": 49,
		"invoices": [
			{
				"amount": 45,
				"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:39"
			},
			{
				"amount": 3,
				"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:4"
			}
		]
	}
}
```    

Sample response:
```
{
  "data": {
    "createInvoicePayment": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:40",
      "metadata": {
        "entityVersion": "0"
      },
      "amount": 49.00,
      "account": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:15",
        "name": "Payments to deposit",
        "fullyQualifiedName": null
      },
      "class": null,
      "currency": {
        "name": null,
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
        "displayName": "SC 1 Project 3",
        "firstName": null,
        "lastName": null,
        "companyName": null
      },
      "emailDeliveryInfo": {
        "to": [
          "null"
        ],
        "cc": [
          "null"
        ],
        "bcc": [
          "null"
        ]
      },
      "invoices": [
        {
          "amount": 3.00,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:4",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": 45.00,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:39",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": null,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:26",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": null,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:27",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": null,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:29",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": null,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:30",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        }
      ],
      "payment": {
        "paymentMethod": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjVlNGYwZjQ5Y2Q:2",
          "name": "Check",
          "type": null
        }
      },
      "privateMemo": null,
      "project": null,
      "transactionDate": "2021-05-26",
      "referenceNumber": null,
      "voided": false
    }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updateInvoicePayment($input_0: UpdateInvoicePaymentInput!) {
  updateInvoicePayment(invoicePayment: $input_0) {
    id
    metadata {
      entityVersion
    }
    amount
    account {
      id
      name
      fullyQualifiedName
    }
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
      firstName
      lastName
      companyName
    }
    emailDeliveryInfo {
      to
      cc
      bcc
    }
    invoices {
      amount
      invoice {
        id
        customer {
          id
          displayName
        }
      }
    }
    payment {
      paymentMethod {
        id
        name
        type
      }
    }
    privateMemo
    project {
      id
      name
      description
      customer {
        id
        displayName
      }
    }
    transactionDate
    referenceNumber
    voided
  }
}
```

Variables:
```
{
	"input_0": {
		"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:40",
		"metadata": {
			"entityVersion": "0"
		},
		"account": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:15"
		},
		"customer": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17"
		},
		"transactionDate": "2021-05-26",
		"referenceNumber": "RecvPayment25",
		"payment": {
			"paymentMethod": {
				"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjVlNGYwZjQ5Y2Q:2",
				"name": "CHECK"
			}
		},
		"amount": 48,
		"invoices": [
			{
				"amount": 45,
				"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:39"
			},
			{
				"amount": 3,
				"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:4"
			}
		]
	}
}
```
Response:
```
{
  "data": {
    "updateInvoicePayment": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:40",
      "metadata": {
        "entityVersion": "1"
      },
      "amount": 48.00,
      "account": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:15",
        "name": "Payments to deposit",
        "fullyQualifiedName": null
      },
      "class": null,
      "currency": {
        "name": null,
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
        "displayName": "SC 1 Project 3",
        "firstName": null,
        "lastName": null,
        "companyName": null
      },
      "emailDeliveryInfo": {
        "to": [
          "null"
        ],
        "cc": [
          "null"
        ],
        "bcc": [
          "null"
        ]
      },
      "invoices": [
        {
          "amount": 3.00,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:4",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": 45.00,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:39",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": null,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:26",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": null,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:27",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": null,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:29",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        },
        {
          "amount": null,
          "invoice": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:30",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:17",
              "displayName": "SC 1 Project 3"
            }
          }
        }
      ],
      "payment": {
        "paymentMethod": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjVlNGYwZjQ5Y2Q:2",
          "name": "Check",
          "type": null
        }
      },
      "privateMemo": null,
      "project": null,
      "transactionDate": "2021-05-26",
      "referenceNumber": null,
      "voided": false
    }
  }
}
```
### Delete Mutation

Mutation:

``` 
mutation deleteInvoicePayment($input: ID!) {
  deleteInvoicePayment(id: $input){
    id
    success
  }
}
```

Variables:
``` 
{
	"input": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:40"
}
```

Response:
```
{
  "data": {
    "deleteInvoicePayment": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:40",
      "success": true
    }
  }
}
```