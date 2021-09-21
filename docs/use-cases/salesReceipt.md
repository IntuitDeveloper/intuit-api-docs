---
layout: default
title: SalesReceipt
nav_order: 16
parent: Use Cases
---

## Sales Receipt

The APIs related to the Sales Receipt entity allow you to manage Sales Receipts for your customers.
The Sales Receipt API provides support for create, read, update and delete operations.

### Operations for Sales Receipt entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the Sales Receipt scope **[com.intuit.quickbooks.accounting]** for the authorization header

### Sample query body

Sample query (Read an Sales Receipt by Id):
```
query readSalesReceipts($id: String!) {
  company{
  salesReceipts (filter: {id: {equals : $id}}) {
    nodes {
      id
      metadata {
        entityVersion
      }
    transactionDate
      referenceNumber
      amount
      location {
        id
        name
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
      currency {
        name
        currency
        symbol
        exchangeRate
      }
      privateMemo
      customerMemo
      itemLines {
        sequence
        description
        amount
        unitPrice
        class {
          id
          name
        }
        item {
          id
          name
            sku
           }
        quantity
        tax {
          taxAmount
          taxGroup {
            id
            name
            code
            description
            saleRates {
              taxRate {
                id
                name
                endDate
                description
              }
            }
          }
          taxable
        }
        
      }
      emailDeliveryInfo {
        to
        cc
        bcc
        status
      }
      shipping {
        shipDate
        shipVia
        shipAddress {
          freeFormAddressLine
        }
        shipFromAddress {
          freeFormAddressLine
        }
        trackingNumber
        shippingAmount
      }
      tax {
        totalTaxAmount
        taxGroup {
            id
            name
            code
            description
            saleRates {
              taxRate {
                id
                name
                endDate
                description
                status
                startDate
                rate
              }
            }
          }
        taxable
        taxDetails {
          taxAmount
          taxableAmount
          taxRate {
            id
            name
            endDate
            description
            status
            startDate
            rate
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
    }
  }
  }
}
```
Required fields:
- id: ID of an existing Sales Receipt

Variables:

