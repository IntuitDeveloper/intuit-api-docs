---
layout: default
title: refundReciept
nav_order: 14
parent: Use Cases
---

## Invoice

The APIs related to the reFundReceipt entity allow you to manage refund reciepts for your customer to track accomplished payments.
The refundReciept API provides support for create, read, update and delete operations.

### Operations for Invoice entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the invoice scope **[com.intuit.quickbooks.accounting]** for the authorization header

### Sample query body

Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an Invoice by Id):
```
query fetchRefundReceipt($id: String!) {
  company {
    refundReceipts (filter: {id: {equals: $id}}){
      nodes {
        id
       type
        amount
        voided
        location {
          id
          name
        }
        tax{
          totalTaxAmount
          taxable
          taxGroup {
            id
            name
            description
          }
           taxDetails {
            taxRate {
              id
              name
              description
            }
            taxAmount
          }
        }
        emailDeliveryInfo{
          to
          cc
          bcc
          status
        }
        transactionDate
        referenceNumber
        metadata{
          entityVersion
        }
        privateMemo
        customerMemo
        class{
          id
          name
        }
        discount {
          amount {
            percentage
            value
          }
          applyTaxAfterDiscount
        }
        billingAddress {
          freeFormAddressLine
        }
        shipping{
          shipFromAddress {
            freeFormAddressLine
          }
        }
        currency{
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
        payment{
          paymentMethod {
            id
            name
            type
          }
          
        }
        account{
          id
          name
          fullyQualifiedName
        }
        customFields {
          fieldId
          fieldName
          value
          fieldDefinition {
            id
            name
            inactive
          }
        }
        itemLines{
          sequence
          description
          quantity
          item{
            id
            name
            sku
          }
          amount
          unitPrice
          class{
            id
            name        
          }
          tax{ 
            taxable
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
	"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6889"
}
```

