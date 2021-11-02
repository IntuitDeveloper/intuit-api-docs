---
layout: default
title: PurchaseOrder
nav_order: 17
parent: Use Cases
---

## PurchaseOrder

The APIs related to the PurchaseOrder entity allow you to manage purchase orders so that you can directly send 
A payee can currently be either a customer or a vendor.
The PurchaseOrder API provides support for create, read, update and delete operations.

### Operations for PurchaseOrder entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the purchase order scope **[com.intuit.quickbooks.accounting]** for the authorization header 

### Sample query body

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the PurchaseOrder entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an PurchaseOrder by Id):
```
query fetchPurchaseOrders($id: String) {
  company {
    purchaseOrders(filter: {id: {equals: $id}}) {
      nodes {
        id
        metadata {
          entityVersion
        }
        purchaseOrderNumber
        referenceNumber
        transactionDate
        closed
        amount
        location {
          id
          name
        }
        currency {
          name
          currency
          exchangeRate
        }
        project {
          id
          name
          active
          completedDate
          description
          customer {
            id
            displayName
          }
        }
        memo
        vendorMemo
        emailDeliveryInfo {
          to
          bcc
          cc
        }
        customFields {
          fieldId
          fieldName
          value
          fieldDefinition {
            id
            name
            associatedEntityTypes {
              type
              subtype
            }
            inactive
          }
        }
        vendor {
          id
          displayName
        }
        class {
          id
          name
        }
        mailingAddress {
          freeFormAddressLine
        }
        permitNumber
        shipping {
          shipDate
          shipVia
          shipFromAddress {
            freeFormAddressLine
          }
          shippingAmount
          shipAddress {
            freeFormAddressLine
          }
          trackingNumber
          tax {
            taxable
            taxAmount
            taxGroup {
              id
              name
            }
          }
        }
        itemLines {
          sequence
          description
          quantity
          amount
          billable
          billableAmount
          markup {
            amount
            account {
              id
              name
            }
            percent
          }
          item {
            id
            name
          }
          class {
            id
            name
          }
          customer {
            id
            displayName
          }
          tax {
            taxable
            taxAmount
            taxGroup {
              id
              name
            }
          }
        }
        accountLines {
          sequence
          description
          billable
          billableAmount
          amount
          markup {
            account {
              id
              name
            }
            amount
            percent
          }
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
          tax {
            taxable
            taxAmount
            taxGroup {
              id
              name
            }
          }
        }
        tax {
          taxable
          taxDetails {
            taxRate {
              id
              name
              description
              startDate
              endDate
              status
            }
          }
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
              }
            }
            purchaseRates {
              taxRate {
                id
                name
              }
            }
          }
          totalTaxAmount
        }
      }
    }
  }
}

```

Variables:

```
{
	"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:445"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "purchaseOrders": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:445",
            "metadata": {
              "entityVersion": "1"
            },
            "purchaseOrderNumber": null,
            "referenceNumber": null,
            "transactionDate": "2021-04-21",
            "closed": true,
            "amount": 450.00,
            "location": {
              "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OmJmN2IzNDhiNzk:1",
              "name": "Mountain view"
            },
            "currency": {
              "name": null,
              "currency": "USD",
              "exchangeRate": 1.00
            },
            "project": null,
            "memo": "This is updated memo",
            "vendorMemo": "Update vendor memo!",
            "emailDeliveryInfo": {
              "to": [
                "jblack@gmail.com"
              ],
              "bcc": [
                "null"
              ],
              "cc": [
                "null"
              ]
            },
            "customFields": [
              {
                "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
                "fieldName": "newCFUI",
                "value": "updated cf",
                "fieldDefinition": {
                  "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
                  "name": "newCFUI",
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
                  ],
                  "inactive": false
                }
              },
              {
                "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
                "fieldName": "Sales rep",
                "value": null,
                "fieldDefinition": {
                  "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
                  "name": "Sales rep",
                  "associatedEntityTypes": [
                    {
                      "type": "/transactions/Transaction",
                      "subtype": [
                        "SALE_INVOICE",
                        "PURCHASE_ORDER",
                        "PURCHASE"
                      ]
                    }
                  ],
                  "inactive": false
                }
              }
            ],
            "vendor": {
              "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:16",
              "displayName": "Jack Black"
            },
            "class": null,
            "mailingAddress": {
              "freeFormAddressLine": "Jack Black\r\n2535 Garcia Ave\r\nMountain View, CA  94043"
            },
            "permitNumber": "4567",
            "shipping": {
              "shipDate": null,
              "shipVia": "test ship via",
              "shipFromAddress": null,
              "shippingAmount": null,
              "shipAddress": {
                "freeFormAddressLine": "hubspot e2e\r\n2700 Coast Ave\r\nWoodland Hills, CA 91367 US\r\n"
              },
              "trackingNumber": null,
              "tax": null
            },
            "itemLines": [
              {
                "sequence": "3",
                "description": "Dummy description2",
                "quantity": 10,
                "amount": 150.00,
                "billable": null,
                "billableAmount": null,
                "markup": null,
                "item": {
                  "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjExMmRlNzQ2OTk:4",
                  "name": "T-shirts"
                },
                "class": {
                  "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115",
                  "name": "Class1"
                },
                "customer": {
                  "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:5",
                  "displayName": "HubSpot Customer 2"
                },
                "tax": {
                  "taxable": false,
                  "taxAmount": null,
                  "taxGroup": null
                }
              }
            ],
            "accountLines": [
              {
                "sequence": "4",
                "description": "Test description 2",
                "billable": null,
                "billableAmount": null,
                "amount": 300.00,
                "markup": null,
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
                },
                "tax": {
                  "taxable": false,
                  "taxAmount": null,
                  "taxGroup": null
                }
              }
            ],
            "tax": {
              "taxable": null,
              "taxDetails": [],
              "taxGroup": null,
              "totalTaxAmount": null
            }
          }
        ]
      }
    }
  }
}
```