```
{
  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6801"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "salesReceipts": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6801",
            "metadata": {
              "entityVersion": "0"
            },
            "transactionDate": "2021-04-16",
            "referenceNumber": null,
            "amount": 119.00,
            "location": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
              "name": "SomeLocation"
            },
            "account": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:26",
              "name": "Undeposited Funds",
              "fullyQualifiedName": "Undeposited Funds"
            },
            "customer": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:418",
              "displayName": "Test Customer",
              "firstName": "Test",
              "lastName": "Customer",
              "companyName": "Customer company",
              "notes": null,
              "website": null,
              "email": "customerTest@customerTest.com",
              "phone": "555-5555",
              "mobile": "666-6666",
              "fax": "777-7777",
              "contactMethods": [
                {
                  "type": "BILLING",
                  "primary": true,
                  "address": {
                    "streetAddress1": "1234 Billing St.",
                    "streetAddress2": null,
                    "city": "Mountain View",
                    "state": "CA",
                    "country": null,
                    "zipCode": "94043"
                  }
                },
                {
                  "type": "SHIPPING",
                  "primary": false,
                  "address": {
                    "streetAddress1": "1234 Shipping St.",
                    "streetAddress2": null,
                    "city": "Mountain View",
                    "state": "CA",
                    "country": null,
                    "zipCode": "94043"
                  }
                }
              ]
            },
            "billingAddress": {
              "freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Billing St.\r\nMountain View, CA  94043"
            },
            "currency": {
              "name": null,
              "currency": "USD",
              "symbol": "$",
              "exchangeRate": 1.00
            },
            "privateMemo": "Test message for sales statement.",
            "customerMemo": "Test message for sales receipt.",
            "itemLines": [
              {
                "sequence": "1",
                "description": "Selling roses to rosie",
                "amount": 100.00,
                "unitPrice": 100.00,
                "class": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
                  "name": "SomeClass"
                },
                "item": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8",
                  "name": "Rose Bushes",
                  "sku": "77-88-99"
                },
                "quantity": 1,
                "tax": {
                  "taxAmount": 9.00,
                  "taxGroup": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6",
                    "name": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
                    "code": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
                    "description": "CA-Santa Clara-Santa Clara",
                    "saleRates": [
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
                          "name": "California State",
                          "endDate": null,
                          "description": "Sales Tax"
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                          "name": "California, Santa Clara County",
                          "endDate": null,
                          "description": "Sales Tax"
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                          "name": "California, Santa Clara County District",
                          "endDate": null,
                          "description": "Sales Tax"
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                          "name": "California State",
                          "endDate": null,
                          "description": "Sales Tax"
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                          "name": "California, Santa Clara County",
                          "endDate": null,
                          "description": "Sales Tax"
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                          "name": "California, Santa Clara County District",
                          "endDate": null,
                          "description": "Sales Tax"
                        }
                      }
                    ]
                  },
                  "taxable": true
                }
              }
            ],
            "emailDeliveryInfo": {
              "to": [
                "customerTest@customerTest.com"
              ],
              "cc": [
                "CCcustomerTest@customerTest.com"
              ],
              "bcc": [
                "BCCcustomerTest@customerTest.com"
              ],
              "status": "NOT_SET"
            },
            "shipping": {
              "shipDate": "2021-04-14",
              "shipVia": "FedEx",
              "shipAddress": {
                "freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043"
              },
              "shipFromAddress": {
                "freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043\r\n"
              },
              "trackingNumber": "12345",
              "shippingAmount": 10.00
            },
            "tax": {
              "totalTaxAmount": 9.00,
              "taxGroup": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6",
                "name": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
                "code": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
                "description": "CA-Santa Clara-Santa Clara",
                "saleRates": [
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
                      "name": "California State",
                      "endDate": null,
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "rate": "6.25%"
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                      "name": "California, Santa Clara County",
                      "endDate": null,
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "rate": "1%"
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                      "name": "California, Santa Clara County District",
                      "endDate": null,
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "rate": "1.75%"
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                      "name": "California State",
                      "endDate": null,
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "rate": "6.25%"
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                      "name": "California, Santa Clara County",
                      "endDate": null,
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "rate": "1%"
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                      "name": "California, Santa Clara County District",
                      "endDate": null,
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "rate": "1.75%"
                    }
                  }
                ]
              },
              "taxable": null,
              "taxDetails": [
                {
                  "taxAmount": 0.00,
                  "taxableAmount": 0.00,
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                    "name": "California State",
                    "endDate": null,
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "rate": "6.25%"
                  }
                },
                {
                  "taxAmount": 1.00,
                  "taxableAmount": 100.00,
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                    "name": "California, Santa Clara County",
                    "endDate": null,
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "rate": "1%"
                  }
                },
                {
                  "taxAmount": 1.75,
                  "taxableAmount": 100.00,
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                    "name": "California, Santa Clara County District",
                    "endDate": null,
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "rate": "1.75%"
                  }
                },
                {
                  "taxAmount": 0.00,
                  "taxableAmount": 0.00,
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                    "name": "California, Santa Clara County",
                    "endDate": null,
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "rate": "1%"
                  }
                },
                {
                  "taxAmount": 0.00,
                  "taxableAmount": 0.00,
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                    "name": "California, Santa Clara County District",
                    "endDate": null,
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "rate": "1.75%"
                  }
                },
                {
                  "taxAmount": 6.25,
                  "taxableAmount": 100.00,
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
                    "name": "California State",
                    "endDate": null,
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "rate": "6.25%"
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
            }
          }
        ]
      }
    }
  }
}
```

## Filter support:

You can choose to **query by id of salesReceipt** (as shown above).

### Create mutation

Mutation:

```
mutation createSalesReceipt($input : CreateSalesReceiptInput!){
  createSalesReceipt(salesReceipt: $input) 
  {
      id
      metadata {
        entityVersion
      }
      transactionDate
      referenceNumber
      amount
      voided
      location {
        id
        name
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
       currency {
        name
        currency
        symbol
        exchangeRate
      }
      privateMemo
      customerMemo
      itemLines {
        sequence
        description
        amount
   unitPrice
     class {
          id
          name
        }
        item {
          id
          name
          sku
         }
        quantity
        tax {
          taxAmount
          taxGroup {
            id
            name
            code
            description
            saleRates {
              taxRate {
                id
                name
                endDate
                description
              }
            }
          }
          taxable
        }
        
      }
      emailDeliveryInfo {
        to
        cc
        bcc
        status
      }
      shipping {
        shipDate
        shipVia
        shipAddress {
          freeFormAddressLine
        }
        shipFromAddress {
          freeFormAddressLine
        }
        trackingNumber
        shippingAmount
      }
      tax {
        totalTaxAmount
        taxGroup {
            id
            name
            code
            description
            saleRates {
              taxRate {
                id
                name
                endDate
                description
                status
                startDate
                rate
              }
            }
          }
        taxable
        taxDetails {
          taxAmount
          taxableAmount
          taxRate {
            id
            name
            endDate
            description
            status
            startDate
            rate
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
    }
}
```

Sample Variables:
``` 
{
	"input": {
		"transactionDate": "2021-04-16",
		"amount": 119,
		"department": {
			"id": "1"
		},
		"account": {
			"id": "26"
		},
		"customer": {
			"id": "418"
		},
		"billingAddress": {
			"freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Billing St.\r\nMountain View, CA  94043"
		},
		"currency": {
			"name": null,
			"currency": "USD",
			"exchangeRate": 1
		},
		"privateMemo": "Test message for sales statement.",
		"customerMemo": "Test message for sales receipt.",
		"itemLines": [
			{
				"description": "Selling roses to rosie",
				"unitPrice": 100,
				"amount": 100,
				"class": {
					"id": "302300000000001849620"
				},
				"item": {
					"id": "8"
				},
				"quantity": 1,
				"tax": {
					"totalTaxAmount": 9,
					"taxGroup": {
						"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6"
					},
					"taxable": true
				}
			}
		],
		"emailDeliveryInfo": {
			"to": [
				"customerTest@customerTest.com"
			],
			"cc": [
				"CCcustomerTest@customerTest.com"
			],
			"bcc": [
				"BCCcustomerTest@customerTest.com"
			]
		},
		"shipping": {
			"shipDate": "2021-04-14",
			"shipVia": "FedEx",
			"shipAddress": {
				"freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043"
			},
			"shipFromAddress": {
				"freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043"
			},
			"trackingNumber": "12345",
			"shippingAmount": 10
		},
		"tax": {
			"totalTaxAmount": 9,
			"taxGroup": {
				"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6"
			},
			"taxable": true
		},
		"payment": {
			"paymentMethod": {
				"id": "1",
				"name": "Cash",
				"type": "CASH"
			}
		}
	}
}
```    