Response:
``` 
 {
  "data": {
    "company": {
      "refundReceipts": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6889",
            "type": null,
            "amount": 17.32,
            "voided": false,
            "location": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
              "name": "SomeLocation"
            },
            "tax": {
              "totalTaxAmount": 1.32,
              "taxable": null,
              "taxGroup": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:3",
                "name": "08edb556738fa830bf6d2a09730df639e963c0c5ce1d5b4e97a376abec0bfa7c",
                "description": "TX-Plano-3057994"
              },
              "taxDetails": [
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:4",
                    "name": "Texas, Plano City",
                    "description": "ST"
                  },
                  "taxAmount": 0.16
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:5",
                    "name": "Texas, Dallas Mta District",
                    "description": "ST"
                  },
                  "taxAmount": 0.16
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:3",
                    "name": "Texas State",
                    "description": "ST"
                  },
                  "taxAmount": 1.00
                }
              ]
            },
            "emailDeliveryInfo": {
              "to": [
                "somefirstname@intuit.com"
              ],
              "cc": [
                "ccsomefirstname@intuit.com"
              ],
              "bcc": [
                "bccsomefirstname@intuit.com"
              ],
              "status": "NOT_SET"
            },
            "transactionDate": "2021-05-16",
            "referenceNumber": "SomeReceiptNumber",
            "metadata": {
              "entityVersion": "0"
            },
            "privateMemo": "Some private memo",
            "customerMemo": "Some Customer memo",
            "class": null,
            "discount": {
              "amount": {
                "percentage": false,
                "value": -4.00
              },
              "applyTaxAfterDiscount": true
            },
            "billingAddress": {
              "freeFormAddressLine": "Mr. SomeFirstName SomeLastName Some Company 2535 Garcia Ave Mountain View, CA 94043 USA\r\n"
            },
            "shipping": {
              "shipFromAddress": {
                "freeFormAddressLine": "5601 Headquarters Dr., Plano, CA, 75024, USA\r\n"
              }
            },
            "currency": {
              "name": "United States Dollar",
              "currency": "USD",
              "symbol": "$",
              "exchangeRate": 1.00
            },
            "customer": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
              "displayName": "Mr. SomeFirstName SomeLastName",
              "firstName": "SomeFirstName",
              "lastName": "SomeLastName",
              "companyName": "Some Company",
              "notes": "This is a sample note",
              "website": "https://intuit.com",
              "email": "somefirstname@intuit.com",
              "phone": "(408) 412-9211",
              "mobile": "(408) 412-9211",
              "fax": "(408) 412-9211",
              "contactMethods": [
                {
                  "type": "BILLING",
                  "primary": true,
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
                  "primary": false,
                  "address": {
                    "streetAddress1": "2535 Garcia Ave",
                    "streetAddress2": null,
                    "city": "Mountain View",
                    "state": "CA",
                    "country": "USA",
                    "zipCode": "94043"
                  }
                }
              ]
            },
            "payment": {
              "paymentMethod": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjVlNGYwZjQ5Y2Q:1",
                "name": "Cash",
                "type": null
              }
            },
            "account": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:31",
              "name": "Inventory Asset",
              "fullyQualifiedName": "Inventory Asset"
            },
            "customFields": [
              {
                "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
                "fieldName": "Sales Rep",
                "value": "text cf value",
                "fieldDefinition": {
                  "id": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
                  "name": "Sales Rep",
                  "inactive": false
                }
              },
              {
                "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000061217",
                "fieldName": "Test SR CF",
                "value": null,
                "fieldDefinition": {
                  "id": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000061217",
                  "name": "Test SR CF",
                  "inactive": false
                }
              }
            ],
            "itemLines": [
              {
                "sequence": "1",
                "description": "Some Item description",
                "quantity": 10,
                "item": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8",
                  "name": "Rose Bushes",
                  "sku": "77-88-99"
                },
                "amount": 20.00,
                "unitPrice": 2.00,
                "class": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
                  "name": "SomeClass"
                },
                "tax": {
                  "taxable": true
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

## Filter support:

You can choose to **query by id of refundReceipt** (as shown above).

### Create mutation

Mutation:

```
mutation createRefundReceipt($input: CreateRefundReceiptInput!) {
  createRefundReceipt(refundReceipt: $input) {
    id
    amount
    voided
    referenceNumber
    transactionDate
    tax {
      totalTaxAmount
    }
    metadata{
      entityVersion
    }
    location{
      id
      name
    }
    discount{
      amount {
        percentage
        value
      }
      applyTaxAfterDiscount
    }
    currency{
      name
      currency
      exchangeRate
      symbol
    }
    account {
      id
      name
      fullyQualifiedName
    }
    customer {
      id
      displayName
      firstName
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
    billingAddress {
      freeFormAddressLine
    }
    shipping {
      shipFromAddress {
        freeFormAddressLine
      }
    }
    payment{
      paymentMethod {
        id
        name
        type
      }
    }
    emailDeliveryInfo {
      to
      cc
      bcc
    }
    customFields{
      fieldId
      fieldName
      value
      fieldDefinition {
        id
        name
        inactive
        associatedEntityTypes{
          type
          subtype
        }
      }
    }
    privateMemo
    customerMemo
    itemLines{
      sequence
      description     
      amount
      quantity
      item {
        id
        name  
        sku
      }
      tax {
        taxable
      }
      unitPrice
      class {
        id
        name
      }
    }
  }
}
```

Sample Variables:
``` 
{
	"input": {
		"referenceNumber": "SomeReceiptNumber",
		"transactionDate": "2021-05-16",
		"privateMemo": "Some private memo",
		"customerMemo": "Some Customer memo",
		"customer": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1"
		},
		"currency": {
			"name": "United States Dollar",
			"currency": "USD",
			"exchangeRate": 1
		},
		"billingAddress": {
			"freeFormAddressLine": "Mr. SomeFirstName SomeLastName Some Company 2535 Garcia Ave Mountain View, CA 94043 USA"
		},
		"location": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1"
		},
		"emailDeliveryInfo": {
			"to": "somefirstname@intuit.com",
			"cc": "ccsomefirstname@intuit.com",
			"bcc": "bccsomefirstname@intuit.com"
		},
		"shipping": {
			"shipFromAddress": {
				"freeFormAddressLine": "5601 Headquarters Dr., Plano, CA, 75024, USA"
			}
		},
		"payment": {
			"paymentMethod": {
				"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjVlNGYwZjQ5Y2Q:1"
			}
		},
		"account": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:31"
		},
		"customFields": [
			{
				"fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
				"value": "text cf value"
			}
		],
		"itemLines": [
			{
				"description": "Some Item description",
				"item": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8"
				},
				"tax": {
					"taxable": true
				},
				"unitPrice": "2",
				"class": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
				},
				"quantity": "10",
				"serviceDate": "2021-05-25",
				"amount": "20"
			}
		],
		"discount": {
			"amount": {
				"percentage": false,
				"value": 4
			},
			"applyTaxAfterDiscount": true
		}
	}
}
```    

Sample response:
```
{
  "data": {
    "createRefundReceipt": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6889",
      "amount": 17.32,
      "voided": false,
      "referenceNumber": "SomeReceiptNumber",
      "transactionDate": "2021-05-16",
      "tax": {
        "totalTaxAmount": 1.32
      },
      "metadata": {
        "entityVersion": "0"
      },
      "location": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
        "name": "SomeLocation"
      },
      "discount": {
        "amount": {
          "percentage": false,
          "value": -4.00
        },
        "applyTaxAfterDiscount": true
      },
      "currency": {
        "name": "United States Dollar",
        "currency": "USD",
        "exchangeRate": 1.00,
        "symbol": "$"
      },
      "account": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:31",
        "name": "Inventory Asset",
        "fullyQualifiedName": "Inventory Asset"
      },
      "customer": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
        "displayName": "Mr. SomeFirstName SomeLastName",
        "firstName": "SomeFirstName",
        "lastName": "SomeLastName",
        "companyName": "Some Company",
        "notes": "This is a sample note",
        "website": "https://intuit.com",
        "email": "somefirstname@intuit.com",
        "phone": "(408) 412-9211",
        "mobile": "(408) 412-9211",
        "fax": "(408) 412-9211",
        "contactMethods": [
          {
            "type": "BILLING",
            "primary": true,
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
            "primary": false,
            "address": {
              "streetAddress1": "2535 Garcia Ave",
              "streetAddress2": null,
              "city": "Mountain View",
              "state": "CA",
              "country": "USA",
              "zipCode": "94043"
            }
          }
        ]
      },
      "billingAddress": {
        "freeFormAddressLine": "Mr. SomeFirstName SomeLastName Some Company 2535 Garcia Ave Mountain View, CA 94043 USA\r\n"
      },
      "shipping": {
        "shipFromAddress": {
          "freeFormAddressLine": "5601 Headquarters Dr., Plano, CA, 75024, USA\r\n"
        }
      },
      "payment": {
        "paymentMethod": {
          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjVlNGYwZjQ5Y2Q:1",
          "name": "Cash",
          "type": null
        }
      },
      "emailDeliveryInfo": {
        "to": [
          "somefirstname@intuit.com"
        ],
        "cc": [
          "ccsomefirstname@intuit.com"
        ],
        "bcc": [
          "bccsomefirstname@intuit.com"
        ]
      },
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
          "fieldName": "Sales Rep",
          "value": "text cf value",
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
            "name": "Sales Rep",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE",
                  "SALE_ESTIMATE",
                  "SALE_INVOICE",
                  "SALE_CREDIT",
                  "SALE_REFUND"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000061217",
          "fieldName": "Test SR CF",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000061217",
            "name": "Test SR CF",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE",
                  "SALE_ESTIMATE",
                  "SALE_INVOICE",
                  "SALE_CREDIT",
                  "SALE_REFUND"
                ]
              }
            ]
          }
        }
      ],
      "privateMemo": "Some private memo",
      "customerMemo": "Some Customer memo",
      "itemLines": [
        {
          "sequence": "1",
          "description": "Some Item description",
          "amount": 20.00,
          "quantity": 10,
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8",
            "name": "Rose Bushes",
            "sku": "77-88-99"
          },
          "tax": {
            "taxable": true
          },
          "unitPrice": 2.00,
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
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
mutation updateRefundReceipt($input: UpdateRefundReceiptInput!) {
  updateRefundReceipt(refundReceipt: $input) {
    id
    amount
    voided
    referenceNumber
    transactionDate
    tax {
      totalTaxAmount
    }
    metadata{
      entityVersion
    }
    location{
      id
      name
    }
    discount{
      amount {
        percentage
        value
      }
      applyTaxAfterDiscount
    }
    currency{
      name
      currency
      exchangeRate
      symbol
    }
    account {
      id
      name
      fullyQualifiedName
    }
    customer {
      id
      displayName
      firstName
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
    billingAddress {
      freeFormAddressLine
    }
    shipping {
      shipFromAddress {
        freeFormAddressLine
      }
    }
    payment{
      paymentMethod {
        id
        name
        type
      }
    }
    emailDeliveryInfo {
      to
      cc
      bcc
    }
    customFields{
      fieldId
      fieldName
      value
      fieldDefinition {
        id
        name
        inactive
        associatedEntityTypes{
          type
          subtype
        }
      }
    }
    privateMemo
    customerMemo
    itemLines{
      sequence
      description     
      amount
      quantity
      item {
        id
        name  
        sku
      }
      tax {
        taxable
      }
      unitPrice
      class {
        id
        name
      }
    }
  }
}
```

Required fields:
- id: ID of an existing refundReciept
- metadata: you need to provide the entity version returned from a previous create/update/read operation.
- the entity version must match with the last entity version
  Variables:

```
{
	"input": {
		"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6889",
		"metadata": {
			"entityVersion": "0"
		},
		"referenceNumber": "SomeReceiptNumber",
		"transactionDate": "2021-05-16",
		"privateMemo": "Some private memo - updated",
		"customerMemo": "Some Customer memo - updated",
		"customer": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1"
		},
		"currency": {
			"name": "United States Dollar",
			"currency": "USD",
			"exchangeRate": 1
		},
		"billingAddress": {
			"freeFormAddressLine": "Mr. SomeFirstName SomeLastName Some Company 2535 Garcia Ave Mountain View, CA 94043 USA"
		},
		"location": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1"
		},
		"emailDeliveryInfo": {
			"to": "somefirstname-u@intuit.com",
			"cc": "ccsomefirstname-u@intuit.com",
			"bcc": "bccsomefirstname-u@intuit.com"
		},
		"shipping": {
			"shipFromAddress": {
				"freeFormAddressLine": "5601 Headquarters Dr., Plano, CA, 75024, USA"
			}
		},
		"payment": {
			"paymentMethod": {
				"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjVlNGYwZjQ5Y2Q:1"
			}
		},
		"account": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:31"
		},
		"customFields": [
			{
				"fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
				"value": "text cf value"
			}
		],
		"itemLines": [
			{
				"sequence": "1",
				"description": "Some updated Item description",
				"item": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8"
				},
				"tax": {
					"taxable": true
				},
				"unitPrice": "2",
				"class": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
				},
				"quantity": "10",
				"serviceDate": "2021-05-25",
				"amount": "20"
			},
			{
				"description": "Some another updated Item description",
				"item": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8"
				},
				"tax": {
					"taxable": true
				},
				"unitPrice": "2",
				"class": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
				},
				"quantity": "20",
				"serviceDate": "2021-05-25",
				"amount": "40"
			}
		],
		"discount": {
			"amount": {
				"percentage": false,
				"value": 4
			},
			"applyTaxAfterDiscount": true
		}
	}
}
```

Response:
```
{
  "data": {
    "updateRefundReceipt": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6889",
      "amount": 60.62,
      "voided": false,
      "referenceNumber": "SomeReceiptNumber",
      "transactionDate": "2021-05-16",
      "tax": {
        "totalTaxAmount": 4.62
      },
      "metadata": {
        "entityVersion": "1"
      },
      "location": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
        "name": "SomeLocation"
      },
      "discount": {
        "amount": {
          "percentage": false,
          "value": -4.00
        },
        "applyTaxAfterDiscount": true
      },
      "currency": {
        "name": "United States Dollar",
        "currency": "USD",
        "exchangeRate": 1.00,
        "symbol": "$"
      },
      "account": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:31",
        "name": "Inventory Asset",
        "fullyQualifiedName": "Inventory Asset"
      },
      "customer": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
        "displayName": "Mr. SomeFirstName SomeLastName",
        "firstName": "SomeFirstName",
        "lastName": "SomeLastName",
        "companyName": "Some Company",
        "notes": "This is a sample note",
        "website": "https://intuit.com",
        "email": "somefirstname@intuit.com",
        "phone": "(408) 412-9211",
        "mobile": "(408) 412-9211",
        "fax": "(408) 412-9211",
        "contactMethods": [
          {
            "type": "BILLING",
            "primary": true,
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
            "primary": false,
            "address": {
              "streetAddress1": "2535 Garcia Ave",
              "streetAddress2": null,
              "city": "Mountain View",
              "state": "CA",
              "country": "USA",
              "zipCode": "94043"
            }
          }
        ]
      },
      "billingAddress": {
        "freeFormAddressLine": "Mr. SomeFirstName SomeLastName Some Company 2535 Garcia Ave Mountain View, CA 94043 USA\r\n"
      },
      "shipping": {
        "shipFromAddress": {
          "freeFormAddressLine": "5601 Headquarters Dr., Plano, CA, 75024, USA\r\n"
        }
      },
      "payment": {
        "paymentMethod": {
          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjVlNGYwZjQ5Y2Q:1",
          "name": "Cash",
          "type": null
        }
      },
      "emailDeliveryInfo": {
        "to": [
          "somefirstname-u@intuit.com"
        ],
        "cc": [
          "ccsomefirstname-u@intuit.com"
        ],
        "bcc": [
          "bccsomefirstname-u@intuit.com"
        ]
      },
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
          "fieldName": "Sales Rep",
          "value": "text cf value",
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
            "name": "Sales Rep",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE",
                  "SALE_ESTIMATE",
                  "SALE_INVOICE",
                  "SALE_CREDIT",
                  "SALE_REFUND"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000061217",
          "fieldName": "Test SR CF",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000061217",
            "name": "Test SR CF",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE",
                  "SALE_ESTIMATE",
                  "SALE_INVOICE",
                  "SALE_CREDIT",
                  "SALE_REFUND"
                ]
              }
            ]
          }
        }
      ],
      "privateMemo": "Some private memo - updated",
      "customerMemo": "Some Customer memo - updated",
      "itemLines": [
        {
          "sequence": "1",
          "description": "Some updated Item description",
          "amount": 20.00,
          "quantity": 10,
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8",
            "name": "Rose Bushes",
            "sku": "77-88-99"
          },
          "tax": {
            "taxable": true
          },
          "unitPrice": 2.00,
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
          }
        },
        {
          "sequence": "6",
          "description": "Some another updated Item description",
          "amount": 40.00,
          "quantity": 20,
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8",
            "name": "Rose Bushes",
            "sku": "77-88-99"
          },
          "tax": {
            "taxable": true
          },
          "unitPrice": 2.00,
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
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
mutation deleteRefundReceipt($input: ID!) {
  deleteRefundReceipt(id: $input){
    id
    success
  }
}
```

Required fields:
- id: ID of an existing refundReciept

Variables:
``` 
{
	"input": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6860"
}
```

Response:
```
{
  "data": {
    "deleteRefundReceipt": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6889",
      "success": true
    }
  }
}
```