## Filter support:

You can choose to **query by id** (as shown above) or query for all purchase orders by removing the filter.

### Create mutation
 
Mutation:
 
```
mutation createPurchaseOrder($input0: CreatePurchaseOrderInput!) {
  createPurchaseOrder(purchaseOrder: $input0) {
    id
    metadata {
      entityVersion
    }
    purchaseOrderNumber
    referenceNumber
    transactionDate
    closed
    amount
    location {
      id
      name
    }
    currency {
      name
      currency
      exchangeRate
    }
    project {
      id
      name
      active
      completedDate
      description
      customer {
        id
        displayName
      }
    }
    memo
    vendorMemo
    emailDeliveryInfo {
      to
      bcc
      cc
    }
    customFields {
      fieldId
      fieldName
      value
      fieldDefinition {
        id
        name
        associatedEntityTypes {
          type
          subtype
        }
        inactive
      }
    }
    vendor {
      id
      displayName
    }
    class {
      id
      name
    }
    mailingAddress {
      freeFormAddressLine
    }
    permitNumber
    shipping {
      shipDate
      shipVia
      shipFromAddress {
        freeFormAddressLine
      }
      shippingAmount
      shipAddress {
        freeFormAddressLine
      }
      trackingNumber
      tax {
        taxable
        taxAmount
        taxGroup {
          id
          name
        }
      }
    }
    itemLines {
      sequence
      description
      quantity
      amount
      billable
      billableAmount
      markup {
        amount
        account {
          id
          name
        }
        percent
      }
      item {
        id
        name
      }
      class {
        id
        name
      }
      customer {
        id
        displayName
      }
      tax {
        taxable
        taxAmount
        taxGroup {
          id
          name
        }
      }
    }
    accountLines {
      sequence
      description
      billable
      billableAmount
      amount
      markup {
        account {
          id
          name
        }
        amount
        percent
      }
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
      tax {
        taxable
        taxAmount
        taxGroup {
          id
          name
        }
      }
    }
    tax {
      taxable
      taxDetails {
        taxRate {
          id
          name
          description
          startDate
          endDate
          status
        }
      }
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
          }
        }
        purchaseRates {
          taxRate {
            id
            name
          }
        }
      }
      totalTaxAmount
    }
  }
}

```
 
Sample Variables: 
``` 
{
	"input0": {
		"vendor": {
			"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:002071a7bc53d6b24c43c1814150289f2df6d6"
		},
		"closed": false,
		"memo": "This is test memo",
		"vendorMemo": "Vendor memo!",
		"permitNumber": "1234",
    "purchaseOrderNumber": "44444",
    "customFields": [
      {
        "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
        "value": "some cf value"
      }
    ],
		"transactionDate": "2021-04-20",
		"emailDeliveryInfo": {
			"to": [
				"jblack@gmail.com"
			]
		},
		"tax": {
			"totalTaxAmount": 9,
			"taxGroup": {
				"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6"
			},
			"taxable": true
		},
		"mailingAddress": {
			"freeFormAddressLine": "Jack Black\r\n2535 Garcia Ave\r\nMountain View, CA 94043"
		},
		"shipping": {
			"shipVia": "test ship via",
			"shipAddress": {
				"freeFormAddressLine": "hubspot e2e\r\n2700 Coast Ave\r\nWoodland Hills, CA 91367 US\r\n"
			}
		},
		"location": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1"
		},
		"itemLines": [
			{
				"description": "Dummy description2",
				"quantity": 10,
				"amount": 150,
				"item": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjExMmRlNzQ2OTk:4"
				},
				"customer": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:16"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115"
				}
			}
		],
		"accountLines": [
			{
				"description": "Test description 2",
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
		]
	}
}
```    