Sample response:
```
{
  "data": {
    "createSalesReceipt": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6860",
      "metadata": {
        "entityVersion": "0"
      },
      "transactionDate": "2021-04-16",
      "referenceNumber": null,
      "amount": 119.00,
      "voided": false,
      "location": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
        "name": "SomeLocation"
      },
      "account": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:26",
        "name": "Undeposited Funds",
        "fullyQualifiedName": "Undeposited Funds"
      },
      "customer": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:418",
        "displayName": "Test Customer",
        "firstName": "Test",
        "lastName": "Customer",
        "companyName": "Customer company",
        "notes": null,
        "website": null,
        "email": "customerTest@customerTest.com",
        "phone": "555-5555",
        "mobile": "666-6666",
        "fax": "777-7777",
        "contactMethods": [
          {
            "type": "BILLING",
            "primary": true,
            "address": {
              "streetAddress1": "1234 Billing St.",
              "streetAddress2": null,
              "city": "Mountain View",
              "state": "CA",
              "country": null,
              "zipCode": "94043"
            }
          },
          {
            "type": "SHIPPING",
            "primary": false,
            "address": {
              "streetAddress1": "1234 Shipping St.",
              "streetAddress2": null,
              "city": "Mountain View",
              "state": "CA",
              "country": null,
              "zipCode": "94043"
            }
          }
        ]
      },
      "billingAddress": {
        "freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Billing St.\r\nMountain View, CA  94043"
      },
      "currency": {
        "name": null,
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "privateMemo": "Test message for sales statement.",
      "customerMemo": "Test message for sales receipt.",
      "itemLines": [
        {
          "sequence": "1",
          "description": "Selling roses to rosie",
          "amount": 100.00,
          "unitPrice": 100.00,
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
          },
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8",
            "name": "Rose Bushes",
            "sku": "77-88-99"
          },
          "quantity": 1,
          "tax": {
            "taxAmount": 9.00,
            "taxGroup": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6",
              "name": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
              "code": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
              "description": "CA-Santa Clara-Santa Clara",
              "saleRates": [
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
                    "name": "California State",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                    "name": "California, Santa Clara County",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                    "name": "California, Santa Clara County District",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                    "name": "California State",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                    "name": "California, Santa Clara County",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                    "name": "California, Santa Clara County District",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                }
              ]
            },
            "taxable": true
          }
        }
      ],
      "emailDeliveryInfo": {
        "to": [
          "customerTest@customerTest.com"
        ],
        "cc": [
          "CCcustomerTest@customerTest.com"
        ],
        "bcc": [
          "BCCcustomerTest@customerTest.com"
        ],
        "status": "NOT_SET"
      },
      "shipping": {
        "shipDate": "2021-04-14",
        "shipVia": "FedEx",
        "shipAddress": {
          "freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043"
        },
        "shipFromAddress": {
          "freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043\r\n"
        },
        "trackingNumber": "12345",
        "shippingAmount": 10.00
      },
      "tax": {
        "totalTaxAmount": 9.00,
        "taxGroup": {
          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6",
          "name": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
          "code": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
          "description": "CA-Santa Clara-Santa Clara",
          "saleRates": [
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
                "name": "California State",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "6.25%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                "name": "California, Santa Clara County",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "1%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                "name": "California, Santa Clara County District",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "1.75%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                "name": "California State",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "6.25%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                "name": "California, Santa Clara County",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "1%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                "name": "California, Santa Clara County District",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "1.75%"
              }
            }
          ]
        },
        "taxable": null,
        "taxDetails": [
          {
            "taxAmount": 0.00,
            "taxableAmount": 0.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
              "name": "California State",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "6.25%"
            }
          },
          {
            "taxAmount": 1.00,
            "taxableAmount": 100.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
              "name": "California, Santa Clara County",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "1%"
            }
          },
          {
            "taxAmount": 1.75,
            "taxableAmount": 100.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
              "name": "California, Santa Clara County District",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "1.75%"
            }
          },
          {
            "taxAmount": 0.00,
            "taxableAmount": 0.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
              "name": "California, Santa Clara County",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "1%"
            }
          },
          {
            "taxAmount": 0.00,
            "taxableAmount": 0.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
              "name": "California, Santa Clara County District",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "1.75%"
            }
          },
          {
            "taxAmount": 6.25,
            "taxableAmount": 100.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
              "name": "California State",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "6.25%"
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
      }
    }
  }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updateSalesReceipt($input : UpdateSalesReceiptInput!){
  updateSalesReceipt(salesReceipt: $input) 
  {
      id
      metadata {
        entityVersion
      }
    transactionDate
      referenceNumber
      voided
      amount
      location {
        id
        name
      }
      account {
        id
        name
        fullyQualifiedName
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
       currency {
        name
        currency
        symbol
        exchangeRate
      }
      privateMemo
      customerMemo
      itemLines {
        sequence
        description
        amount
        unitPrice
        class {
          id
          name
        }
        item {
          id
          name
           sku
         }
        quantity
        tax {
          taxAmount
          taxGroup {
            id
            name
            code
            description
            saleRates {
              taxRate {
                id
                name
                endDate
                description
              }
            }
          }
          taxable
        }
        
      }
      emailDeliveryInfo {
        to
        cc
        bcc
        status
      }
      shipping {
        shipDate
        shipVia
        shipAddress {
          freeFormAddressLine
        }
        shipFromAddress {
          freeFormAddressLine
        }
        trackingNumber
        shippingAmount
      }
      tax {
        totalTaxAmount
        taxGroup {
            id
            name
            code
            description
            saleRates {
              taxRate {
                id
                name
                endDate
                description
                status
                startDate
                rate
              }
            }
          }
        taxable
        taxDetails {
          taxAmount
          taxableAmount
          taxRate {
            id
            name
            endDate
            description
            status
            startDate
            rate
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
    }
}
```

