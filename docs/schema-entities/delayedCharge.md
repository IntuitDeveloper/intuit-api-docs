---
layout: default
title: Delayed Charge
nav_order: 4
parent: Schema Entities
---

## Delayed Charge

The APIs related to the Delayed Charge entity allow you to manage delayed charges for your customer that they can use in the future.
You can use delayed charges to keep track of items to be invoiced to clients in the future.
The DelayedCharge API provides support for create, read, update and delete operations.

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

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the delayedCharge entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an DelayedCharge by Id):
```
query fetchDelayedCharge($id: String!) {
  company {
    delayedCharges(filter: { id: { equals: $id } }) {
      pageInfo {
        hasNextPage
        hasPreviousPage
        startCursor
        endCursor
      }
      nodes {
        __typename

        id
        metadata {
          entityVersion
        }
        amount
        currency {
          name
          currency
          symbol
        }
        customer {
          id
          displayName
        }

        itemLines {
          sequence
          class {
            id
            name
          }
          description
          account {
            id
            name
          }
          item {
            id
            name
            active
          }
          quantity
          unitPrice
        }
        location {
          id
          name
        }
        privateMemo
        project {
          id
          name
          customer {
            id
            displayName
          }
        }
        referenceNumber
        tax {
          totalTaxAmount
        }
        transactionDate
      }
    }
  }
}
```

Variables:

```
{
	"id": "djQuMTo5MTMwMzUzOTY3NzQ0NjY2OjgwMjcxZWRkOGE:399"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "delayedCharges": {
        "pageInfo": {
          "hasNextPage": false,
          "hasPreviousPage": false,
          "startCursor": "c2ltcGxlLWN1cnNvcjA=",
          "endCursor": "c2ltcGxlLWN1cnNvcjA="
        },
        "nodes": [
          {
            "__typename": "DelayedCharge",
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:399",
            "metadata": {
              "entityVersion": "1"
            },
            "amount": 0.00,
            "currency": {
              "name": null,
              "currency": "USD",
              "symbol": "$"
            },
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:13",
              "displayName": "New project - demo3"
            },
            "itemLines": [
              {
                "sequence": "1",
                "description": "test",
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
                  "name": "Services"
                },
                "item": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:5",
                  "name": "Test non-inventory",
                  "active": true
                },
                "quantity": 1,
                "unitPrice": 0.00
              }
            ],
            "location": null,
            "privateMemo": "test private emo",
            "project": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27063631",
              "name": "New project - demo3",
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "displayName": "Alisha Kamat"
              }
            },
            "referenceNumber": "10",
            "tax": {
              "totalTaxAmount": null
            },
            "transactionDate": "2021-10-18"
          }
        ]
      }
    }
  }
}
```

## Filter support:

You can choose to **query by id** (as shown above) or query for all delayed charges by removing the filter.

### Create mutation
 
Mutation:
 
```
mutation createDelayedCharge($input_0: CreateDelayedChargeInput!) {
  createDelayedCharge(delayedCharge: $input_0) {
    id
    metadata {
      entityVersion
    }
    amount
    project {
      id
      name
      customer {
        id
      }
    }
    currency {
      name
      currency
      symbol
    }
    customer {
      id
      displayName
    }
    itemLines {
      sequence
      description
      account {
        id
        name
      }
      item {
        id
        name
        active
        amount
      }
      quantity
      unitPrice
    }
    location {
      id
      name
    }
    privateMemo
    project {
      id
      name
      customer {
        id
        displayName
      }
    }
    referenceNumber
    tax {
      totalTaxAmount
    }
    transactionDate
  }
}

```
 
Sample Variables: 
``` 
{
	"input_0": {
		"project": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:28392628"
		},
		"privateMemo": "test private memo",
		"transactionDate": "2021-10-20",
		"itemLines": [
			{
				"description": "test descriptoin",
				"account": {
					"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5"
				},
				"item": {
					"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:5"
				},
				"quantity": 1,
				"unitPrice": 45
			}
		]
	}
}
```    

Sample response:
```
{
  "data": {
    "createDelayedCharge": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:666",
      "metadata": {
        "entityVersion": "0"
      },
      "amount": 0.00,
      "project": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:28392628",
        "name": "Ata Bi Pro",
        "customer": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:34",
          "displayName": "Tanmay B"
        }
      },
      "currency": {
        "name": null,
        "currency": "USD",
        "symbol": "$"
      },
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:35",
        "displayName": "Ata Bi Pro"
      },
      "invoice": null,
      "itemLines": [
        {
          "sequence": "1",
          "description": "test descriptoin",
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
            "name": "Services"
          },
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:5",
            "name": "Test non-inventory",
            "active": true
          },
          "quantity": 1,
          "unitPrice": 45.00
        }
      ],
      "location": null,
      "privateMemo": "test private memo",
      "referenceNumber": null,
      "tax": {
        "totalTaxAmount": null
      },
      "transactionDate": "2021-10-20"
    }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updateDelayedCharge($input_0: UpdateDelayedChargeInput!) {
  updateDelayedCharge(delayedCharge: $input_0) {
    id
    metadata {
      entityVersion
    }
    amount
    project {
      id
      name
      customer {
        id
      }
    }
    currency {
      name
      currency
      symbol
    }
    customer {
      id
      displayName
    }
    itemLines {
      sequence
      description
      account {
        id
        name
      }
      item {
        id
        name
        active
      }
      quantity
      unitPrice
    }
    location {
      id
      name
    }
    privateMemo
    project {
      id
      name
      customer {
        id
        displayName
      }
    }
    referenceNumber
    tax {
      totalTaxAmount
    }
    transactionDate
  }
}

```

Required fields:
- id: ID of an existing DelayedCharge
- metadata: you need to provide the entity version returned from a previous create/update/read operation. 

Variables:

```
{
	"input_0": {
		"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:666",
		"metadata": {
			"entityVersion": "0"
		},
		"project": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:28392628"
		},
		"privateMemo": "test private memo",
		"transactionDate": "2021-10-20",
		"itemLines": [
			{
				"description": "test descriptoin",
				"account": {
					"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5"
				},
				"item": {
					"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:5"
				},
				"quantity": 1,
				"unitPrice": 45
			}
		]
	}
}
```

Response:
```
{
  "data": {
    "updateDelayedCharge": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:666",
      "metadata": {
        "entityVersion": "1"
      },
      "amount": 0.00,
      "project": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:28392628",
        "name": "Ata Bi Pro",
        "customer": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:34",
          "displayName": "Tanmay B"
        }
      },
      "currency": {
        "name": null,
        "currency": "USD",
        "symbol": "$"
      },
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:35",
        "displayName": "Ata Bi Pro"
      },
      "itemLines": [
        {
          "sequence": "2",
          "description": "test descriptoin",
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
            "name": "Services"
          },
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:5",
            "name": "Test non-inventory",
            "active": true
          },
          "quantity": 1,
          "unitPrice": 45.00
        }
      ],
      "location": null,
      "privateMemo": "test private memo",
      "referenceNumber": null,
      "tax": {
        "totalTaxAmount": null
      },
      "transactionDate": "2021-10-20"
    }
  }
}
```

### Delete Mutation

Mutation:

``` 
mutation deleteDelayedCharge($input: ID!) {
  deleteDelayedCharge(id: $input){
    id
    success
  }
}
```

Required fields:
- id: ID of an existing DelayedCharge

Variables:
``` 
{
	"input": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:666"
}
```

Response:
```
{
  "data": {
    "deleteDelayedCharge": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:666",
      "success": true
    }
  }
}
```