Sample response:
```
{
  "data": {
    "createPurchaseOrder": {
      "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:3675",
      "metadata": {
        "entityVersion": "0"
      },
      "purchaseOrderNumber": "44444",
      "referenceNumber": "44444",
      "transactionDate": "2021-04-20",
      "closed": false,
      "amount": 450.00,
      "location": {
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OmJmN2IzNDhiNzk:1",
        "name": "Mountain view"
      },
      "currency": {
        "name": null,
        "currency": "USD",
        "exchangeRate": 1.00
      },
      "project": null,
      "memo": "This is test memo",
      "vendorMemo": "Vendor memo!",
      "emailDeliveryInfo": {
        "to": [
          "jblack@gmail.com"
        ],
        "bcc": [
          "null"
        ],
        "cc": [
          "null"
        ]
      },
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
          "fieldName": "newCFUI",
          "value": "some cf value",
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
            "name": "newCFUI",
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
            ],
            "inactive": false
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
          "fieldName": "Sales rep",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
            "name": "Sales rep",
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "PURCHASE_ORDER",
                  "PURCHASE"
                ]
              }
            ],
            "inactive": false
          }
        }
      ],
      "vendor": {
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:16",
        "displayName": "Jack Black"
      },
      "class": null,
      "mailingAddress": {
        "freeFormAddressLine": "Jack Black\r\n2535 Garcia Ave\r\nMountain View, CA  94043"
      },
      "permitNumber": "1234",
      "shipping": {
        "shipDate": null,
        "shipVia": "test ship via",
        "shipFromAddress": null,
        "shippingAmount": null,
        "shipAddress": {
          "freeFormAddressLine": "hubspot e2e\r\n2700 Coast Ave\r\nWoodland Hills, CA 91367 US\r\n"
        },
        "trackingNumber": null,
        "tax": null
      },
      "itemLines": [
        {
          "sequence": "1",
          "description": "Dummy description2",
          "quantity": 10,
          "amount": 150.00,
          "billable": null,
          "billableAmount": null,
          "markup": null,
          "item": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjExMmRlNzQ2OTk:4",
            "name": "T-shirts"
          },
          "class": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115",
            "name": "Class1"
          },
          "customer": null,
          "tax": {
            "taxable": false,
            "taxAmount": null,
            "taxGroup": null
          }
        }
      ],
      "accountLines": [
        {
          "sequence": "2",
          "description": "Test description 2",
          "billable": null,
          "billableAmount": null,
          "amount": 300.00,
          "markup": null,
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
          },
          "tax": {
            "taxable": false,
            "taxAmount": null,
            "taxGroup": null
          }
        }
      ],
      "tax": {
        "taxable": null,
        "taxDetails": [],
        "taxGroup": null,
        "totalTaxAmount": null
      }
    }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updatePurchaseOrder($input0: UpdatePurchaseOrderInput!) {
  updatePurchaseOrder(purchaseOrder: $input0) {
    id
    metadata {
      entityVersion
    }
    purchaseOrderNumber
    referenceNumber
    transactionDate
    closed
    amount
    location {
      id
      name
    }
    currency {
      name
      currency
      exchangeRate
    }
    project {
      id
      name
      active
      completedDate
      description
      customer {
        id
        displayName
      }
    }
    memo
    vendorMemo
    emailDeliveryInfo {
      to
      bcc
      cc
    }
    customFields {
      fieldId
      fieldName
      value
      fieldDefinition {
        id
        name
        associatedEntityTypes {
          type
          subtype
        }
        inactive
      }
    }
    vendor {
      id
      displayName
    }
    class {
      id
      name
    }
    mailingAddress {
      freeFormAddressLine
    }
    permitNumber
    shipping {
      shipDate
      shipVia
      shipFromAddress {
        freeFormAddressLine
      }
      shippingAmount
      shipAddress {
        freeFormAddressLine
      }
      trackingNumber
      tax {
        taxable
        taxAmount
        taxGroup {
          id
          name
        }
      }
    }
    itemLines {
      sequence
      description
      quantity
      amount
      billable
      billableAmount
      markup {
        amount
        account {
          id
          name
        }
        percent
      }
      item {
        id
        name
      }
      class {
        id
        name
      }
      customer {
        id
        displayName
      }
      tax {
        taxable
        taxAmount
        taxGroup {
          id
          name
        }
      }
    }
    accountLines {
      sequence
      description
      billable
      billableAmount
      amount
      markup {
        account {
          id
          name
        }
        amount
        percent
      }
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
      tax {
        taxable
        taxAmount
        taxGroup {
          id
          name
        }
      }
    }
    tax {
      taxable
      taxDetails {
        taxRate {
          id
          name
          description
          startDate
          endDate
          status
        }
      }
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
          }
        }
        purchaseRates {
          taxRate {
            id
            name
          }
        }
      }
      totalTaxAmount
    }
  }
}

```