Required fields:
- id: ID of an existing salesReceipt
- metadata: you need to provide the entity version returned from a previous create/update/read operation.
- the entity version must match with the last entity version
Variables:

```
{
	"input": {
		"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6801",
		"metadata": {
			"entityVersion": "0"
		},
		"privateMemo": "111",
		"customerMemo": "Test message for sales receipt updated.",
		"transactionDate": "2021-04-17",
		"amount": 119,
		"department": {
			"id": "1"
		},
		"account": {
			"id": "26"
		},
		"customer": {
			"id": "418"
		},
		"billingAddress": {
			"freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Billing St.\r\nMountain View, CA  94043"
		},
		"currency": {
			"name": null,
			"currency": "USD",
			"exchangeRate": 1
		},
		"itemLines": [
			{
				"description": "Selling roses to rosie",
				"unitPrice": 100,
				"amount": 100,
				"class": {
					"id": "302300000000001849620"
				},
				"item": {
					"id": "8"
				},
				"quantity": 1,
				"tax": {
					"totalTaxAmount": 9,
					"taxGroup": {
						"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6"
					},
					"taxable": true
				}
			}
		],
		"emailDeliveryInfo": {
			"to": [
				"customerTest@customerTest.com"
			],
			"cc": [
				"CCcustomerTest@customerTest.com"
			],
			"bcc": [
				"BCCcustomerTest@customerTest.com"
			]
		},
		"shipping": {
			"shipDate": "2021-04-14",
			"shipVia": "FedEx",
			"shipAddress": {
				"freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043"
			},
			"shipFromAddress": {
				"freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043"
			},
			"trackingNumber": "12345",
			"shippingAmount": 10
		},
		"tax": {
			"totalTaxAmount": 9,
			"taxGroup": {
				"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6"
			},
			"taxable": true
		},
		"payment": {
			"paymentMethod": {
				"id": "1",
				"name": "Cash",
				"type": "CASH"
			}
		}
	}
}
```