Required fields:
- id: ID of an existing purchase order.
- metadata: you need to provide the entity version returned from a previous create/update/read operation. 

Variables:
```
{
	"input0": {
		"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:3675",
		"vendor": {
			"id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:16"
		},
		"customFields": [
			{
				"fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
				"value": "updated cf value for purchaseOder"
			}
		],
		"closed": true,
		"memo": "This is updated memo",
		"vendorMemo": "Update vendor memo!",
		"permitNumber": "3675",
		"transactionDate": "2021-04-21",
		"emailDeliveryInfo": {
			"to": [
				"jblack@gmail.com"
			]
		},
		"mailingAddress": {
			"freeFormAddressLine": "Jack Black\r\n2535 Garcia Ave\r\nMountain View, CA 94043"
		},
		"shipping": {
			"shipVia": "test ship via",
			"shipAddress": {
				"freeFormAddressLine": "hubspot e2e\r\n2700 Coast Ave\r\nWoodland Hills, CA 91367 US\r\n"
			}
		},
		"location": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1"
		},
		"metadata": {
			"entityVersion": "0"
		},
		"itemLines": [
			{
				"description": "Dummy description2",
				"quantity": 10,
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
				"description": "Test description 2",
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
		]
	}
}
```

Response:
```
{
  "data": {
    "updatePurchaseOrder": {
      "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:3675",
      "metadata": {
        "entityVersion": "1"
      },
      "purchaseOrderNumber": null,
      "referenceNumber": null,
      "transactionDate": "2021-04-21",
      "closed": true,
      "amount": 450.00,
      "location": {
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OmJmN2IzNDhiNzk:1",
        "name": "Mountain view"
      },
      "currency": {
        "name": null,
        "currency": "USD",
        "exchangeRate": 1.00
      },
      "project": null,
      "memo": "This is updated memo",
      "vendorMemo": "Update vendor memo!",
      "emailDeliveryInfo": {
        "to": [
          "jblack@gmail.com"
        ],
        "bcc": [
          "null"
        ],
        "cc": [
          "null"
        ]
      },
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
          "fieldName": "newCFUI",
          "value": "updated cf value for purchaseOder",
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000059612",
            "name": "newCFUI",
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
            ],
            "inactive": false
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
          "fieldName": "Sales rep",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MjMyNTc1ODI5NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060876",
            "name": "Sales rep",
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "PURCHASE_ORDER",
                  "PURCHASE"
                ]
              }
            ],
            "inactive": false
          }
        }
      ],
      "vendor": {
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:16",
        "displayName": "Jack Black"
      },
      "class": null,
      "mailingAddress": {
        "freeFormAddressLine": "Jack Black\r\n2535 Garcia Ave\r\nMountain View, CA  94043"
      },
      "permitNumber": "3675",
      "shipping": {
        "shipDate": null,
        "shipVia": "test ship via",
        "shipFromAddress": null,
        "shippingAmount": null,
        "shipAddress": {
          "freeFormAddressLine": "hubspot e2e\r\n2700 Coast Ave\r\nWoodland Hills, CA 91367 US\r\n"
        },
        "trackingNumber": null,
        "tax": null
      },
      "itemLines": [
        {
          "sequence": "3",
          "description": "Dummy description2",
          "quantity": 10,
          "amount": 150.00,
          "billable": null,
          "billableAmount": null,
          "markup": null,
          "item": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjExMmRlNzQ2OTk:4",
            "name": "T-shirts"
          },
          "class": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjIyYzE1MDQ2NzU:302300000000001854115",
            "name": "Class1"
          },
          "customer": {
            "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:5",
            "displayName": "HubSpot Customer 2"
          },
          "tax": {
            "taxable": false,
            "taxAmount": null,
            "taxGroup": null
          }
        }
      ],
      "accountLines": [
        {
          "sequence": "4",
          "description": "Test description 2",
          "billable": null,
          "billableAmount": null,
          "amount": 300.00,
          "markup": null,
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
          },
          "tax": {
            "taxable": false,
            "taxAmount": null,
            "taxGroup": null
          }
        }
      ],
      "tax": {
        "taxable": null,
        "taxDetails": [],
        "taxGroup": null,
        "totalTaxAmount": null
      }
    }
  }
}
```
### Delete Mutation

Mutation:

``` 
mutation deletePurchaseOrder($input: ID!) {
  deletePurchaseOrder(id: $input){
    id
    success
  }
}
```

Required fields:
- id: ID of an existing purchase order

Variables:
``` 
{
	"input": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:3675"
}
```

Response:
```
{
  "data": {
    "deletePurchaseOrder": {
      "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjgwMjcxZWRkOGE:3675",
      "success": true
    }
  }
}
```