Response:
```
{
  "data": {
    "updateSalesReceipt": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6801",
      "metadata": {
        "entityVersion": "1"
      },
      "transactionDate": "2021-04-17",
      "referenceNumber": null,
      "voided": false,
      "amount": 119.00,
      "location": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
        "name": "SomeLocation"
      },
      "account": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:26",
        "name": "Undeposited Funds",
        "fullyQualifiedName": "Undeposited Funds"
      },
      "currency": {
        "name": null,
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "customer": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:418",
        "displayName": "Test Customer",
        "firstName": "Test",
        "lastName": "Customer",
        "companyName": "Customer company",
        "notes": null,
        "website": null,
        "email": "customerTest@customerTest.com",
        "phone": "555-5555",
        "mobile": "666-6666",
        "fax": "777-7777",
        "contactMethods": [
          {
            "type": "BILLING",
            "primary": true,
            "address": {
              "streetAddress1": "1234 Billing St.",
              "streetAddress2": null,
              "city": "Mountain View",
              "state": "CA",
              "country": null,
              "zipCode": "94043"
            }
          },
          {
            "type": "SHIPPING",
            "primary": false,
            "address": {
              "streetAddress1": "1234 Shipping St.",
              "streetAddress2": null,
              "city": "Mountain View",
              "state": "CA",
              "country": null,
              "zipCode": "94043"
            }
          }
        ]
      },
      "billingAddress": {
        "freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Billing St.\r\nMountain View, CA  94043"
      },
      "privateMemo": "111",
      "customerMemo": "Test message for sales receipt updated.",
      "itemLines": [
        {
          "sequence": "9",
          "description": "Selling roses to rosie",
          "amount": 100.00,
          "unitPrice": 100.00,
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
          },
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:8",
            "name": "Rose Bushes",
            "sku": "77-88-99"
          },
          "quantity": 1,
          "tax": {
            "taxAmount": 9.00,
            "taxGroup": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6",
              "name": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
              "code": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
              "description": "CA-Santa Clara-Santa Clara",
              "saleRates": [
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
                    "name": "California State",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                    "name": "California, Santa Clara County",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                    "name": "California, Santa Clara County District",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                    "name": "California State",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                    "name": "California, Santa Clara County",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                    "name": "California, Santa Clara County District",
                    "endDate": null,
                    "description": "Sales Tax"
                  }
                }
              ]
            },
            "taxable": true
          }
        }
      ],
      "emailDeliveryInfo": {
        "to": [
          "customerTest@customerTest.com"
        ],
        "cc": [
          "CCcustomerTest@customerTest.com"
        ],
        "bcc": [
          "BCCcustomerTest@customerTest.com"
        ],
        "status": "NOT_SET"
      },
      "shipping": {
        "shipDate": "2021-04-14",
        "shipVia": "FedEx",
        "shipAddress": {
          "freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043"
        },
        "shipFromAddress": {
          "freeFormAddressLine": "Test Customer\r\nCustomer company\r\n1234 Shipping St.\r\nMountain View, CA  94043\r\n"
        },
        "trackingNumber": "12345",
        "shippingAmount": 10.00
      },
      "tax": {
        "totalTaxAmount": 9.00,
        "taxGroup": {
          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6",
          "name": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
          "code": "f64e34ef1640aabf09d74735150a737ee21ccd6ef5d0dd6f1580cf0f44320d24",
          "description": "CA-Santa Clara-Santa Clara",
          "saleRates": [
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
                "name": "California State",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "6.25%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                "name": "California, Santa Clara County",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "1%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                "name": "California, Santa Clara County District",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "1.75%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                "name": "California State",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "6.25%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                "name": "California, Santa Clara County",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "1%"
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                "name": "California, Santa Clara County District",
                "endDate": null,
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "rate": "1.75%"
              }
            }
          ]
        },
        "taxable": null,
        "taxDetails": [
          {
            "taxAmount": 0.00,
            "taxableAmount": 0.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
              "name": "California State",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "6.25%"
            }
          },
          {
            "taxAmount": 1.00,
            "taxableAmount": 100.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
              "name": "California, Santa Clara County",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "1%"
            }
          },
          {
            "taxAmount": 1.75,
            "taxableAmount": 100.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
              "name": "California, Santa Clara County District",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "1.75%"
            }
          },
          {
            "taxAmount": 0.00,
            "taxableAmount": 0.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
              "name": "California, Santa Clara County",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "1%"
            }
          },
          {
            "taxAmount": 0.00,
            "taxableAmount": 0.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
              "name": "California, Santa Clara County District",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "1.75%"
            }
          },
          {
            "taxAmount": 6.25,
            "taxableAmount": 100.00,
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
              "name": "California State",
              "endDate": null,
              "description": "Sales Tax",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "rate": "6.25%"
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
      }
    }
  }
}
```

### Delete Mutation

Mutation:

``` 
mutation deleteSalesReceipt($input : ID!){
  deleteSalesReceipt(id: $input) 
  {
    id
    success
  }
}
```

Required fields:
- id: ID of an existing salesReceipt

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
    "deleteInvoice": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:32",
      "success": true
    }
  }
}
{
  "data": {
    "deleteSalesReceipt": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6860",
      "success": true
    }
  }
}
```