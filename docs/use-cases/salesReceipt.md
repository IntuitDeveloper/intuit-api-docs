---
layout: default
title: salesReciept
nav_order: 14
parent: Use Cases
---

## Invoice

The APIs related to the salesReciept entity allow you to manage sales receipts for your customer to track accomplished payments.
The salesReciept API provides support for create, read, update and delete operations.

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

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the invoice entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an Invoice by Id):
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
  },
  "extensions": {
    "tracing": {
      "version": 1,
      "startTime": "2021-09-07T20:24:31.287346Z",
      "endTime": "2021-09-07T20:24:33.076995Z",
      "duration": 1790002947,
      "parsing": {
        "startOffset": 2316039,
        "duration": 2063623
      },
      "validation": {
        "startOffset": 3289519,
        "duration": 948142
      },
      "execution": {
        "resolvers": [
          {
            "path": [
              "company"
            ],
            "parentType": "Query",
            "returnType": "Company",
            "fieldName": "company",
            "startOffset": 3408439,
            "duration": 977146
          },
          {
            "path": [
              "company",
              "salesReceipts"
            ],
            "parentType": "Company",
            "returnType": "SalesReceiptConnection",
            "fieldName": "salesReceipts",
            "startOffset": 4465599,
            "duration": 1777863942
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes"
            ],
            "parentType": "SalesReceiptConnection",
            "returnType": "[SalesReceipt!]!",
            "fieldName": "nodes",
            "startOffset": 1782452555,
            "duration": 2799030
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "id"
            ],
            "parentType": "SalesReceipt",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1785339367,
            "duration": 4715
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "transactionDate"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Date",
            "fieldName": "transactionDate",
            "startOffset": 1785423828,
            "duration": 2610
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "referenceNumber"
            ],
            "parentType": "SalesReceipt",
            "returnType": "String",
            "fieldName": "referenceNumber",
            "startOffset": 1785525196,
            "duration": 3286
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "amount"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Amount",
            "fieldName": "amount",
            "startOffset": 1785559823,
            "duration": 2393
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "location"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Location",
            "fieldName": "location",
            "startOffset": 1785600943,
            "duration": 4173
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "location",
              "id"
            ],
            "parentType": "Location",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 1785649397,
            "duration": 2490
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "location",
              "name"
            ],
            "parentType": "Location",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1785682375,
            "duration": 2126
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "billingAddress"
            ],
            "parentType": "SalesReceipt",
            "returnType": "FreeFormAddress",
            "fieldName": "billingAddress",
            "startOffset": 1785811850,
            "duration": 3584
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "billingAddress",
              "freeFormAddressLine"
            ],
            "parentType": "FreeFormAddress",
            "returnType": "String",
            "fieldName": "freeFormAddressLine",
            "startOffset": 1785857038,
            "duration": 2414
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "privateMemo"
            ],
            "parentType": "SalesReceipt",
            "returnType": "String",
            "fieldName": "privateMemo",
            "startOffset": 1785938651,
            "duration": 2445
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customerMemo"
            ],
            "parentType": "SalesReceipt",
            "returnType": "String",
            "fieldName": "customerMemo",
            "startOffset": 1785970045,
            "duration": 2061
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax"
            ],
            "parentType": "SalesReceipt",
            "returnType": "TransactionTaxInfo",
            "fieldName": "tax",
            "startOffset": 1786106684,
            "duration": 3558
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "totalTaxAmount"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "Amount",
            "fieldName": "totalTaxAmount",
            "startOffset": 1786152824,
            "duration": 2318
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxable"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "Boolean",
            "fieldName": "taxable",
            "startOffset": 1786228267,
            "duration": 2637
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "account"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Account",
            "fieldName": "account",
            "startOffset": 1785741232,
            "duration": 599678
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "account",
              "id"
            ],
            "parentType": "Account",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 1786432983,
            "duration": 6029
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "account",
              "name"
            ],
            "parentType": "Account",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1786496428,
            "duration": 4164
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "account",
              "fullyQualifiedName"
            ],
            "parentType": "Account",
            "returnType": "String",
            "fieldName": "fullyQualifiedName",
            "startOffset": 1786549291,
            "duration": 3767
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "currency"
            ],
            "parentType": "SalesReceipt",
            "returnType": "CurrencyInfo",
            "fieldName": "currency",
            "startOffset": 1785903514,
            "duration": 716458
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "shipping"
            ],
            "parentType": "SalesReceipt",
            "returnType": "ShippingDetails",
            "fieldName": "shipping",
            "startOffset": 1786072303,
            "duration": 560016
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "emailDeliveryInfo"
            ],
            "parentType": "SalesReceipt",
            "returnType": "EmailDeliveryInfo",
            "fieldName": "emailDeliveryInfo",
            "startOffset": 1786038915,
            "duration": 654832
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "currency",
              "name"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1786696951,
            "duration": 4395
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "shipping",
              "shipDate"
            ],
            "parentType": "ShippingDetails",
            "returnType": "Date",
            "fieldName": "shipDate",
            "startOffset": 1786700366,
            "duration": 4434
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "currency",
              "currency"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "String",
            "fieldName": "currency",
            "startOffset": 1786740606,
            "duration": 3004
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "emailDeliveryInfo",
              "to"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "[String!]",
            "fieldName": "to",
            "startOffset": 1786763270,
            "duration": 4593
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "currency",
              "symbol"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "String",
            "fieldName": "symbol",
            "startOffset": 1786774978,
            "duration": 2530
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "[TaxDetails]",
            "fieldName": "taxDetails",
            "startOffset": 1786260902,
            "duration": 517071
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "shipping",
              "shipVia"
            ],
            "parentType": "ShippingDetails",
            "returnType": "String",
            "fieldName": "shipVia",
            "startOffset": 1786802347,
            "duration": 3417
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "currency",
              "exchangeRate"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "Amount",
            "fieldName": "exchangeRate",
            "startOffset": 1786807258,
            "duration": 2296
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "TaxGroup",
            "fieldName": "taxGroup",
            "startOffset": 1786192369,
            "duration": 626532
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "emailDeliveryInfo",
              "cc"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "[String!]",
            "fieldName": "cc",
            "startOffset": 1786818407,
            "duration": 3054
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 1786850585,
            "duration": 4444
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "emailDeliveryInfo",
              "bcc"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "[String!]",
            "fieldName": "bcc",
            "startOffset": 1786862688,
            "duration": 2611
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "id"
            ],
            "parentType": "TaxGroup",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1786891793,
            "duration": 5443
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 1786900369,
            "duration": 3166
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "emailDeliveryInfo",
              "status"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "EmailStatus",
            "fieldName": "status",
            "startOffset": 1786903535,
            "duration": 2674
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "shipping",
              "trackingNumber"
            ],
            "parentType": "ShippingDetails",
            "returnType": "String",
            "fieldName": "trackingNumber",
            "startOffset": 1786908289,
            "duration": 2949
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "shipping",
              "shippingAmount"
            ],
            "parentType": "ShippingDetails",
            "returnType": "Amount",
            "fieldName": "shippingAmount",
            "startOffset": 1786942540,
            "duration": 2395
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "name"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1786969343,
            "duration": 3112
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "code"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "code",
            "startOffset": 1787007675,
            "duration": 2656
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 1787007231,
            "duration": 3121
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "description"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1787040268,
            "duration": 2181
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 1787057527,
            "duration": 2649
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "shipping",
              "shipAddress"
            ],
            "parentType": "ShippingDetails",
            "returnType": "FreeFormAddress",
            "fieldName": "shipAddress",
            "startOffset": 1786837111,
            "duration": 233007
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates"
            ],
            "parentType": "TaxGroup",
            "returnType": "[TaxGroupRate]",
            "fieldName": "saleRates",
            "startOffset": 1787071639,
            "duration": 4325
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines"
            ],
            "parentType": "SalesReceipt",
            "returnType": "[SalesTransactionItemLine]",
            "fieldName": "itemLines",
            "startOffset": 1786000113,
            "duration": 1090105
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "payment"
            ],
            "parentType": "SalesReceipt",
            "returnType": "PaymentInfo",
            "fieldName": "payment",
            "startOffset": 1786306872,
            "duration": 802329
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Customer",
            "fieldName": "customer",
            "startOffset": 1785780397,
            "duration": 1360038
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 1787152789,
            "duration": 2761
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "shipping",
              "shipAddress",
              "freeFormAddressLine"
            ],
            "parentType": "FreeFormAddress",
            "returnType": "String",
            "fieldName": "freeFormAddressLine",
            "startOffset": 1787152336,
            "duration": 5309
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "sequence"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "String",
            "fieldName": "sequence",
            "startOffset": 1787166333,
            "duration": 4484
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "shipping",
              "shipFromAddress"
            ],
            "parentType": "ShippingDetails",
            "returnType": "FreeFormAddress",
            "fieldName": "shipFromAddress",
            "startOffset": 1786872785,
            "duration": 298220
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 1787192966,
            "duration": 2366
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1786941027,
            "duration": 270189
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "description"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1787211130,
            "duration": 2784
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "id"
            ],
            "parentType": "Customer",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 1787225823,
            "duration": 5483
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "shipping",
              "shipFromAddress",
              "freeFormAddressLine"
            ],
            "parentType": "FreeFormAddress",
            "returnType": "String",
            "fieldName": "freeFormAddressLine",
            "startOffset": 1787238031,
            "duration": 5546
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "amount"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Amount",
            "fieldName": "amount",
            "startOffset": 1787247543,
            "duration": 2336
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1787273571,
            "duration": 3798
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "displayName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "displayName",
            "startOffset": 1787295223,
            "duration": 5229
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 1787297049,
            "duration": 4230
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "unitPrice"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Amount",
            "fieldName": "unitPrice",
            "startOffset": 1787305724,
            "duration": 2844
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787313803,
            "duration": 2486
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1787347232,
            "duration": 2586
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "firstName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "firstName",
            "startOffset": 1787358029,
            "duration": 4768
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 1787358350,
            "duration": 4769
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1787379963,
            "duration": 2418
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1787416672,
            "duration": 3739
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "lastName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "lastName",
            "startOffset": 1787417527,
            "duration": 4354
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787095355,
            "duration": 326241
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1787474296,
            "duration": 4152
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "companyName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "companyName",
            "startOffset": 1787476264,
            "duration": 4235
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787133601,
            "duration": 347128
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1787502905,
            "duration": 5297
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 1787513565,
            "duration": 4146
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "quantity"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Int",
            "fieldName": "quantity",
            "startOffset": 1787518817,
            "duration": 4975
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787229450,
            "duration": 295345
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "notes"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "notes",
            "startOffset": 1787533622,
            "duration": 4192
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "payment",
              "paymentMethod"
            ],
            "parentType": "PaymentInfo",
            "returnType": "PaymentMethod",
            "fieldName": "paymentMethod",
            "startOffset": 1787198824,
            "duration": 369982
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787569666,
            "duration": 4703
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1787574896,
            "duration": 5542
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787218784,
            "duration": 362726
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 1787580916,
            "duration": 4742
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1787584154,
            "duration": 4557
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "website"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "website",
            "startOffset": 1787589233,
            "duration": 4074
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1787603784,
            "duration": 4850
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1787631389,
            "duration": 4700
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787641008,
            "duration": 5066
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "email"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "email",
            "startOffset": 1787651123,
            "duration": 4216
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787662745,
            "duration": 4136
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787314885,
            "duration": 359798
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1787680951,
            "duration": 5532
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1787694829,
            "duration": 4986
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "payment",
              "paymentMethod",
              "id"
            ],
            "parentType": "PaymentMethod",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 1787704355,
            "duration": 4772
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1787704355,
            "duration": 4772
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "phone"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "phone",
            "startOffset": 1787706846,
            "duration": 3908
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1787717444,
            "duration": 4251
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787409678,
            "duration": 321602
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 1787735396,
            "duration": 5105
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787747037,
            "duration": 4439
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1787755145,
            "duration": 4535
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "mobile"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "mobile",
            "startOffset": 1787763174,
            "duration": 4051
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1787769330,
            "duration": 3670
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "payment",
              "paymentMethod",
              "name"
            ],
            "parentType": "PaymentMethod",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787769548,
            "duration": 4666
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1787769548,
            "duration": 4666
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787423237,
            "duration": 357471
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "class"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Class",
            "fieldName": "class",
            "startOffset": 1787382579,
            "duration": 414085
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 1787805636,
            "duration": 4863
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1787806104,
            "duration": 4484
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1787810297,
            "duration": 5697
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1787810297,
            "duration": 5697
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1787815779,
            "duration": 4724
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1787820243,
            "duration": 3860
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "fax"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "fax",
            "startOffset": 1787820243,
            "duration": 3860
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1787842289,
            "duration": 4842
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1787871071,
            "duration": 4831
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787878115,
            "duration": 4619
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787878115,
            "duration": 4625
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1787879453,
            "duration": 4136
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods"
            ],
            "parentType": "Customer",
            "returnType": "[ContactMethod!]!",
            "fieldName": "contactMethods",
            "startOffset": 1787879453,
            "duration": 6055
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "payment",
              "paymentMethod",
              "type"
            ],
            "parentType": "PaymentMethod",
            "returnType": "PaymentMethodTypeEnum",
            "fieldName": "type",
            "startOffset": 1787880522,
            "duration": 5959
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "class",
              "id"
            ],
            "parentType": "Class",
            "returnType": "String",
            "fieldName": "id",
            "startOffset": 1787882171,
            "duration": 5841
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1787898408,
            "duration": 3598
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1787907813,
            "duration": 4964
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1787930333,
            "duration": 3433
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1787940520,
            "duration": 4518
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1787940520,
            "duration": 4538
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "class",
              "name"
            ],
            "parentType": "Class",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787949946,
            "duration": 4496
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              0,
              "type"
            ],
            "parentType": "ContactMethod",
            "returnType": "ContactType",
            "fieldName": "type",
            "startOffset": 1787966501,
            "duration": 4724
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1787973095,
            "duration": 4457
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787582455,
            "duration": 394891
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1787979378,
            "duration": 4268
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1787982757,
            "duration": 3540
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1788000871,
            "duration": 4354
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1788000871,
            "duration": 4354
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788002717,
            "duration": 4407
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              0,
              "primary"
            ],
            "parentType": "ContactMethod",
            "returnType": "Boolean",
            "fieldName": "primary",
            "startOffset": 1788029393,
            "duration": 4470
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1788034125,
            "duration": 4501
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788039247,
            "duration": 5306
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1788057850,
            "duration": 5071
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1788060727,
            "duration": 4064
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1788063321,
            "duration": 3550
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788080617,
            "duration": 4164
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              0,
              "address"
            ],
            "parentType": "ContactMethod",
            "returnType": "Address",
            "fieldName": "address",
            "startOffset": 1788090170,
            "duration": 6199
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1788093154,
            "duration": 4285
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1788119789,
            "duration": 3376
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1788121673,
            "duration": 4570
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1788133373,
            "duration": 4192
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1788157291,
            "duration": 2448
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "item"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Item",
            "fieldName": "item",
            "startOffset": 1787450853,
            "duration": 709026
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              0,
              "address",
              "streetAddress1"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress1",
            "startOffset": 1788166208,
            "duration": 3582
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1788168919,
            "duration": 3632
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1788189782,
            "duration": 2340
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              0,
              "address",
              "streetAddress2"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress2",
            "startOffset": 1788202912,
            "duration": 2484
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1788219702,
            "duration": 4420
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787871175,
            "duration": 359246
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              0,
              "address",
              "city"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "city",
            "startOffset": 1788235498,
            "duration": 2445
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788233624,
            "duration": 4558
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1788235304,
            "duration": 4300
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788233624,
            "duration": 4558
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787502905,
            "duration": 745695
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              0,
              "address",
              "state"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "state",
            "startOffset": 1788268428,
            "duration": 2516
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1787646956,
            "duration": 641692
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "metadata"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Metadata",
            "fieldName": "metadata",
            "startOffset": 1785383235,
            "duration": 2907431
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "item",
              "id"
            ],
            "parentType": "InventoryItem",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 1788289238,
            "duration": 5412
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1788295972,
            "duration": 4419
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              0,
              "address",
              "country"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "country",
            "startOffset": 1788300100,
            "duration": 2368
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788318885,
            "duration": 3280
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1788322172,
            "duration": 5929
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1788325449,
            "duration": 4574
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              0,
              "address",
              "zipCode"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "zipCode",
            "startOffset": 1788332183,
            "duration": 2296
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "TaxInfo",
            "fieldName": "tax",
            "startOffset": 1787593626,
            "duration": 742833
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "metadata",
              "entityVersion"
            ],
            "parentType": "Metadata",
            "returnType": "String!",
            "fieldName": "entityVersion",
            "startOffset": 1788354020,
            "duration": 4343
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "item",
              "name"
            ],
            "parentType": "InventoryItem",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1788353345,
            "duration": 4699
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1788369562,
            "duration": 4274
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1788386016,
            "duration": 3605
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788393483,
            "duration": 3478
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1788399644,
            "duration": 3990
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              1,
              "type"
            ],
            "parentType": "ContactMethod",
            "returnType": "ContactType",
            "fieldName": "type",
            "startOffset": 1788401622,
            "duration": 2593
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxAmount"
            ],
            "parentType": "TaxInfo",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 1788404422,
            "duration": 4066
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "item",
              "sku"
            ],
            "parentType": "InventoryItem",
            "returnType": "String",
            "fieldName": "sku",
            "startOffset": 1788413390,
            "duration": 3269
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1788425527,
            "duration": 2942
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1788443710,
            "duration": 2952
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              1,
              "primary"
            ],
            "parentType": "ContactMethod",
            "returnType": "Boolean",
            "fieldName": "primary",
            "startOffset": 1788450429,
            "duration": 2567
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1788455810,
            "duration": 3667
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1788459294,
            "duration": 2407
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1788478023,
            "duration": 2360
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              1,
              "address"
            ],
            "parentType": "ContactMethod",
            "returnType": "Address",
            "fieldName": "address",
            "startOffset": 1788482527,
            "duration": 3593
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1788492014,
            "duration": 2433
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1788493591,
            "duration": 2580
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxable"
            ],
            "parentType": "TaxInfo",
            "returnType": "Boolean",
            "fieldName": "taxable",
            "startOffset": 1788498930,
            "duration": 3000
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1788509839,
            "duration": 2423
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1788524670,
            "duration": 2287
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              1,
              "address",
              "streetAddress1"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress1",
            "startOffset": 1788526505,
            "duration": 2254
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1788529313,
            "duration": 2554
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1788544506,
            "duration": 2241
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              1,
              "address",
              "streetAddress2"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress2",
            "startOffset": 1788558937,
            "duration": 2174
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 1788563159,
            "duration": 2261
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              1,
              "address",
              "city"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "city",
            "startOffset": 1788589519,
            "duration": 2029
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 1788595968,
            "duration": 2409
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788601127,
            "duration": 2671
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788611281,
            "duration": 2899
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              1,
              "address",
              "state"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "state",
            "startOffset": 1788620054,
            "duration": 2168
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              1,
              "address",
              "country"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "country",
            "startOffset": 1788650286,
            "duration": 1937
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 1788664525,
            "duration": 2776
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "customer",
              "contactMethods",
              1,
              "address",
              "zipCode"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "zipCode",
            "startOffset": 1788679823,
            "duration": 2047
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup"
            ],
            "parentType": "TaxInfo",
            "returnType": "TaxGroup",
            "fieldName": "taxGroup",
            "startOffset": 1788454781,
            "duration": 493383
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "id"
            ],
            "parentType": "TaxGroup",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1789013845,
            "duration": 4343
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "name"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1789054700,
            "duration": 2673
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "code"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "code",
            "startOffset": 1789087146,
            "duration": 2420
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "description"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1789117690,
            "duration": 2115
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates"
            ],
            "parentType": "TaxGroup",
            "returnType": "[TaxGroupRate]",
            "fieldName": "saleRates",
            "startOffset": 1789154497,
            "duration": 3923
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1789204617,
            "duration": 282589
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1789556185,
            "duration": 4273
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1789264023,
            "duration": 307838
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1789315538,
            "duration": 281505
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1789602476,
            "duration": 2711
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1789639777,
            "duration": 2441
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1789643740,
            "duration": 4320
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1789365573,
            "duration": 297759
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1789665729,
            "duration": 4271
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1789673578,
            "duration": 2283
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1789417872,
            "duration": 269671
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1789688099,
            "duration": 2886
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1789710027,
            "duration": 2697
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 1789467534,
            "duration": 256650
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1789726470,
            "duration": 2820
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1789733702,
            "duration": 4273
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1789749602,
            "duration": 2646
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1789758663,
            "duration": 4614
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1789762500,
            "duration": 2408
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1789777438,
            "duration": 2839
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1789783901,
            "duration": 2231
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 1789784514,
            "duration": 3801
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1789805254,
            "duration": 2692
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1789812973,
            "duration": 2724
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 1789825606,
            "duration": 2362
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1789842194,
            "duration": 2441
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1789847436,
            "duration": 2364
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 1789862771,
            "duration": 2476
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1789875780,
            "duration": 2317
          },
          {
            "path": [
              "company",
              "salesReceipts",
              "nodes",
              0,
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 1789896373,
            "duration": 2240
          }
        ]
      }
    },
    "ftv1": "GgsIgZXfiQYQwNHeJCIMCP+U34kGENjBgokBWO3Fx9UGcoVUYoJUCgdjb21wYW55GgdDb21wYW55QI7lzwFIl8aLAmLcUwoNc2FsZXNSZWNlaXB0cxoWU2FsZXNSZWNlaXB0Q29ubmVjdGlvbkCDp5ACSLHk8NEGYp5TCgVub2RlcxoQW1NhbGVzUmVjZWlwdCFdIUDBhvjRBkjqhaPTBmLeUhAAYiMKAmlkGgNJRCFAh5yo0wZIlMmo0wZqDFNhbGVzUmVjZWlwdGIxCg90cmFuc2FjdGlvbkRhdGUaBERhdGVA4Kyt0wZIlNut0wZqDFNhbGVzUmVjZWlwdGIzCg9yZWZlcmVuY2VOdW1iZXIaBlN0cmluZ0DZxbPTBkjL57PTBmoMU2FsZXNSZWNlaXB0YioKBmFtb3VudBoGQW1vdW50QJ3TtdMGSM/qtdMGagxTYWxlc1JlY2VpcHRidAoIbG9jYXRpb24aCExvY2F0aW9uQOWUuNMGSKO6uNMGYh4KAmlkGgJJREDLj7vTBkjWqLvTBmoITG9jYXRpb25iJAoEbmFtZRoGU3RyaW5nQLeQvdMGSIanvdMGaghMb2NhdGlvbmoMU2FsZXNSZWNlaXB0YncKDmJpbGxpbmdBZGRyZXNzGg9GcmVlRm9ybUFkZHJlc3NAoITF0wZIpKjF0wZiOgoTZnJlZUZvcm1BZGRyZXNzTGluZRoGU3RyaW5nQL7lx9MGSIv/x9MGag9GcmVlRm9ybUFkZHJlc3NqDFNhbGVzUmVjZWlwdGIvCgtwcml2YXRlTWVtbxoGU3RyaW5nQObizNMGSM38zNMGagxTYWxlc1JlY2VpcHRiMAoMY3VzdG9tZXJNZW1vGgZTdHJpbmdAgtjO0wZI/uzO0wZqDFNhbGVzUmVjZWlwdGLHJgoDdGF4GhJUcmFuc2FjdGlvblRheEluZm9AuYPX0wZIs6XX0wZiOAoOdG90YWxUYXhBbW91bnQaBkFtb3VudED569nTBkjThNrTBmoSVHJhbnNhY3Rpb25UYXhJbmZvYjIKB3RheGFibGUaB0Jvb2xlYW5A87ne0wZIjtXe0wZqElRyYW5zYWN0aW9uVGF4SW5mb2KAFAoKdGF4RGV0YWlscxoMW1RheERldGFpbHNdQNy44NMGSImVgNQGYp4DEABiKwoJdGF4QW1vdW50GgZBbW91bnRAvLqE1AZIoOSE1AZqClRheERldGFpbHNiLwoNdGF4YWJsZUFtb3VudBoGQW1vdW50QJu+h9QGSNrdh9QGagpUYXhEZXRhaWxzYrsCCgd0YXhSYXRlGgdUYXhSYXRlQI77idQGSKzFmtQGYh4KAmlkGgNJRCFAkKKe1AZIxcie1AZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQP7aoNQGSIn1oNQGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVA8OCi1AZIt/mi1AZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0Cp4KTUBki9+KTUBmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0DTgKfUBki3pqfUBmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVAvsKq1AZIgfCq1AZqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQPWesdQGSPvOsdQGagdUYXhSYXRlagpUYXhEZXRhaWxzYp4DEAFiKwoJdGF4QW1vdW50GgZBbW91bnRAioCO1AZI0qCO1AZqClRheERldGFpbHNiLwoNdGF4YWJsZUFtb3VudBoGQW1vdW50QOmIkdQGSM+kkdQGagpUYXhEZXRhaWxzYrsCCgd0YXhSYXRlGgdUYXhSYXRlQISwk9QGSMi3p9QGYh4KAmlkGgNJRCFAgqSs1AZIi9ms1AZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQIuusNQGSLncsNQGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAwY+01AZI1r+01AZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0CW/7fUBkiBs7jUBmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0CX17vUBkj4g7zUBmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVAwLC/1AZI6d+/1AZqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQM2CzdQGSJO6zdQGagdUYXhSYXRlagpUYXhEZXRhaWxzYp4DEAJiKwoJdGF4QW1vdW50GgZBbW91bnRAsfGW1AZIv46X1AZqClRheERldGFpbHNiLwoNdGF4YWJsZUFtb3VudBoGQW1vdW50QLaqmdQGSNnDmdQGagpUYXhEZXRhaWxzYrsCCgd0YXhSYXRlGgdUYXhSYXRlQOfHm9QGSMXerdQGYh4KAmlkGgNJRCFAybey1AZIsuuy1AZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQPeCttQGSNqsttQGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVA5K651AZIrtm51AZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0CWw7zUBkjO57zUBmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0Cp0r/UBkjT+r/UBmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVAyKHD1AZIkczD1AZqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQJiuydQGSNvZydQGagdUYXhSYXRlagpUYXhEZXRhaWxzYp4DEANiKwoJdGF4QW1vdW50GgZBbW91bnRA0tif1AZIxIKg1AZqClRheERldGFpbHNiLwoNdGF4YWJsZUFtb3VudBoGQW1vdW50QJy6o9QGSMDqo9QGagpUYXhEZXRhaWxzYrsCCgd0YXhSYXRlGgdUYXhSYXRlQIC0p9QGSNewvdQGYh4KAmlkGgNJRCFAnoDF1AZIkbTF1AZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQPv+yNQGSO+oydQGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVA7tnM1AZI1YbN1AZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0CCptDUBkiB0NDUBmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0Dp9NTUBkjHmtXUBmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVAm4TY1AZIhbDY1AZqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQKCI3tQGSOSq3tQGagdUYXhSYXRlagpUYXhEZXRhaWxzYp4DEARiKwoJdGF4QW1vdW50GgZBbW91bnRAtPas1AZIpaGt1AZqClRheERldGFpbHNiLwoNdGF4YWJsZUFtb3VudBoGQW1vdW50QKeGsdQGSLK2sdQGagpUYXhEZXRhaWxzYrsCCgd0YXhSYXRlGgdUYXhSYXRlQLqItdQGSIWu3NQGYh4KAmlkGgNJRCFAsJTh1AZIgMfh1AZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQLK25tQGSM3b5tQGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAn9zo1AZI4ffo1AZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0Cr8+rUBkiPjuvUBmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0Cm++zUBkiUk+3UBmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVAgP3u1AZIoJXv1AZqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQJeT89QGSIyx89QGagdUYXhSYXRlagpUYXhEZXRhaWxzYp4DEAViKwoJdGF4QW1vdW50GgZBbW91bnRAibu61AZIh/G61AZqClRheERldGFpbHNiLwoNdGF4YWJsZUFtb3VudBoGQW1vdW50QMfgvtQGSPGQv9QGagpUYXhEZXRhaWxzYrsCCgd0YXhSYXRlGgdUYXhSYXRlQIbhwtQGSOLq2NQGYh4KAmlkGgNJRCFAxqbe1AZI1eTe1AZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQICV4tQGSK654tQGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVA+snk1AZIneXk1AZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0Cs0ObUBkig6ObUBmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0Cm0OjUBkjJ6ejUBmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVA5c7q1AZI7Obq1AZqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQLmk79QGSLjB79QGagdUYXhSYXRlagpUYXhEZXRhaWxzahJUcmFuc2FjdGlvblRheEluZm9ioBEKCHRheEdyb3VwGghUYXhHcm91cECVotzTBkiq1oLUBmIfCgJpZBoDSUQhQP7+htQGSJ60h9QGaghUYXhHcm91cGIkCgRuYW1lGgZTdHJpbmdA7tiL1AZIivyL1AZqCFRheEdyb3VwYiQKBGNvZGUaBlN0cmluZ0DSg47UBkiLnY7UBmoIVGF4R3JvdXBiKwoLZGVzY3JpcHRpb24aBlN0cmluZ0DGgZDUBkipmJDUBmoIVGF4R3JvdXBizw8KCXNhbGVSYXRlcxoOW1RheEdyb3VwUmF0ZV1AgfeR1AZI4qCS1AZiwgIQAGK9AgoHdGF4UmF0ZRoHVGF4UmF0ZUDO3ZXUBkiwh6vUBmIeCgJpZBoDSUQhQJ/YsNQGSISPsdQGagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0DM27TUBkjIj7XUBmoHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQJrKuNQGSNL6uNQGagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA98e81AZI4PS81AZqB1RheFJhdGViKwoGc3RhdHVzGgxBY3RpdmVTdGF0dXNAv//A1AZI3rDB1AZqB1RheFJhdGViJgoJc3RhcnREYXRlGgREYXRlQLK1xNQGSIXaxNQGagdUYXhSYXRlYiMKBHJhdGUaBlN0cmluZ0Dw48rUBki1ksvUBmoHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlYsICEAFivQIKB3RheFJhdGUaB1RheFJhdGVAkPea1AZIt5mx1AZiHgoCaWQaA0lEIUCpk7fUBkipzbfUBmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA25e71AZI0MO71AZqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUCY5L7UBkikkr/UBmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQKThwtQGSNiQw9QGagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQL2txtQGSKjRxtQGagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUC6x8nUBkiA7MnUBmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdAqsTP1AZI4+7P1AZqB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLCAhACYr0CCgd0YXhSYXRlGgdUYXhSYXRlQObnoNQGSIr1ttQGYh4KAmlkGgNJRCFAv4a/1AZI1r+/1AZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQKmXw9QGSJDGw9QGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAv/7G1AZI9KvH1AZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0C91crUBki/gMvUBmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0DwqM7UBkiw1M7UBmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVAvODS1AZI6ofT1AZqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQNjv2NQGSOG12dQGagdUYXhSYXRlagxUYXhHcm91cFJhdGViwgIQA2K9AgoHdGF4UmF0ZRoHVGF4UmF0ZUCvzKbUBkiyq7rUBmIeCgJpZBoDSUQhQL+Gv9QGSJ/Av9QGagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0Cpl8PUBkiQxsPUBmoHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQLn+xtQGSL+rx9QGagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdAvdXK1AZIp4HL1AZqB1RheFJhdGViKwoGc3RhdHVzGgxBY3RpdmVTdGF0dXNA07vO1AZIj97O1AZqB1RheFJhdGViJgoJc3RhcnREYXRlGgREYXRlQMiG0tQGSPGz0tQGagdUYXhSYXRlYiMKBHJhdGUaBlN0cmluZ0DY79jUBkjTn9nUBmoHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlYsICEAVivQIKB3RheFJhdGUaB1RheFJhdGVAq5Kx1AZIlKrJ1AZiHgoCaWQaA0lEIUDck87UBkjtx87UBmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAjPXR1AZImpfS1AZqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDJmNTUBkiqstTUBmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQMuW1tQGSKey1tQGagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQOT92NQGSImr2dQGagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUCp1tzUBkiggt3UBmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdAs87i1AZI//Pi1AZqB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLCAhAEYr0CCgd0YXhSYXRlGgdUYXhSYXRlQJWkrNQGSNDv2dQGYh4KAmlkGgNJRCFAwL3e1AZIge7e1AZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQLWA49QGSICn49QGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAg9fl1AZIyfTl1AZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0CL4ufUBkjw+ufUBmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0Cj2+nUBki28+nUBmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVAs+nr1AZItoDs1AZqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQN3z79QGSIyR8NQGagdUYXhSYXRlagxUYXhHcm91cFJhdGVqCFRheEdyb3VwahJUcmFuc2FjdGlvblRheEluZm9qDFNhbGVzUmVjZWlwdGKjAQoHYWNjb3VudBoHQWNjb3VudECO3sDTBkitweXTBmIdCgJpZBoCSURA5P3q0wZItLnr0wZqB0FjY291bnRiIwoEbmFtZRoGU3RyaW5nQNnr7tMGSO2V79MGagdBY2NvdW50YjEKEmZ1bGx5UXVhbGlmaWVkTmFtZRoGU3RyaW5nQLWH8tMGSPar8tMGagdBY2NvdW50agxTYWxlc1JlY2VpcHRi6AEKCGN1cnJlbmN5GgxDdXJyZW5jeUluZm9AntDK0wZI3cT20wZiKAoEbmFtZRoGU3RyaW5nQJeK+9MGSMaz+9MGagxDdXJyZW5jeUluZm9iLAoIY3VycmVuY3kaBlN0cmluZ0Ck3f3TBkjG+v3TBmoMQ3VycmVuY3lJbmZvYioKBnN5bWJvbBoGU3RyaW5nQOHp/9MGSNWCgNQGagxDdXJyZW5jeUluZm9iMAoMZXhjaGFuZ2VSYXRlGgZBbW91bnRAkeWB1AZI+f2B1AZqDEN1cnJlbmN5SW5mb2oMU2FsZXNSZWNlaXB0YvgDCghzaGlwcGluZxoPU2hpcHBpbmdEZXRhaWxzQLv31NMGSOuf99MGYi0KCHNoaXBEYXRlGgREYXRlQKSk+9MGSNHN+9MGag9TaGlwcGluZ0RldGFpbHNiLgoHc2hpcFZpYRoGU3RyaW5nQOTAgdQGSInkgdQGag9TaGlwcGluZ0RldGFpbHNiNQoOdHJhY2tpbmdOdW1iZXIaBlN0cmluZ0DG+ofUBkiBmojUBmoPU2hpcHBpbmdEZXRhaWxzYjUKDnNoaXBwaW5nQW1vdW50GgZBbW91bnRAr4aK1AZIjZ6K1AZqD1NoaXBwaW5nRGV0YWlsc2J3CgtzaGlwQWRkcmVzcxoPRnJlZUZvcm1BZGRyZXNzQN3Og9QGSI39kdQGYjoKE2ZyZWVGb3JtQWRkcmVzc0xpbmUaBlN0cmluZ0Du8ZbUBkjzp5fUBmoPRnJlZUZvcm1BZGRyZXNzag9TaGlwcGluZ0RldGFpbHNiewoPc2hpcEZyb21BZGRyZXNzGg9GcmVlRm9ybUFkZHJlc3NAguaF1AZIlY6Y1AZiOgoTZnJlZUZvcm1BZGRyZXNzTGluZRoGU3RyaW5nQIaQnNQGSKvGnNQGag9GcmVlRm9ybUFkZHJlc3NqD1NoaXBwaW5nRGV0YWlsc2oMU2FsZXNSZWNlaXB0YocCChFlbWFpbERlbGl2ZXJ5SW5mbxoRRW1haWxEZWxpdmVyeUluZm9AvPLS0wZImIH70wZiLgoCdG8aCVtTdHJpbmchXUCQkP/TBkigwP/TBmoRRW1haWxEZWxpdmVyeUluZm9iLgoCY2MaCVtTdHJpbmchXUCZv4LUBkjY3oLUBmoRRW1haWxEZWxpdmVyeUluZm9iLwoDYmNjGglbU3RyaW5nIV1AvJaF1AZI57OF1AZqEUVtYWlsRGVsaXZlcnlJbmZvYjQKBnN0YXR1cxoLRW1haWxTdGF0dXNA6dWH1AZItPGH1AZqEUVtYWlsRGVsaXZlcnlJbmZvagxTYWxlc1JlY2VpcHRi1hEKCWl0ZW1MaW5lcxoaW1NhbGVzVHJhbnNhY3Rpb25JdGVtTGluZV1AnMPQ0wZI9puT1AZikhEQAGI4CghzZXF1ZW5jZRoGU3RyaW5nQK3cl9QGSNqImNQGahhTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmViOwoLZGVzY3JpcHRpb24aBlN0cmluZ0DcuJrUBkjY15rUBmoYU2FsZXNUcmFuc2FjdGlvbkl0ZW1MaW5lYjYKBmFtb3VudBoGQW1vdW50QMDVnNQGSMntnNQGahhTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmViOQoJdW5pdFByaWNlGgZBbW91bnRAzJyg1AZI1rqg1AZqGFNhbGVzVHJhbnNhY3Rpb25JdGVtTGluZWI1CghxdWFudGl0eRoDSW50QMmfrdQGSNbUrdQGahhTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmVieAoFY2xhc3MaBUNsYXNzQID3pNQGSMOrvtQGYh8KAmlkGgZTdHJpbmdA6LjD1AZI+/PD1AZqBUNsYXNzYiEKBG5hbWUaBlN0cmluZ0DvyMfUBkiE88fUBmoFQ2xhc3NqGFNhbGVzVHJhbnNhY3Rpb25JdGVtTGluZWKsAQoEaXRlbRoESXRlbUD8jKnUBkjLwdTUBmIjCgJpZBoCSURAlKTc1AZIwtjc1AZqDUludmVudG9yeUl0ZW1iKQoEbmFtZRoGU3RyaW5nQPiX4NQGSKDI4NQGag1JbnZlbnRvcnlJdGVtYigKA3NrdRoGU3RyaW5nQMvq49QGSKSM5NQGag1JbnZlbnRvcnlJdGVtahhTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmViwwwKA3RheBoHVGF4SW5mb0CD6bHUBkibnt/UBmIoCgl0YXhBbW91bnQaBkFtb3VudED1pOPUBkjDy+PUBmoHVGF4SW5mb2InCgd0YXhhYmxlGgdCb29sZWFuQPSF6dQGSPek6dQGagdUYXhJbmZvYrkLCgh0YXhHcm91cBoIVGF4R3JvdXBA2a3m1AZItcuE1QZiHwoCaWQaA0lEIUCRvojVBkj/54jVBmoIVGF4R3JvdXBiJAoEbmFtZRoGU3RyaW5nQNT7itUGSOmWi9UGaghUYXhHcm91cGIkCgRjb2RlGgZTdHJpbmdArvmM1QZIo5GN1QZqCFRheEdyb3VwYisKC2Rlc2NyaXB0aW9uGgZTdHJpbmdApueO1QZImJWP1QZqCFRheEdyb3VwYvMJCglzYWxlUmF0ZXMaDltUYXhHcm91cFJhdGVdQKmHkdUGSJ+tkdUGYsgBEABiwwEKB3RheFJhdGUaB1RheFJhdGVAm46U1QZI2b6l1QZiHgoCaWQaA0lEIUD7yqnVBkiU9qnVBmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAkLOs1QZIjs+s1QZqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDw1a7VBkjF767VBmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQKLesNUGSLf2sNUGagdUYXhSYXRlagxUYXhHcm91cFJhdGViyAEQAWLDAQoHdGF4UmF0ZRoHVGF4UmF0ZUDa3pfVBkiT1qrVBmIeCgJpZBoDSUQhQL33rtUGSP6jr9UGagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0Du0LHVBkiH77HVBmoHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQNT8s9UGSNmZtNUGagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA9pS21QZIma+21QZqB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLIARACYsMBCgd0YXhSYXRlGgdUYXhSYXRlQN/wmtUGSNuYrNUGYh4KAmlkGgNJRCFAnKOw1QZI586w1QZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQLr7stUGSMKss9UGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAvLC11QZI8su11QZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0CrvLfVBkib1LfVBmoHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlYsgBEANiwwEKB3RheFJhdGUaB1RheFJhdGVA8Ped1QZIt56w1QZiHgoCaWQaA0lEIUDNtbTVBkjp4LTVBmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAhYu31QZI0ae31QZqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDHn7nVBkiwu7nVBmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQMWsu9UGSJDGu9UGagdUYXhSYXRlagxUYXhHcm91cFJhdGViyAEQBGLDAQoHdGF4UmF0ZRoHVGF4UmF0ZUDWkKHVBkiM3bHVBmIeCgJpZBoDSUQhQOD5tdUGSIOnttUGagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0Dh4rjVBkjg/7jVBmoHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQKGEu9UGSI6eu9UGagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdAs4q91QZInKO91QZqB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLIARAFYsMBCgd0YXhSYXRlGgdUYXhSYXRlQK+UpNUGSKz4s9UGYh4KAmlkGgNJRCFAocO31QZI2ei31QZqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQP6CutUGSKOcutUGagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVA+6S81QZI+r281QZqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0Dmq77VBkjCwb7VBmoHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlaghUYXhHcm91cGoHVGF4SW5mb2oYU2FsZXNUcmFuc2FjdGlvbkl0ZW1MaW5lagxTYWxlc1JlY2VpcHRi9AEKB3BheW1lbnQaC1BheW1lbnRJbmZvQL+f49MGSKnJlNQGYsEBCg1wYXltZW50TWV0aG9kGg1QYXltZW50TWV0aG9kQPvbmdQGSPS2sNQGYiMKAmlkGgJJRECjyrjUBkjS+rjUBmoNUGF5bWVudE1ldGhvZGIpCgRuYW1lGgZTdHJpbmdA98e81AZIqvS81AZqDVBheW1lbnRNZXRob2RiOAoEdHlwZRoVUGF5bWVudE1ldGhvZFR5cGVFbnVtQMSqw9QGSIrmw9QGag1QYXltZW50TWV0aG9kagtQYXltZW50SW5mb2oMU2FsZXNSZWNlaXB0Yr4KCghjdXN0b21lchoIQ3VzdG9tZXJAv4/D0wZIg6KW1AZiHgoCaWQaAklEQOCvm9QGSPjmm9QGaghDdXN0b21lcmIrCgtkaXNwbGF5TmFtZRoGU3RyaW5nQM3Pn9QGSNeBoNQGaghDdXN0b21lcmIpCglmaXJzdE5hbWUaBlN0cmluZ0DCuaPUBkjY6aPUBmoIQ3VzdG9tZXJiKAoIbGFzdE5hbWUaBlN0cmluZ0CziqfUBkiAtKfUBmoIQ3VzdG9tZXJiKwoLY29tcGFueU5hbWUaBlN0cmluZ0CH06rUBkjf/6rUBmoIQ3VzdG9tZXJiJQoFbm90ZXMaBlN0cmluZ0CUkq7UBki2vK7UBmoIQ3VzdG9tZXJiJwoHd2Vic2l0ZRoGU3RyaW5nQJ3EsdQGSIrusdQGaghDdXN0b21lcmIlCgVlbWFpbBoGU3RyaW5nQNaotdQGSMnTtdQGaghDdXN0b21lcmIlCgVwaG9uZRoGU3RyaW5nQI3buNQGSOOCudQGaghDdXN0b21lcmImCgZtb2JpbGUaBlN0cmluZ0D6k7zUBkjhvLzUBmoIQ3VzdG9tZXJiIwoDZmF4GgZTdHJpbmdAqdK/1AZI2/q/1AZqCEN1c3RvbWVyYtMGCg5jb250YWN0TWV0aG9kcxoRW0NvbnRhY3RNZXRob2QhXSFAr6HD1AZI/tvD1AZiigMQAGIuCgR0eXBlGgtDb250YWN0VHlwZUCGycjUBkit+cjUBmoNQ29udGFjdE1ldGhvZGItCgdwcmltYXJ5GgdCb29sZWFuQJ+0zNQGSNrkzNQGag1Db250YWN0TWV0aG9kYqYCCgdhZGRyZXNzGgdBZGRyZXNzQMWP0NQGSIDJ0NQGYi0KDnN0cmVldEFkZHJlc3MxGgZTdHJpbmdAneDU1AZI/4PV1AZqB0FkZHJlc3NiLQoOc3RyZWV0QWRkcmVzczIaBlN0cmluZ0CQ/dbUBki6ltfUBmoHQWRkcmVzc2IjCgRjaXR5GgZTdHJpbmdAvvzY1AZIu5TZ1AZqB0FkZHJlc3NiJAoFc3RhdGUaBlN0cmluZ0Dl/NrUBkiRldvUBmoHQWRkcmVzc2ImCgdjb3VudHJ5GgZTdHJpbmdA2vTc1AZI8ovd1AZqB0FkZHJlc3NiJgoHemlwQ29kZRoGU3RyaW5nQJ/v3tQGSNiG39QGagdBZGRyZXNzag1Db250YWN0TWV0aG9kYooDEAFiLgoEdHlwZRoLQ29udGFjdFR5cGVA0Y3j1AZItanj1AZqDUNvbnRhY3RNZXRob2RiLQoHcHJpbWFyeRoHQm9vbGVhbkCBi+bUBkiWpebUBmoNQ29udGFjdE1ldGhvZGKmAgoHYWRkcmVzcxoHQWRkcmVzc0DLhejUBkiZpujUBmItCg5zdHJlZXRBZGRyZXNzMRoGU3RyaW5nQOPc6tQGSJj16tQGagdBZGRyZXNzYi0KDnN0cmVldEFkZHJlc3MyGgZTdHJpbmdA0Nrs1AZI1fHs1AZqB0FkZHJlc3NiIwoEY2l0eRoGU3RyaW5nQNTI7tQGSJrf7tQGagdBZGRyZXNzYiQKBXN0YXRlGgZTdHJpbmdA4Lfw1AZIt8/w1AZqB0FkZHJlc3NiJgoHY291bnRyeRoGU3RyaW5nQKGj8tQGSKS48tQGagdBZGRyZXNzYiYKB3ppcENvZGUaBlN0cmluZ0CeivTUBki7n/TUBmoHQWRkcmVzc2oNQ29udGFjdE1ldGhvZGoIQ3VzdG9tZXJqDFNhbGVzUmVjZWlwdGJeCghtZXRhZGF0YRoITWV0YWRhdGFAk/Cq0wZIqbnc1AZiLgoNZW50aXR5VmVyc2lvbhoHU3RyaW5nIUCJm+DUBkj9xeDUBmoITWV0YWRhdGFqDFNhbGVzUmVjZWlwdGoWU2FsZXNSZWNlaXB0Q29ubmVjdGlvbmoHQ29tcGFueWoFUXVlcnk="
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
  },
  "extensions": {
    "tracing": {
      "version": 1,
      "startTime": "2021-09-08T21:22:41.244520Z",
      "endTime": "2021-09-08T21:22:45.271373Z",
      "duration": 4026781093,
      "parsing": {
        "startOffset": 1794763,
        "duration": 1473020
      },
      "validation": {
        "startOffset": 2749868,
        "duration": 875335
      },
      "execution": {
        "resolvers": [
          {
            "path": [
              "createSalesReceipt"
            ],
            "parentType": "Mutation",
            "returnType": "SalesReceipt",
            "fieldName": "createSalesReceipt",
            "startOffset": 3056209,
            "duration": 4017389392
          },
          {
            "path": [
              "createSalesReceipt",
              "id"
            ],
            "parentType": "SalesReceipt",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4020556461,
            "duration": 11629
          },
          {
            "path": [
              "createSalesReceipt",
              "transactionDate"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Date",
            "fieldName": "transactionDate",
            "startOffset": 4020798474,
            "duration": 4991
          },
          {
            "path": [
              "createSalesReceipt",
              "referenceNumber"
            ],
            "parentType": "SalesReceipt",
            "returnType": "String",
            "fieldName": "referenceNumber",
            "startOffset": 4020889802,
            "duration": 4469
          },
          {
            "path": [
              "createSalesReceipt",
              "amount"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Amount",
            "fieldName": "amount",
            "startOffset": 4020924994,
            "duration": 3310
          },
          {
            "path": [
              "createSalesReceipt",
              "voided"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Boolean",
            "fieldName": "voided",
            "startOffset": 4020958573,
            "duration": 3071
          },
          {
            "path": [
              "createSalesReceipt",
              "location"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Location",
            "fieldName": "location",
            "startOffset": 4020990414,
            "duration": 4893
          },
          {
            "path": [
              "createSalesReceipt",
              "location",
              "id"
            ],
            "parentType": "Location",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 4021048727,
            "duration": 5827
          },
          {
            "path": [
              "createSalesReceipt",
              "location",
              "name"
            ],
            "parentType": "Location",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4021085922,
            "duration": 3151
          },
          {
            "path": [
              "createSalesReceipt",
              "billingAddress"
            ],
            "parentType": "SalesReceipt",
            "returnType": "FreeFormAddress",
            "fieldName": "billingAddress",
            "startOffset": 4021471618,
            "duration": 7528
          },
          {
            "path": [
              "createSalesReceipt",
              "billingAddress",
              "freeFormAddressLine"
            ],
            "parentType": "FreeFormAddress",
            "returnType": "String",
            "fieldName": "freeFormAddressLine",
            "startOffset": 4021540794,
            "duration": 4948
          },
          {
            "path": [
              "createSalesReceipt",
              "privateMemo"
            ],
            "parentType": "SalesReceipt",
            "returnType": "String",
            "fieldName": "privateMemo",
            "startOffset": 4021638702,
            "duration": 3429
          },
          {
            "path": [
              "createSalesReceipt",
              "customerMemo"
            ],
            "parentType": "SalesReceipt",
            "returnType": "String",
            "fieldName": "customerMemo",
            "startOffset": 4021671696,
            "duration": 2891
          },
          {
            "path": [
              "createSalesReceipt",
              "account"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Account",
            "fieldName": "account",
            "startOffset": 4021138600,
            "duration": 906083
          },
          {
            "path": [
              "createSalesReceipt",
              "account",
              "id"
            ],
            "parentType": "Account",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 4022111184,
            "duration": 6473
          },
          {
            "path": [
              "createSalesReceipt",
              "account",
              "name"
            ],
            "parentType": "Account",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4022152510,
            "duration": 3672
          },
          {
            "path": [
              "createSalesReceipt",
              "currency"
            ],
            "parentType": "SalesReceipt",
            "returnType": "CurrencyInfo",
            "fieldName": "currency",
            "startOffset": 4021599621,
            "duration": 556363
          },
          {
            "path": [
              "createSalesReceipt",
              "account",
              "fullyQualifiedName"
            ],
            "parentType": "Account",
            "returnType": "String",
            "fieldName": "fullyQualifiedName",
            "startOffset": 4022185107,
            "duration": 2950
          },
          {
            "path": [
              "createSalesReceipt",
              "currency",
              "name"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4022220990,
            "duration": 6376
          },
          {
            "path": [
              "createSalesReceipt",
              "currency",
              "currency"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "String",
            "fieldName": "currency",
            "startOffset": 4022260559,
            "duration": 3483
          },
          {
            "path": [
              "createSalesReceipt",
              "currency",
              "symbol"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "String",
            "fieldName": "symbol",
            "startOffset": 4022293309,
            "duration": 3094
          },
          {
            "path": [
              "createSalesReceipt",
              "currency",
              "exchangeRate"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "Amount",
            "fieldName": "exchangeRate",
            "startOffset": 4022323679,
            "duration": 2965
          },
          {
            "path": [
              "createSalesReceipt",
              "customer"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Customer",
            "fieldName": "customer",
            "startOffset": 4021298227,
            "duration": 1209670
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "id"
            ],
            "parentType": "Customer",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 4022577481,
            "duration": 6564
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "displayName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "displayName",
            "startOffset": 4022619786,
            "duration": 3852
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "firstName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "firstName",
            "startOffset": 4022652151,
            "duration": 3087
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "lastName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "lastName",
            "startOffset": 4022681701,
            "duration": 2922
          },
          {
            "path": [
              "createSalesReceipt",
              "emailDeliveryInfo"
            ],
            "parentType": "SalesReceipt",
            "returnType": "EmailDeliveryInfo",
            "fieldName": "emailDeliveryInfo",
            "startOffset": 4021898648,
            "duration": 791493
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "companyName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "companyName",
            "startOffset": 4022711256,
            "duration": 2966
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "notes"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "notes",
            "startOffset": 4022740726,
            "duration": 2936
          },
          {
            "path": [
              "createSalesReceipt",
              "emailDeliveryInfo",
              "to"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "[String!]",
            "fieldName": "to",
            "startOffset": 4022757884,
            "duration": 5998
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "website"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "website",
            "startOffset": 4022771039,
            "duration": 2953
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "email"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "email",
            "startOffset": 4022800495,
            "duration": 2870
          },
          {
            "path": [
              "createSalesReceipt",
              "emailDeliveryInfo",
              "cc"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "[String!]",
            "fieldName": "cc",
            "startOffset": 4022812953,
            "duration": 4065
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "phone"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "phone",
            "startOffset": 4022829393,
            "duration": 2791
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "mobile"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "mobile",
            "startOffset": 4022859105,
            "duration": 2732
          },
          {
            "path": [
              "createSalesReceipt",
              "emailDeliveryInfo",
              "bcc"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "[String!]",
            "fieldName": "bcc",
            "startOffset": 4022858967,
            "duration": 3598
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "fax"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "fax",
            "startOffset": 4022888682,
            "duration": 2737
          },
          {
            "path": [
              "createSalesReceipt",
              "emailDeliveryInfo",
              "status"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "EmailStatus",
            "fieldName": "status",
            "startOffset": 4022902936,
            "duration": 3500
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods"
            ],
            "parentType": "Customer",
            "returnType": "[ContactMethod!]!",
            "fieldName": "contactMethods",
            "startOffset": 4022919599,
            "duration": 4662
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "type"
            ],
            "parentType": "ContactMethod",
            "returnType": "ContactType",
            "fieldName": "type",
            "startOffset": 4022972096,
            "duration": 3408
          },
          {
            "path": [
              "createSalesReceipt",
              "tax"
            ],
            "parentType": "SalesReceipt",
            "returnType": "TransactionTaxInfo",
            "fieldName": "tax",
            "startOffset": 4022995018,
            "duration": 5259
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "primary"
            ],
            "parentType": "ContactMethod",
            "returnType": "Boolean",
            "fieldName": "primary",
            "startOffset": 4023013049,
            "duration": 3265
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines"
            ],
            "parentType": "SalesReceipt",
            "returnType": "[SalesTransactionItemLine]",
            "fieldName": "itemLines",
            "startOffset": 4021703030,
            "duration": 1314067
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address"
            ],
            "parentType": "ContactMethod",
            "returnType": "Address",
            "fieldName": "address",
            "startOffset": 4023046715,
            "duration": 4088
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "totalTaxAmount"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "Amount",
            "fieldName": "totalTaxAmount",
            "startOffset": 4023047685,
            "duration": 3558
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "sequence"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "String",
            "fieldName": "sequence",
            "startOffset": 4023087031,
            "duration": 6237
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "streetAddress1"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress1",
            "startOffset": 4023099464,
            "duration": 3509
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxable"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "Boolean",
            "fieldName": "taxable",
            "startOffset": 4023129280,
            "duration": 3182
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "description"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4023129529,
            "duration": 3631
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "streetAddress2"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress2",
            "startOffset": 4023133843,
            "duration": 3105
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "amount"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Amount",
            "fieldName": "amount",
            "startOffset": 4023165370,
            "duration": 3227
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "city"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "city",
            "startOffset": 4023166320,
            "duration": 3122
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "state"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "state",
            "startOffset": 4023199255,
            "duration": 3210
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "unitPrice"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Amount",
            "fieldName": "unitPrice",
            "startOffset": 4023200157,
            "duration": 2998
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "country"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "country",
            "startOffset": 4023231358,
            "duration": 2868
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "zipCode"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "zipCode",
            "startOffset": 4023264398,
            "duration": 3030
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "type"
            ],
            "parentType": "ContactMethod",
            "returnType": "ContactType",
            "fieldName": "type",
            "startOffset": 4023327768,
            "duration": 3624
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "primary"
            ],
            "parentType": "ContactMethod",
            "returnType": "Boolean",
            "fieldName": "primary",
            "startOffset": 4023366635,
            "duration": 4637
          },
          {
            "path": [
              "createSalesReceipt",
              "metadata"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Metadata",
            "fieldName": "metadata",
            "startOffset": 4020607603,
            "duration": 2784233
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address"
            ],
            "parentType": "ContactMethod",
            "returnType": "Address",
            "fieldName": "address",
            "startOffset": 4023412095,
            "duration": 4804
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "streetAddress1"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress1",
            "startOffset": 4023457807,
            "duration": 3083
          },
          {
            "path": [
              "createSalesReceipt",
              "shipping"
            ],
            "parentType": "SalesReceipt",
            "returnType": "ShippingDetails",
            "fieldName": "shipping",
            "startOffset": 4022954268,
            "duration": 528781
          },
          {
            "path": [
              "createSalesReceipt",
              "metadata",
              "entityVersion"
            ],
            "parentType": "Metadata",
            "returnType": "String!",
            "fieldName": "entityVersion",
            "startOffset": 4023476528,
            "duration": 7256
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "streetAddress2"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress2",
            "startOffset": 4023489367,
            "duration": 2907
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "city"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "city",
            "startOffset": 4023520270,
            "duration": 2898
          },
          {
            "path": [
              "createSalesReceipt",
              "shipping",
              "shipDate"
            ],
            "parentType": "ShippingDetails",
            "returnType": "Date",
            "fieldName": "shipDate",
            "startOffset": 4023541695,
            "duration": 5913
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "state"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "state",
            "startOffset": 4023550508,
            "duration": 3016
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "TaxGroup",
            "fieldName": "taxGroup",
            "startOffset": 4023092287,
            "duration": 472810
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "country"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "country",
            "startOffset": 4023581230,
            "duration": 2727
          },
          {
            "path": [
              "createSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "zipCode"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "zipCode",
            "startOffset": 4023611448,
            "duration": 2794
          },
          {
            "path": [
              "createSalesReceipt",
              "shipping",
              "shipVia"
            ],
            "parentType": "ShippingDetails",
            "returnType": "String",
            "fieldName": "shipVia",
            "startOffset": 4023624593,
            "duration": 4682
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "id"
            ],
            "parentType": "TaxGroup",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4023623978,
            "duration": 5804
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "class"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Class",
            "fieldName": "class",
            "startOffset": 4023238703,
            "duration": 407128
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "name"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4023665107,
            "duration": 3609
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "[TaxDetails]",
            "fieldName": "taxDetails",
            "startOffset": 4023163007,
            "duration": 514189
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "code"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "code",
            "startOffset": 4023697937,
            "duration": 3087
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "class",
              "id"
            ],
            "parentType": "Class",
            "returnType": "String",
            "fieldName": "id",
            "startOffset": 4023703505,
            "duration": 5217
          },
          {
            "path": [
              "createSalesReceipt",
              "payment"
            ],
            "parentType": "SalesReceipt",
            "returnType": "PaymentInfo",
            "fieldName": "payment",
            "startOffset": 4023207763,
            "duration": 507631
          },
          {
            "path": [
              "createSalesReceipt",
              "shipping",
              "trackingNumber"
            ],
            "parentType": "ShippingDetails",
            "returnType": "String",
            "fieldName": "trackingNumber",
            "startOffset": 4023725477,
            "duration": 3443
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "description"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4023729393,
            "duration": 2985
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "class",
              "name"
            ],
            "parentType": "Class",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4023741465,
            "duration": 2974
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 4023747748,
            "duration": 6851
          },
          {
            "path": [
              "createSalesReceipt",
              "shipping",
              "shippingAmount"
            ],
            "parentType": "ShippingDetails",
            "returnType": "Amount",
            "fieldName": "shippingAmount",
            "startOffset": 4023759182,
            "duration": 2838
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates"
            ],
            "parentType": "TaxGroup",
            "returnType": "[TaxGroupRate]",
            "fieldName": "saleRates",
            "startOffset": 4023761496,
            "duration": 5094
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 4023798761,
            "duration": 5927
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "quantity"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Int",
            "fieldName": "quantity",
            "startOffset": 4023831660,
            "duration": 3239
          },
          {
            "path": [
              "createSalesReceipt",
              "shipping",
              "shipAddress"
            ],
            "parentType": "ShippingDetails",
            "returnType": "FreeFormAddress",
            "fieldName": "shipAddress",
            "startOffset": 4023657812,
            "duration": 253669
          },
          {
            "path": [
              "createSalesReceipt",
              "shipping",
              "shipFromAddress"
            ],
            "parentType": "ShippingDetails",
            "returnType": "FreeFormAddress",
            "fieldName": "shipFromAddress",
            "startOffset": 4023693237,
            "duration": 239125
          },
          {
            "path": [
              "createSalesReceipt",
              "shipping",
              "shipAddress",
              "freeFormAddressLine"
            ],
            "parentType": "FreeFormAddress",
            "returnType": "String",
            "fieldName": "freeFormAddressLine",
            "startOffset": 4023967376,
            "duration": 9944
          },
          {
            "path": [
              "createSalesReceipt",
              "shipping",
              "shipFromAddress",
              "freeFormAddressLine"
            ],
            "parentType": "FreeFormAddress",
            "returnType": "String",
            "fieldName": "freeFormAddressLine",
            "startOffset": 4023998175,
            "duration": 6503
          },
          {
            "path": [
              "createSalesReceipt",
              "payment",
              "paymentMethod"
            ],
            "parentType": "PaymentInfo",
            "returnType": "PaymentMethod",
            "fieldName": "paymentMethod",
            "startOffset": 4023772829,
            "duration": 284228
          },
          {
            "path": [
              "createSalesReceipt",
              "payment",
              "paymentMethod",
              "id"
            ],
            "parentType": "PaymentMethod",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 4024114562,
            "duration": 5915
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4023813189,
            "duration": 309355
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "item"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Item",
            "fieldName": "item",
            "startOffset": 4023791118,
            "duration": 337262
          },
          {
            "path": [
              "createSalesReceipt",
              "payment",
              "paymentMethod",
              "name"
            ],
            "parentType": "PaymentMethod",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4024159823,
            "duration": 3692
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4024186909,
            "duration": 5813
          },
          {
            "path": [
              "createSalesReceipt",
              "payment",
              "paymentMethod",
              "type"
            ],
            "parentType": "PaymentMethod",
            "returnType": "PaymentMethodTypeEnum",
            "fieldName": "type",
            "startOffset": 4024193230,
            "duration": 3117
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "item",
              "id"
            ],
            "parentType": "InventoryItem",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 4024219091,
            "duration": 5775
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4024236210,
            "duration": 4272
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "item",
              "name"
            ],
            "parentType": "InventoryItem",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4024261383,
            "duration": 3463
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4023859180,
            "duration": 409816
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4024273628,
            "duration": 3212
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "item",
              "sku"
            ],
            "parentType": "InventoryItem",
            "returnType": "String",
            "fieldName": "sku",
            "startOffset": 4024294752,
            "duration": 3147
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4024307340,
            "duration": 3058
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4024328132,
            "duration": 4966
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4024340406,
            "duration": 2974
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4023873712,
            "duration": 490587
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4024366921,
            "duration": 3108
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4024372912,
            "duration": 3057
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4024400950,
            "duration": 2936
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4024432888,
            "duration": 2972
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4024436457,
            "duration": 5686
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4024442211,
            "duration": 3803
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4024463681,
            "duration": 2867
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4024479262,
            "duration": 3627
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4024495623,
            "duration": 3033
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4024513618,
            "duration": 3161
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4024545874,
            "duration": 2893
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4024560182,
            "duration": 3442
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4024577123,
            "duration": 2854
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4024608906,
            "duration": 2789
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 4024625693,
            "duration": 3649
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 4024661924,
            "duration": 3033
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4024674649,
            "duration": 3576
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "TaxInfo",
            "fieldName": "tax",
            "startOffset": 4023872983,
            "duration": 838648
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 4024751975,
            "duration": 3348
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxAmount"
            ],
            "parentType": "TaxInfo",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 4024774652,
            "duration": 5126
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 4024788221,
            "duration": 3046
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxable"
            ],
            "parentType": "TaxInfo",
            "returnType": "Boolean",
            "fieldName": "taxable",
            "startOffset": 4024865908,
            "duration": 5941
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 4024884070,
            "duration": 5534
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 4024938354,
            "duration": 4938
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4024695095,
            "duration": 281275
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4024743465,
            "duration": 258542
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025043121,
            "duration": 6528
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4024800510,
            "duration": 260905
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 4025058120,
            "duration": 10116
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025086871,
            "duration": 3675
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4024821078,
            "duration": 276963
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025101004,
            "duration": 21501
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025121629,
            "duration": 3532
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025126000,
            "duration": 6330
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 4025127498,
            "duration": 5891
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4024850528,
            "duration": 300473
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025155743,
            "duration": 3788
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4024900572,
            "duration": 270994
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025170231,
            "duration": 3795
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025178103,
            "duration": 7248
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025182072,
            "duration": 4603
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4025190056,
            "duration": 3051
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025207130,
            "duration": 3415
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4024979995,
            "duration": 235461
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025223345,
            "duration": 3664
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025227233,
            "duration": 7795
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025232590,
            "duration": 5482
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4025235173,
            "duration": 5927
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025241784,
            "duration": 3510
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025244356,
            "duration": 6453
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025259241,
            "duration": 3599
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025274373,
            "duration": 3811
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4025275701,
            "duration": 3161
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025276187,
            "duration": 3219
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025277359,
            "duration": 6044
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 4025277995,
            "duration": 6179
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4025293651,
            "duration": 3151
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup"
            ],
            "parentType": "TaxInfo",
            "returnType": "TaxGroup",
            "fieldName": "taxGroup",
            "startOffset": 4024816584,
            "duration": 487738
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025304218,
            "duration": 5615
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4025310287,
            "duration": 3103
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025311014,
            "duration": 3450
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025319142,
            "duration": 3396
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025323849,
            "duration": 4518
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4025327867,
            "duration": 3138
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4025339322,
            "duration": 6962
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025345798,
            "duration": 3064
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 4025342983,
            "duration": 5911
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025353037,
            "duration": 3414
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025365141,
            "duration": 5581
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "id"
            ],
            "parentType": "TaxGroup",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025365250,
            "duration": 5959
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025373635,
            "duration": 3897
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4025378610,
            "duration": 2913
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4025378281,
            "duration": 3699
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4025396646,
            "duration": 3772
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025408516,
            "duration": 3735
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4025411656,
            "duration": 3198
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4025412066,
            "duration": 2788
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "name"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025415327,
            "duration": 3768
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4025428909,
            "duration": 5622
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4025442586,
            "duration": 2996
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4025445071,
            "duration": 3148
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "code"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "code",
            "startOffset": 4025450157,
            "duration": 3271
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4025184215,
            "duration": 292500
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4025474836,
            "duration": 2920
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "description"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025482169,
            "duration": 3019
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4025480779,
            "duration": 4409
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4025506163,
            "duration": 5940
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates"
            ],
            "parentType": "TaxGroup",
            "returnType": "[TaxGroupRate]",
            "fieldName": "saleRates",
            "startOffset": 4025515174,
            "duration": 4758
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4025540879,
            "duration": 3641
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4025546633,
            "duration": 5104
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025570668,
            "duration": 4528
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4025581604,
            "duration": 4469
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025610165,
            "duration": 2970
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4025403680,
            "duration": 211910
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025641675,
            "duration": 2956
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025673715,
            "duration": 2774
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025671896,
            "duration": 5265
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4025704893,
            "duration": 2668
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025711972,
            "duration": 3085
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4025736108,
            "duration": 2780
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025744503,
            "duration": 3125
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025775562,
            "duration": 3007
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4025796332,
            "duration": 3464
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 4025806999,
            "duration": 2818
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4025565554,
            "duration": 246442
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 4025838403,
            "duration": 2875
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4025868217,
            "duration": 4492
          },
          {
            "path": [
              "createSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 4025902201,
            "duration": 3420
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4025914986,
            "duration": 3345
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4025948663,
            "duration": 3059
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4025980532,
            "duration": 2859
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4026040295,
            "duration": 225215
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4026324044,
            "duration": 5320
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4026375281,
            "duration": 3517
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4026095984,
            "duration": 310309
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4026410319,
            "duration": 3188
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4026145540,
            "duration": 280669
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4026443795,
            "duration": 3302
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4026462008,
            "duration": 5129
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4026201155,
            "duration": 285278
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 4026250182,
            "duration": 245807
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4026495024,
            "duration": 6402
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4026501058,
            "duration": 3107
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4026535953,
            "duration": 3014
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4026540504,
            "duration": 7056
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4026555103,
            "duration": 6838
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 4026563062,
            "duration": 6692
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4026568852,
            "duration": 3034
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4026580129,
            "duration": 3361
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4026606617,
            "duration": 4216
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 4026608263,
            "duration": 3967
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4026613587,
            "duration": 3259
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4026644143,
            "duration": 3573
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 4026645663,
            "duration": 3261
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4026679407,
            "duration": 3144
          },
          {
            "path": [
              "createSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 4026680009,
            "duration": 3051
          }
        ]
      }
    },
    "ftv1": "GgwIpdPkiQYQgLS2gQEiCwih0+SJBhDgx8x0WLPYkYAPcsNTYsBTChJjcmVhdGVTYWxlc1JlY2VpcHQaDFNhbGVzUmVjZWlwdECdq7oBSJfIjP0OYiMKAmlkGgNJRCFA6Y2T/Q5I4/CT/Q5qDFNhbGVzUmVjZWlwdGIxCg90cmFuc2FjdGlvbkRhdGUaBERhdGVAp+2h/Q5I/5yi/Q5qDFNhbGVzUmVjZWlwdGIzCg9yZWZlcmVuY2VOdW1iZXIaBlN0cmluZ0Dntqf9Dkim4af9DmoMU2FsZXNSZWNlaXB0YioKBmFtb3VudBoGQW1vdW50QPrIqf0OSN3mqf0OagxTYWxlc1JlY2VpcHRiKwoGdm9pZGVkGgdCb29sZWFuQIrPq/0OSMfsq/0OagxTYWxlc1JlY2VpcHRidAoIbG9jYXRpb24aCExvY2F0aW9uQNDHrf0OSIfyrf0OYh4KAmlkGgJJREDBkLH9DkiCw7H9DmoITG9jYXRpb25iJAoEbmFtZRoGU3RyaW5nQN2ys/0OSLzPs/0OaghMb2NhdGlvbmoMU2FsZXNSZWNlaXB0YncKDmJpbGxpbmdBZGRyZXNzGg9GcmVlRm9ybUFkZHJlc3NAivrK/Q5I6cHL/Q5iOgoTZnJlZUZvcm1BZGRyZXNzTGluZRoGU3RyaW5nQNWVz/0OSOfCz/0Oag9GcmVlRm9ybUFkZHJlc3NqDFNhbGVzUmVjZWlwdGIvCgtwcml2YXRlTWVtbxoGU3RyaW5nQNyQ1f0OSOmy1f0OagxTYWxlc1JlY2VpcHRiMAoMY3VzdG9tZXJNZW1vGgZTdHJpbmdA+5HX/Q5I7a3X/Q5qDFNhbGVzUmVjZWlwdGKjAQoHYWNjb3VudBoHQWNjb3VudECWzbb9DkiijO79DmIdCgJpZBoCSURA2v3x/Q5I3LXy/Q5qB0FjY291bnRiIwoEbmFtZRoGU3RyaW5nQKa/9P0OSMfh9P0OagdBY2NvdW50YjEKEmZ1bGx5UXVhbGlmaWVkTmFtZRoGU3RyaW5nQLK99v0OSOnZ9v0OagdBY2NvdW50agxTYWxlc1JlY2VpcHRi6AEKCGN1cnJlbmN5GgxDdXJyZW5jeUluZm9Aq+HS/Q5Ix+n0/Q5iKAoEbmFtZRoGU3RyaW5nQJ7Y+P0OSI2P+f0OagxDdXJyZW5jeUluZm9iLAoIY3VycmVuY3kaBlN0cmluZ0Cmi/v9DkjrrPv9DmoMQ3VycmVuY3lJbmZvYioKBnN5bWJvbBoGU3RyaW5nQKSL/f0OSLWn/f0OagxDdXJyZW5jeUluZm9iMAoMZXhjaGFuZ2VSYXRlGgZBbW91bnRA2Pf+/Q5IzJP//Q5qDEN1cnJlbmN5SW5mb2oMU2FsZXNSZWNlaXB0Yr4KCghjdXN0b21lchoIQ3VzdG9tZXJAhLDA/Q5IjKaK/g5iHgoCaWQaAklEQMe4jv4OSO3yjv4OaghDdXN0b21lcmIrCgtkaXNwbGF5TmFtZRoGU3RyaW5nQN2Bkf4OSLWlkf4OaghDdXN0b21lcmIpCglmaXJzdE5hbWUaBlN0cmluZ0Dl/ZL+DkiTm5P+DmoIQ3VzdG9tZXJiKAoIbGFzdE5hbWUaBlN0cmluZ0CJ5ZT+DkiGgJX+DmoIQ3VzdG9tZXJiKwoLY29tcGFueU5hbWUaBlN0cmluZ0DNy5b+Dkjd6Jb+DmoIQ3VzdG9tZXJiJQoFbm90ZXMaBlN0cmluZ0DhsZj+DkjAzZj+DmoIQ3VzdG9tZXJiJwoHd2Vic2l0ZRoGU3RyaW5nQPKfmv4OSOC6mv4OaghDdXN0b21lcmIlCgVlbWFpbBoGU3RyaW5nQPeEnP4OSOCfnP4OaghDdXN0b21lcmIlCgVwaG9uZRoGU3RyaW5nQN7mnf4OSNGBnv4OaghDdXN0b21lcmImCgZtb2JpbGUaBlN0cmluZ0D2zp/+Dkjz6J/+DmoIQ3VzdG9tZXJiIwoDZmF4GgZTdHJpbmdA/rWh/g5I+dCh/g5qCEN1c3RvbWVyYtMGCg5jb250YWN0TWV0aG9kcxoRW0NvbnRhY3RNZXRob2QhXSFAhKij/g5Ih9ij/g5iigMQAGIuCgR0eXBlGgtDb250YWN0VHlwZUCTwqb+Dkj1+ab+DmoNQ29udGFjdE1ldGhvZGItCgdwcmltYXJ5GgdCb29sZWFuQN2Bqf4OSJyiqf4Oag1Db250YWN0TWV0aG9kYqYCCgdhZGRyZXNzGgdBZGRyZXNzQJ6Iq/4OSOetq/4OYi0KDnN0cmVldEFkZHJlc3MxGgZTdHJpbmdAmaWu/g5Ipsiu/g5qB0FkZHJlc3NiLQoOc3RyZWV0QWRkcmVzczIaBlN0cmluZ0DSsbD+DkiWz7D+DmoHQWRkcmVzc2IjCgRjaXR5GgZTdHJpbmdA4K+y/g5I08yy/g5qB0FkZHJlc3NiJAoFc3RhdGUaBlN0cmluZ0CisLT+Dkinz7T+DmoHQWRkcmVzc2ImCgdjb3VudHJ5GgZTdHJpbmdA46q2/g5I18a2/g5qB0FkZHJlc3NiJgoHemlwQ29kZRoGU3RyaW5nQNOtuP4OSPLJuP4OagdBZGRyZXNzag1Db250YWN0TWV0aG9kYooDEAFiLgoEdHlwZRoLQ29udGFjdFR5cGVAi528/g5I3r+8/g5qDUNvbnRhY3RNZXRob2RiLQoHcHJpbWFyeRoHQm9vbGVhbkD0zr7+DkjW+b7+DmoNQ29udGFjdE1ldGhvZGKmAgoHYWRkcmVzcxoHQWRkcmVzc0DBr8H+DkiX28H+DmItCg5zdHJlZXRBZGRyZXNzMRoGU3RyaW5nQLeUxP4OSKmyxP4OagdBZGRyZXNzYi0KDnN0cmVldEFkZHJlc3MyGgZTdHJpbmdAnIvG/g5IjqfG/g5qB0FkZHJlc3NiIwoEY2l0eRoGU3RyaW5nQK78x/4OSKuYyP4OagdBZGRyZXNzYiQKBXN0YXRlGgZTdHJpbmdAtejJ/g5ItYbK/g5qB0FkZHJlc3NiJgoHY291bnRyeRoGU3RyaW5nQNLYy/4OSLzzy/4OagdBZGRyZXNzYiYKB3ppcENvZGUaBlN0cmluZ0COxM3+DkjU3s3+DmoHQWRkcmVzc2oNQ29udGFjdE1ldGhvZGoIQ3VzdG9tZXJqDFNhbGVzUmVjZWlwdGKHAgoRZW1haWxEZWxpdmVyeUluZm8aEUVtYWlsRGVsaXZlcnlJbmZvQISC5f0OSN64lf4OYi4KAnRvGglbU3RyaW5nIV1AiLuZ/g5IjfaZ/g5qEUVtYWlsRGVsaXZlcnlJbmZvYi4KAmNjGglbU3RyaW5nIV1A4Oec/g5Is5Cd/g5qEUVtYWlsRGVsaXZlcnlJbmZvYi8KA2JjYxoJW1N0cmluZyFdQPbOn/4OSJnyn/4OahFFbWFpbERlbGl2ZXJ5SW5mb2I0CgZzdGF0dXMaC0VtYWlsU3RhdHVzQMqlov4OSLXHov4OahFFbWFpbERlbGl2ZXJ5SW5mb2oMU2FsZXNSZWNlaXB0YscmCgN0YXgaElRyYW5zYWN0aW9uVGF4SW5mb0Ds9Kf+DkjCpqj+DmI4Cg50b3RhbFRheEFtb3VudBoGQW1vdW50QKSRq/4OSLKzq/4OahJUcmFuc2FjdGlvblRheEluZm9iMgoHdGF4YWJsZRoHQm9vbGVhbkDXjbD+DkjWrrD+DmoSVHJhbnNhY3Rpb25UYXhJbmZvYqARCgh0YXhHcm91cBoIVGF4R3JvdXBApO2t/g5IyujK/g5iHwoCaWQaA0lEIUCIqM7+DkiP3c7+DmoIVGF4R3JvdXBiJAoEbmFtZRoGU3RyaW5nQMfo0P4OSP+J0f4OaghUYXhHcm91cGIkCgRjb2RlGgZTdHJpbmdA5ejS/g5Is4bT/g5qCFRheEdyb3VwYisKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA597U/g5I6frU/g5qCFRheEdyb3VwYs8PCglzYWxlUmF0ZXMaDltUYXhHcm91cFJhdGVdQL3a1v4OSLeI1/4OYsICEABivQIKB3RheFJhdGUaB1RheFJhdGVAze3Z/g5Iw/Ds/g5iHgoCaWQaA0lEIUDM1vD+DkjNjfH+DmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA6dfz/g5IiYD0/g5qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUCq+vX+Dkiamfb+DmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQNSB+P4OSJag+P4OagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQImE+v4OSLSg+v4OagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUCDgvz+DkjsoPz+DmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA6p+A/w5IlMWA/w5qB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLCAhABYr0CCgd0YXhSYXRlGgdUYXhSYXRlQJrG3f4OSLTO+/4OYh4KAmlkGgNJRCFAk/X//g5IgquA/w5qB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQKbBgv8OSKDkgv8OagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAqs2E/w5IveuE/w5qB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0DKyIb/Dki45Ib/DmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0DRvYj/DkiK2Yj/DmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVA+rSK/w5IwdCK/w5qB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQLy3jv8OSOvZjv8OagdUYXhSYXRlagxUYXhHcm91cFJhdGViwgIQAmK9AgoHdGF4UmF0ZRoHVGF4UmF0ZUDe0JL/Dkj7xaL/DmIeCgJpZBoDSUQhQKmUqf8OSLr4qf8OagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0DMta3/Dkjk363/DmoHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQOD2r/8OSNyZsP8OagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA54+y/w5IkrCy/w5qB1RheFJhdGViKwoGc3RhdHVzGgxBY3RpdmVTdGF0dXNA45q0/w5Itrm0/w5qB1RheFJhdGViJgoJc3RhcnREYXRlGgREYXRlQKKntv8OSLDGtv8OagdUYXhSYXRlYiMKBHJhdGUaBlN0cmluZ0Dzv7r/Dkin5br/DmoHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlYsICEANivQIKB3RheFJhdGUaB1RheFJhdGVA0Y6W/w5IvJKm/w5iHgoCaWQaA0lEIUDp/6n/Dkinuqr/DmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA4tes/w5IlPys/w5qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUCz967/DkigmK//DmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQJiHsf8OSISnsf8OagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQJaPs/8OSOuts/8OagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUCmnrX/DkiTu7X/DmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA/7C5/w5I09S5/w5qB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLCAhAEYr0CCgd0YXhSYXRlGgdUYXhSYXRlQMKVmf8OSPXRq/8OYh4KAmlkGgNJRCFA4piw/w5Ild+w/w5qB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQOeFs/8OSPeqs/8OagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAxom2/w5In7K2/w5qB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0C3jLn/DkjMsrn/DmoHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0Cktbv/Dkiv1bv/DmoHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVArrq9/w5I2ti9/w5qB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQKPUw/8OSImHxP8OagdUYXhSYXRlagxUYXhHcm91cFJhdGViwgIQBWK9AgoHdGF4UmF0ZRoHVGF4UmF0ZUC7nJz/Dkii76z/DmIeCgJpZBoDSUQhQILAsP8OSMfzsP8OagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0DwkrP/DkjusrP/DmoHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQNSjtf8OSJzDtf8OagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA67K3/w5IvdC3/w5qB1RheFJhdGViKwoGc3RhdHVzGgxBY3RpdmVTdGF0dXNAzLK5/w5Ix8+5/w5qB1RheFJhdGViJgoJc3RhcnREYXRlGgREYXRlQIS4u/8OSPnWu/8OagdUYXhSYXRlYiMKBHJhdGUaBlN0cmluZ0CI07//DkjA+7//DmoHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlaghUYXhHcm91cGoSVHJhbnNhY3Rpb25UYXhJbmZvYoAUCgp0YXhEZXRhaWxzGgxbVGF4RGV0YWlsc11A7pSy/g5I6NnR/g5ingMQAGIrCgl0YXhBbW91bnQaBkFtb3VudECB8NX+DkiMrNb+DmoKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAu//Y/g5IoLbZ/g5qClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVAttXc/g5I1+D1/g5iHgoCaWQaA0lEIUCDpvn+Dkjt0/n+DmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAl9P7/g5IvfH7/g5qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUC/3P3+Dkjb+v3+DmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQOjV//4OSOvy//4OagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQKLGgf8OSIbjgf8OagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUDrwIP/Dkjr3IP/DmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA6biH/w5I69qH/w5qB1RheFJhdGVqClRheERldGFpbHNingMQAWIrCgl0YXhBbW91bnQaBkFtb3VudECMuYv/Dkiy24v/DmoKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAwdON/w5IwvCN/w5qClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVA5daP/w5Iwfug/w5iHgoCaWQaA0lEIUCS+KT/Dkixs6X/DmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAyMun/w5IgfCn/w5qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDk3Kn/Dkj9/Kn/DmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQLLmq/8OSNuLrP8OagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQMLxrf8OSJuPrv8OagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUD51bD/DkiajrH/DmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdAnIO3/w5Ip8a3/w5qB1RheFJhdGVqClRheERldGFpbHNingMQAmIrCgl0YXhBbW91bnQaBkFtb3VudECdk5P/Dki6tJP/DmoKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRA+a6V/w5IhcuV/w5qClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVApK+X/w5IrrOo/w5iHgoCaWQaA0lEIUCpl63/Dkir3a3/DmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAvpux/w5I89mx/w5qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDX77T/Dkimp7X/DmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQJDMuP8OSNiCuf8OagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQNO+vP8OSK71vP8OagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUD3mMH/DkiO0MH/DmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdAy+XF/w5I34/G/w5qB1RheFJhdGVqClRheERldGFpbHNingMQA2IrCgl0YXhBbW91bnQaBkFtb3VudEDenZv/DkiX0pv/DmoKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAx8We/w5IwPSe/w5qClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVA6Yih/w5IysWv/w5iHgoCaWQaA0lEIUDxnbP/Dkii1LP/DmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA1OK1/w5Il4S2/w5qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUCr67f/DkiKjbj/DmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQNmcu/8OSIfBu/8OagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQKGnvf8OSLjEvf8OagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUCtor//DkinwL//DmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA5KbD/w5IrMvD/w5qB1RheFJhdGVqClRheERldGFpbHNingMQBGIrCgl0YXhBbW91bnQaBkFtb3VudEDc7aX/Dkigx6b/DmoKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAhI2q/w5I6sOq/w5qClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVAuMat/w5IkL2//w5iHgoCaWQaA0lEIUD7kMX/DkjrvMX/DmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdArsTH/w5IueDH/w5qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUD/ucn/DkjY1sn/DmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQLq0y/8OSI/Py/8OagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQK+nzf8OSNrBzf8OagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUC/m8//Dkjets//DmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdAm/LS/w5IuZPT/w5qB1RheFJhdGVqClRheERldGFpbHNingMQBWIrCgl0YXhBbW91bnQaBkFtb3VudEDyo7P/DkjE3rP/DmoKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAoJ+3/w5Isti3/w5qClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVAmPq6/w5I1/vH/w5iHgoCaWQaA0lEIUCwqMv/DkjG2Mv/DmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA0d/N/w5I+fzN/w5qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUCx3s//Dkjr+s//DmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQLjP0f8OSKTt0f8OagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQLzF0/8OSJjh0/8OagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUD4utX/Dkib19X/DmoHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA2q3Z/w5I58/Z/w5qB1RheFJhdGVqClRheERldGFpbHNqElRyYW5zYWN0aW9uVGF4SW5mb2oMU2FsZXNSZWNlaXB0YtYRCglpdGVtTGluZXMaGltTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmVdQIaH2f0OSIi0qf4OYpIREABiOAoIc2VxdWVuY2UaBlN0cmluZ0Dxxa3+DkiR/q3+DmoYU2FsZXNUcmFuc2FjdGlvbkl0ZW1MaW5lYjsKC2Rlc2NyaXB0aW9uGgZTdHJpbmdAtpCw/g5I/rOw/g5qGFNhbGVzVHJhbnNhY3Rpb25JdGVtTGluZWI2CgZhbW91bnQaBkFtb3VudEDNp7L+Dkiyx7L+DmoYU2FsZXNUcmFuc2FjdGlvbkl0ZW1MaW5lYjkKCXVuaXRQcmljZRoGQW1vdW50QJq4tP4OSNTUtP4OahhTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmVieAoFY2xhc3MaBUNsYXNzQOjltv4OSIrez/4OYh8KAmlkGgZTdHJpbmdAhpbT/g5Ip8TT/g5qBUNsYXNzYiEKBG5hbWUaBlN0cmluZ0CvvNX+DkiS2tX+DmoFQ2xhc3NqGFNhbGVzVHJhbnNhY3Rpb25JdGVtTGluZWI1CghxdWFudGl0eRoDSW50QMP92v4OSN6e2/4OahhTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmVirAEKBGl0ZW0aBEl0ZW1A88DY/g5Iq5nt/g5iIwoCaWQaAklEQPvR8v4OSJGG8/4Oag1JbnZlbnRvcnlJdGVtYikKBG5hbWUaBlN0cmluZ0CBm/X+DkjQuvX+DmoNSW52ZW50b3J5SXRlbWIoCgNza3UaBlN0cmluZ0C1n/f+Dkijvff+DmoNSW52ZW50b3J5SXRlbWoYU2FsZXNUcmFuc2FjdGlvbkl0ZW1MaW5lYsMMCgN0YXgaB1RheEluZm9A4r/d/g5ItuaQ/w5iKAoJdGF4QW1vdW50GgZBbW91bnRAi8aU/w5IgfSU/w5qB1RheEluZm9iJwoHdGF4YWJsZRoHQm9vbGVhbkDQkJr/DkikyZr/DmoHVGF4SW5mb2K5CwoIdGF4R3JvdXAaCFRheEdyb3VwQMCMl/8OSM/7tP8OYh8KAmlkGgNJRCFAjc64/w5IkIS5/w5qCFRheEdyb3VwYiQKBG5hbWUaBlN0cmluZ0CJ07v/DkiT97v/DmoIVGF4R3JvdXBiJAoEY29kZRoGU3RyaW5nQKnjvf8OSKaBvv8OaghUYXhHcm91cGIrCgtkZXNjcmlwdGlvbhoGU3RyaW5nQMXcv/8OSPb4v/8OaghUYXhHcm91cGLzCQoJc2FsZVJhdGVzGg5bVGF4R3JvdXBSYXRlXUDS3cH/DkjYisL/DmLIARAAYsMBCgd0YXhSYXRlGgdUYXhSYXRlQNvnxP8OSPr40/8OYh4KAmlkGgNJRCFAgaXX/w5ItNDX/w5qB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQJuR2v8OSKiy2v8OagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAqJjc/w5I27Xc/w5qB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0D9kN7/DkjFrN7/DmoHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlYsgBEAFiwwEKB3RheFJhdGUaB1RheFJhdGVA8OPh/w5I09Dv/w5iHgoCaWQaA0lEIUD+jfP/DkiQwPP/DmoHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAsJ32/w5InL/2/w5qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUCsr/j/DkjBzvj/DmoHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQJC1+v8OSJzU+v8OagdUYXhSYXRlagxUYXhHcm91cFJhdGViyAEQAmLDAQoHdGF4UmF0ZRoHVGF4UmF0ZUCil+X/DkjlnPj/DmIeCgJpZBoDSUQhQMbD+/8OSKb0+/8OagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0CA9P3/Dkjekv7/DmoHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQMGEgIAPSJSigIAPagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA/4WCgA9I76OCgA9qB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLIARADYsMBCgd0YXhSYXRlGgdUYXhSYXRlQN2a6P8OSJG++f8OYh4KAmlkGgNJRCFArsf9/w5Ip4P+/w5qB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQKu/gIAPSPDmgIAPagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAy92CgA9Iwf6CgA9qB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0DK44SAD0jPg4WAD2oHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlYsgBEARiwwEKB3RheFJhdGUaB1RheFJhdGVA9szr/w5Il5P9/w5iHgoCaWQaA0lEIUC9nIGAD0iM24GAD2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAxq2EgA9Ix9WEgA9qB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDL0oaAD0jQ9IaAD2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQKDliIAPSLaEiYAPagdUYXhSYXRlagxUYXhHcm91cFJhdGViyAEQBWLDAQoHdGF4UmF0ZRoHVGF4UmF0ZUDqy+7/Dkj52/3/DmIeCgJpZBoDSUQhQPTagYAPSMeXgoAPagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0CCuoSAD0jL4ISAD2oHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQJvehoAPSPP+hoAPagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdAheqIgA9I5IeJgA9qB1RheFJhdGVqDFRheEdyb3VwUmF0ZWoIVGF4R3JvdXBqB1RheEluZm9qGFNhbGVzVHJhbnNhY3Rpb25JdGVtTGluZWoMU2FsZXNSZWNlaXB0Yl4KCG1ldGFkYXRhGghNZXRhZGF0YUDWmZb9Dkizp8D+DmIuCg1lbnRpdHlWZXJzaW9uGgdTdHJpbmchQPipxf4OSPztxf4OaghNZXRhZGF0YWoMU2FsZXNSZWNlaXB0YvgDCghzaGlwcGluZxoPU2hpcHBpbmdEZXRhaWxzQMG2pf4OSOLmxf4OYi0KCHNoaXBEYXRlGgREYXRlQMqlyf4OSNvayf4Oag9TaGlwcGluZ0RldGFpbHNiLgoHc2hpcFZpYRoGU3RyaW5nQJGtzv4OSOzYzv4Oag9TaGlwcGluZ0RldGFpbHNiNQoOdHJhY2tpbmdOdW1iZXIaBlN0cmluZ0DGv9T+Dkjm4tT+DmoPU2hpcHBpbmdEZXRhaWxzYjUKDnNoaXBwaW5nQW1vdW50GgZBbW91bnRA48bW/g5IouPW/g5qD1NoaXBwaW5nRGV0YWlsc2J3CgtzaGlwQWRkcmVzcxoPRnJlZUZvcm1BZGRyZXNzQIWv0P4OSIb43/4OYjoKE2ZyZWVGb3JtQWRkcmVzc0xpbmUaBlN0cmluZ0Cno+P+Dkjb9uP+DmoPRnJlZUZvcm1BZGRyZXNzag9TaGlwcGluZ0RldGFpbHNiewoPc2hpcEZyb21BZGRyZXNzGg9GcmVlRm9ybUFkZHJlc3NA+sTS/g5In57h/g5iOgoTZnJlZUZvcm1BZGRyZXNzTGluZRoGU3RyaW5nQP6T5f4OSMXN5f4Oag9GcmVlRm9ybUFkZHJlc3NqD1NoaXBwaW5nRGV0YWlsc2oMU2FsZXNSZWNlaXB0YvQBCgdwYXltZW50GgtQYXltZW50SW5mb0Cf9LT+DkiZ/dP+DmLBAQoNcGF5bWVudE1ldGhvZBoNUGF5bWVudE1ldGhvZECptNf+DkiB6ej+DmIjCgJpZBoCSURAoqLs/g5Ir9js/g5qDVBheW1lbnRNZXRob2RiKQoEbmFtZRoGU3RyaW5nQNmB7/4OSN2l7/4Oag1QYXltZW50TWV0aG9kYjgKBHR5cGUaFVBheW1lbnRNZXRob2RUeXBlRW51bUCxhvH+DkiqpPH+DmoNUGF5bWVudE1ldGhvZGoLUGF5bWVudEluZm9qDFNhbGVzUmVjZWlwdGoITXV0YXRpb24="
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
  },
  "extensions": {
    "tracing": {
      "version": 1,
      "startTime": "2021-09-07T20:35:35.466303Z",
      "endTime": "2021-09-07T20:35:37.575714Z",
      "duration": 2109390531,
      "parsing": {
        "startOffset": 1664436,
        "duration": 1480630
      },
      "validation": {
        "startOffset": 2411159,
        "duration": 728099
      },
      "execution": {
        "resolvers": [
          {
            "path": [
              "updateSalesReceipt"
            ],
            "parentType": "Mutation",
            "returnType": "SalesReceipt",
            "fieldName": "updateSalesReceipt",
            "startOffset": 2659640,
            "duration": 2081136451
          },
          {
            "path": [
              "updateSalesReceipt",
              "id"
            ],
            "parentType": "SalesReceipt",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2083899714,
            "duration": 9853
          },
          {
            "path": [
              "updateSalesReceipt",
              "transactionDate"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Date",
            "fieldName": "transactionDate",
            "startOffset": 2083981485,
            "duration": 2835
          },
          {
            "path": [
              "updateSalesReceipt",
              "referenceNumber"
            ],
            "parentType": "SalesReceipt",
            "returnType": "String",
            "fieldName": "referenceNumber",
            "startOffset": 2084055846,
            "duration": 3478
          },
          {
            "path": [
              "updateSalesReceipt",
              "voided"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Boolean",
            "fieldName": "voided",
            "startOffset": 2084084591,
            "duration": 2720
          },
          {
            "path": [
              "updateSalesReceipt",
              "amount"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Amount",
            "fieldName": "amount",
            "startOffset": 2084110278,
            "duration": 2452
          },
          {
            "path": [
              "updateSalesReceipt",
              "location"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Location",
            "fieldName": "location",
            "startOffset": 2084167182,
            "duration": 4784
          },
          {
            "path": [
              "updateSalesReceipt",
              "location",
              "id"
            ],
            "parentType": "Location",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 2084207395,
            "duration": 2665
          },
          {
            "path": [
              "updateSalesReceipt",
              "location",
              "name"
            ],
            "parentType": "Location",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2084234030,
            "duration": 2261
          },
          {
            "path": [
              "updateSalesReceipt",
              "billingAddress"
            ],
            "parentType": "SalesReceipt",
            "returnType": "FreeFormAddress",
            "fieldName": "billingAddress",
            "startOffset": 2084360347,
            "duration": 3448
          },
          {
            "path": [
              "updateSalesReceipt",
              "billingAddress",
              "freeFormAddressLine"
            ],
            "parentType": "FreeFormAddress",
            "returnType": "String",
            "fieldName": "freeFormAddressLine",
            "startOffset": 2084398019,
            "duration": 2783
          },
          {
            "path": [
              "updateSalesReceipt",
              "privateMemo"
            ],
            "parentType": "SalesReceipt",
            "returnType": "String",
            "fieldName": "privateMemo",
            "startOffset": 2084436469,
            "duration": 2487
          },
          {
            "path": [
              "updateSalesReceipt",
              "customerMemo"
            ],
            "parentType": "SalesReceipt",
            "returnType": "String",
            "fieldName": "customerMemo",
            "startOffset": 2084461317,
            "duration": 2205
          },
          {
            "path": [
              "updateSalesReceipt",
              "currency"
            ],
            "parentType": "SalesReceipt",
            "returnType": "CurrencyInfo",
            "fieldName": "currency",
            "startOffset": 2084307741,
            "duration": 511398
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax"
            ],
            "parentType": "SalesReceipt",
            "returnType": "TransactionTaxInfo",
            "fieldName": "tax",
            "startOffset": 2084827279,
            "duration": 6518
          },
          {
            "path": [
              "updateSalesReceipt",
              "account"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Account",
            "fieldName": "account",
            "startOffset": 2084275226,
            "duration": 581845
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "totalTaxAmount"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "Amount",
            "fieldName": "totalTaxAmount",
            "startOffset": 2084891450,
            "duration": 4216
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxable"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "Boolean",
            "fieldName": "taxable",
            "startOffset": 2084962164,
            "duration": 2990
          },
          {
            "path": [
              "updateSalesReceipt",
              "emailDeliveryInfo"
            ],
            "parentType": "SalesReceipt",
            "returnType": "EmailDeliveryInfo",
            "fieldName": "emailDeliveryInfo",
            "startOffset": 2084514813,
            "duration": 496616
          },
          {
            "path": [
              "updateSalesReceipt",
              "shipping"
            ],
            "parentType": "SalesReceipt",
            "returnType": "ShippingDetails",
            "fieldName": "shipping",
            "startOffset": 2084540990,
            "duration": 792351
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Customer",
            "fieldName": "customer",
            "startOffset": 2084335185,
            "duration": 1018545
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "TaxGroup",
            "fieldName": "taxGroup",
            "startOffset": 2084928353,
            "duration": 598789
          },
          {
            "path": [
              "updateSalesReceipt",
              "currency",
              "name"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2085735050,
            "duration": 6064
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails"
            ],
            "parentType": "TransactionTaxInfo",
            "returnType": "[TaxDetails]",
            "fieldName": "taxDetails",
            "startOffset": 2084991333,
            "duration": 786337
          },
          {
            "path": [
              "updateSalesReceipt",
              "emailDeliveryInfo",
              "to"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "[String!]",
            "fieldName": "to",
            "startOffset": 2085771849,
            "duration": 7553
          },
          {
            "path": [
              "updateSalesReceipt",
              "account",
              "id"
            ],
            "parentType": "Account",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 2085796136,
            "duration": 6570
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines"
            ],
            "parentType": "SalesReceipt",
            "returnType": "[SalesTransactionItemLine]",
            "fieldName": "itemLines",
            "startOffset": 2084485837,
            "duration": 1403445
          },
          {
            "path": [
              "updateSalesReceipt",
              "shipping",
              "shipDate"
            ],
            "parentType": "ShippingDetails",
            "returnType": "Date",
            "fieldName": "shipDate",
            "startOffset": 2085886807,
            "duration": 7864
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "id"
            ],
            "parentType": "Customer",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 2085919138,
            "duration": 6041
          },
          {
            "path": [
              "updateSalesReceipt",
              "payment"
            ],
            "parentType": "SalesReceipt",
            "returnType": "PaymentInfo",
            "fieldName": "payment",
            "startOffset": 2085180847,
            "duration": 783078
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "id"
            ],
            "parentType": "TaxGroup",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2085982928,
            "duration": 6026
          },
          {
            "path": [
              "updateSalesReceipt",
              "currency",
              "currency"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "String",
            "fieldName": "currency",
            "startOffset": 2086093048,
            "duration": 5168
          },
          {
            "path": [
              "updateSalesReceipt",
              "emailDeliveryInfo",
              "cc"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "[String!]",
            "fieldName": "cc",
            "startOffset": 2086432935,
            "duration": 5194
          },
          {
            "path": [
              "updateSalesReceipt",
              "metadata"
            ],
            "parentType": "SalesReceipt",
            "returnType": "Metadata",
            "fieldName": "metadata",
            "startOffset": 2083944022,
            "duration": 2688440
          },
          {
            "path": [
              "updateSalesReceipt",
              "shipping",
              "shipVia"
            ],
            "parentType": "ShippingDetails",
            "returnType": "String",
            "fieldName": "shipVia",
            "startOffset": 2086632130,
            "duration": 7908
          },
          {
            "path": [
              "updateSalesReceipt",
              "payment",
              "paymentMethod"
            ],
            "parentType": "PaymentInfo",
            "returnType": "PaymentMethod",
            "fieldName": "paymentMethod",
            "startOffset": 2086498910,
            "duration": 297251
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "name"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2086805928,
            "duration": 5915
          },
          {
            "path": [
              "updateSalesReceipt",
              "currency",
              "symbol"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "String",
            "fieldName": "symbol",
            "startOffset": 2086884025,
            "duration": 6691
          },
          {
            "path": [
              "updateSalesReceipt",
              "account",
              "name"
            ],
            "parentType": "Account",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2086921831,
            "duration": 5583
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 2087083359,
            "duration": 4748
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "displayName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "displayName",
            "startOffset": 2087111738,
            "duration": 5541
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "sequence"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "String",
            "fieldName": "sequence",
            "startOffset": 2087149327,
            "duration": 7083
          },
          {
            "path": [
              "updateSalesReceipt",
              "emailDeliveryInfo",
              "bcc"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "[String!]",
            "fieldName": "bcc",
            "startOffset": 2087162949,
            "duration": 5420
          },
          {
            "path": [
              "updateSalesReceipt",
              "currency",
              "exchangeRate"
            ],
            "parentType": "CurrencyInfo",
            "returnType": "Amount",
            "fieldName": "exchangeRate",
            "startOffset": 2087417870,
            "duration": 9076
          },
          {
            "path": [
              "updateSalesReceipt",
              "metadata",
              "entityVersion"
            ],
            "parentType": "Metadata",
            "returnType": "String!",
            "fieldName": "entityVersion",
            "startOffset": 2087441687,
            "duration": 4753
          },
          {
            "path": [
              "updateSalesReceipt",
              "shipping",
              "shipAddress"
            ],
            "parentType": "ShippingDetails",
            "returnType": "FreeFormAddress",
            "fieldName": "shipAddress",
            "startOffset": 2087424902,
            "duration": 205808
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 2087660976,
            "duration": 5182
          },
          {
            "path": [
              "updateSalesReceipt",
              "payment",
              "paymentMethod",
              "id"
            ],
            "parentType": "PaymentMethod",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 2087675865,
            "duration": 5186
          },
          {
            "path": [
              "updateSalesReceipt",
              "account",
              "fullyQualifiedName"
            ],
            "parentType": "Account",
            "returnType": "String",
            "fieldName": "fullyQualifiedName",
            "startOffset": 2087895579,
            "duration": 5667
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "description"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2087991252,
            "duration": 6355
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "code"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "code",
            "startOffset": 2088031715,
            "duration": 4996
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "firstName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "firstName",
            "startOffset": 2088109916,
            "duration": 8121
          },
          {
            "path": [
              "updateSalesReceipt",
              "emailDeliveryInfo",
              "status"
            ],
            "parentType": "EmailDeliveryInfo",
            "returnType": "EmailStatus",
            "fieldName": "status",
            "startOffset": 2088325712,
            "duration": 5732
          },
          {
            "path": [
              "updateSalesReceipt",
              "payment",
              "paymentMethod",
              "name"
            ],
            "parentType": "PaymentMethod",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2088374924,
            "duration": 5498
          },
          {
            "path": [
              "updateSalesReceipt",
              "shipping",
              "shipAddress",
              "freeFormAddressLine"
            ],
            "parentType": "FreeFormAddress",
            "returnType": "String",
            "fieldName": "freeFormAddressLine",
            "startOffset": 2088463436,
            "duration": 6096
          },
          {
            "path": [
              "updateSalesReceipt",
              "shipping",
              "shipFromAddress"
            ],
            "parentType": "ShippingDetails",
            "returnType": "FreeFormAddress",
            "fieldName": "shipFromAddress",
            "startOffset": 2088346171,
            "duration": 169949
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2088494827,
            "duration": 240645
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "amount"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Amount",
            "fieldName": "amount",
            "startOffset": 2088732443,
            "duration": 7129
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "lastName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "lastName",
            "startOffset": 2088765439,
            "duration": 7606
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "description"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2088790250,
            "duration": 6188
          },
          {
            "path": [
              "updateSalesReceipt",
              "shipping",
              "trackingNumber"
            ],
            "parentType": "ShippingDetails",
            "returnType": "String",
            "fieldName": "trackingNumber",
            "startOffset": 2088842254,
            "duration": 5370
          },
          {
            "path": [
              "updateSalesReceipt",
              "payment",
              "paymentMethod",
              "type"
            ],
            "parentType": "PaymentMethod",
            "returnType": "PaymentMethodTypeEnum",
            "fieldName": "type",
            "startOffset": 2088914206,
            "duration": 5261
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 2089094435,
            "duration": 5610
          },
          {
            "path": [
              "updateSalesReceipt",
              "shipping",
              "shipFromAddress",
              "freeFormAddressLine"
            ],
            "parentType": "FreeFormAddress",
            "returnType": "String",
            "fieldName": "freeFormAddressLine",
            "startOffset": 2089102598,
            "duration": 5078
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates"
            ],
            "parentType": "TaxGroup",
            "returnType": "[TaxGroupRate]",
            "fieldName": "saleRates",
            "startOffset": 2089409961,
            "duration": 7409
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2089582484,
            "duration": 6168
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "unitPrice"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Amount",
            "fieldName": "unitPrice",
            "startOffset": 2089610353,
            "duration": 5170
          },
          {
            "path": [
              "updateSalesReceipt",
              "shipping",
              "shippingAmount"
            ],
            "parentType": "ShippingDetails",
            "returnType": "Amount",
            "fieldName": "shippingAmount",
            "startOffset": 2089624065,
            "duration": 6022
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "companyName"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "companyName",
            "startOffset": 2089712285,
            "duration": 6125
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 2089746035,
            "duration": 6243
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2089813640,
            "duration": 221592
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2090091890,
            "duration": 5939
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "notes"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "notes",
            "startOffset": 2090244843,
            "duration": 5207
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "class"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Class",
            "fieldName": "class",
            "startOffset": 2090139499,
            "duration": 284765
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2090269465,
            "duration": 248818
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2090548498,
            "duration": 6819
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2090302475,
            "duration": 260584
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2090587909,
            "duration": 7177
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "website"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "website",
            "startOffset": 2090794468,
            "duration": 5344
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "item"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Item",
            "fieldName": "item",
            "startOffset": 2090705393,
            "duration": 288951
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2091085844,
            "duration": 258748
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2091407684,
            "duration": 7553
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2091457728,
            "duration": 7432
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 2091468253,
            "duration": 7967
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2091590817,
            "duration": 9722
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2091621787,
            "duration": 5863
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "quantity"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "Int",
            "fieldName": "quantity",
            "startOffset": 2091801366,
            "duration": 7101
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "class",
              "id"
            ],
            "parentType": "Class",
            "returnType": "String",
            "fieldName": "id",
            "startOffset": 2091823172,
            "duration": 6475
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "item",
              "id"
            ],
            "parentType": "InventoryItem",
            "returnType": "ID",
            "fieldName": "id",
            "startOffset": 2091836634,
            "duration": 6451
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "email"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "email",
            "startOffset": 2091873159,
            "duration": 7188
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2092054099,
            "duration": 6984
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2092226319,
            "duration": 6615
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 2092441068,
            "duration": 7867
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2092444271,
            "duration": 5880
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2092000185,
            "duration": 493702
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2092645431,
            "duration": 5234
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2092681790,
            "duration": 5890
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "phone"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "phone",
            "startOffset": 2092691463,
            "duration": 5438
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2093167365,
            "duration": 5250
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2093219587,
            "duration": 6829
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2093551007,
            "duration": 6971
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax"
            ],
            "parentType": "SalesTransactionItemLine",
            "returnType": "TaxInfo",
            "fieldName": "tax",
            "startOffset": 2092944424,
            "duration": 725783
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2093406566,
            "duration": 283238
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "item",
              "name"
            ],
            "parentType": "InventoryItem",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2093709353,
            "duration": 6912
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "class",
              "name"
            ],
            "parentType": "Class",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2093751914,
            "duration": 6163
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2093906670,
            "duration": 6716
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2094000379,
            "duration": 7649
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "mobile"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "mobile",
            "startOffset": 2094075454,
            "duration": 7160
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2094248726,
            "duration": 6700
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2094284595,
            "duration": 6683
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 2094349101,
            "duration": 6044
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              0,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2094363829,
            "duration": 6106
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2094401805,
            "duration": 7157
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2094242364,
            "duration": 220092
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "item",
              "sku"
            ],
            "parentType": "InventoryItem",
            "returnType": "String",
            "fieldName": "sku",
            "startOffset": 2094538798,
            "duration": 6746
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxAmount"
            ],
            "parentType": "TaxInfo",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 2094778560,
            "duration": 6315
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2094792727,
            "duration": 6138
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2094885162,
            "duration": 5597
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "fax"
            ],
            "parentType": "Customer",
            "returnType": "String",
            "fieldName": "fax",
            "startOffset": 2094901117,
            "duration": 5290
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2094899714,
            "duration": 7405
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2095002712,
            "duration": 5439
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 2095189587,
            "duration": 5428
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2095038932,
            "duration": 194917
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2095380375,
            "duration": 7140
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2095482776,
            "duration": 7900
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2095570301,
            "duration": 6331
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2095641864,
            "duration": 5506
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2096056673,
            "duration": 7182
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2096173980,
            "duration": 6897
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup"
            ],
            "parentType": "TaxInfo",
            "returnType": "TaxGroup",
            "fieldName": "taxGroup",
            "startOffset": 2095711403,
            "duration": 471637
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods"
            ],
            "parentType": "Customer",
            "returnType": "[ContactMethod!]!",
            "fieldName": "contactMethods",
            "startOffset": 2096328923,
            "duration": 9525
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxable"
            ],
            "parentType": "TaxInfo",
            "returnType": "Boolean",
            "fieldName": "taxable",
            "startOffset": 2096393105,
            "duration": 6508
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2096405200,
            "duration": 7047
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2096453264,
            "duration": 5847
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2096650964,
            "duration": 5304
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2096674883,
            "duration": 7162
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2096789163,
            "duration": 7315
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2096789163,
            "duration": 7315
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2096710130,
            "duration": 283266
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "id"
            ],
            "parentType": "TaxGroup",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2097003509,
            "duration": 7162
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2097295555,
            "duration": 6897
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2097467341,
            "duration": 6566
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2097797696,
            "duration": 7516
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2097834077,
            "duration": 7029
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2097965436,
            "duration": 7201
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2098042495,
            "duration": 7395
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 2098118226,
            "duration": 6690
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2098177660,
            "duration": 7372
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2098277927,
            "duration": 5911
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "type"
            ],
            "parentType": "ContactMethod",
            "returnType": "ContactType",
            "fieldName": "type",
            "startOffset": 2098327966,
            "duration": 6859
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2098545456,
            "duration": 6840
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2098576482,
            "duration": 7239
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2098633331,
            "duration": 5544
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2098766508,
            "duration": 5513
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              1,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2099060694,
            "duration": 6249
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "primary"
            ],
            "parentType": "ContactMethod",
            "returnType": "Boolean",
            "fieldName": "primary",
            "startOffset": 2099339287,
            "duration": 6387
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "name"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2099583827,
            "duration": 7379
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2099635673,
            "duration": 6477
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2099665938,
            "duration": 5465
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2099792263,
            "duration": 5144
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 2099841972,
            "duration": 6000
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2099859099,
            "duration": 7530
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2099866629,
            "duration": 7485
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2099872989,
            "duration": 6919
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address"
            ],
            "parentType": "ContactMethod",
            "returnType": "Address",
            "fieldName": "address",
            "startOffset": 2100015804,
            "duration": 7819
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "code"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "code",
            "startOffset": 2100098956,
            "duration": 6496
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2100186857,
            "duration": 5862
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2100243926,
            "duration": 5274
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2100385605,
            "duration": 5785
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "streetAddress1"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress1",
            "startOffset": 2100731745,
            "duration": 5059
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "description"
            ],
            "parentType": "TaxGroup",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2100783854,
            "duration": 7956
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2100526331,
            "duration": 301223
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              2,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2100863019,
            "duration": 6226
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2100943578,
            "duration": 7880
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2100993045,
            "duration": 6225
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2101117759,
            "duration": 5131
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxAmount",
            "startOffset": 2101162268,
            "duration": 5077
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates"
            ],
            "parentType": "TaxGroup",
            "returnType": "[TaxGroupRate]",
            "fieldName": "saleRates",
            "startOffset": 2101396912,
            "duration": 8103
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "streetAddress2"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress2",
            "startOffset": 2101659424,
            "duration": 5895
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2101657017,
            "duration": 7965
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2101685125,
            "duration": 6095
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2101809293,
            "duration": 5609
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2101906139,
            "duration": 6840
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxableAmount"
            ],
            "parentType": "TaxDetails",
            "returnType": "Amount",
            "fieldName": "taxableAmount",
            "startOffset": 2101986722,
            "duration": 6103
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2102243400,
            "duration": 6856
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2102056340,
            "duration": 290235
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "city"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "city",
            "startOffset": 2102412089,
            "duration": 6002
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2102510741,
            "duration": 5637
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2102612254,
            "duration": 5702
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              3,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2102687116,
            "duration": 6195
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "state"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "state",
            "startOffset": 2102944742,
            "duration": 5208
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate"
            ],
            "parentType": "TaxDetails",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2102830834,
            "duration": 204468
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2103069535,
            "duration": 5829
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2103079982,
            "duration": 6101
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2103010620,
            "duration": 216841
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "country"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "country",
            "startOffset": 2103330941,
            "duration": 4798
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2103501915,
            "duration": 5769
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2103728456,
            "duration": 6423
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2103799778,
            "duration": 5750
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2103891279,
            "duration": 5363
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2103705603,
            "duration": 229094
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2103945260,
            "duration": 5163
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              0,
              "address",
              "zipCode"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "zipCode",
            "startOffset": 2104006548,
            "duration": 6477
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2104211540,
            "duration": 5593
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2104510670,
            "duration": 6164
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2104763409,
            "duration": 7799
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2104849474,
            "duration": 6002
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2104946859,
            "duration": 5826
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "type"
            ],
            "parentType": "ContactMethod",
            "returnType": "ContactType",
            "fieldName": "type",
            "startOffset": 2105004190,
            "duration": 6363
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2105036035,
            "duration": 6234
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2105041261,
            "duration": 5443
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2104987171,
            "duration": 243077
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              4,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2105299636,
            "duration": 5382
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2105300048,
            "duration": 6523
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              0,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2105388574,
            "duration": 5127
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2105889416,
            "duration": 7428
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "status"
            ],
            "parentType": "TaxRate",
            "returnType": "ActiveStatus",
            "fieldName": "status",
            "startOffset": 2105905860,
            "duration": 7433
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2105690305,
            "duration": 271794
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "primary"
            ],
            "parentType": "ContactMethod",
            "returnType": "Boolean",
            "fieldName": "primary",
            "startOffset": 2105955077,
            "duration": 6905
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2105984353,
            "duration": 6406
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              1,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2106016898,
            "duration": 6406
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2106410940,
            "duration": 5793
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate"
            ],
            "parentType": "TaxGroupRate",
            "returnType": "TaxRate",
            "fieldName": "taxRate",
            "startOffset": 2106187005,
            "duration": 258402
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "startDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "startDate",
            "startOffset": 2106537461,
            "duration": 7515
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2106629826,
            "duration": 6251
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2106717069,
            "duration": 6345
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address"
            ],
            "parentType": "ContactMethod",
            "returnType": "Address",
            "fieldName": "address",
            "startOffset": 2106727424,
            "duration": 11125
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              2,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2106880321,
            "duration": 4921
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "id"
            ],
            "parentType": "TaxRate",
            "returnType": "ID!",
            "fieldName": "id",
            "startOffset": 2106948626,
            "duration": 5981
          },
          {
            "path": [
              "updateSalesReceipt",
              "tax",
              "taxDetails",
              5,
              "taxRate",
              "rate"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "rate",
            "startOffset": 2107012779,
            "duration": 5595
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2107088283,
            "duration": 5125
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2107205291,
            "duration": 5466
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "streetAddress1"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress1",
            "startOffset": 2107265716,
            "duration": 5852
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "name"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "name",
            "startOffset": 2107360949,
            "duration": 5174
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              3,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2107484459,
            "duration": 4959
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2107643642,
            "duration": 5153
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "streetAddress2"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "streetAddress2",
            "startOffset": 2107728620,
            "duration": 4675
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "endDate"
            ],
            "parentType": "TaxRate",
            "returnType": "Date",
            "fieldName": "endDate",
            "startOffset": 2107776818,
            "duration": 5005
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              4,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2108042170,
            "duration": 4943
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "city"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "city",
            "startOffset": 2108166438,
            "duration": 4976
          },
          {
            "path": [
              "updateSalesReceipt",
              "itemLines",
              0,
              "tax",
              "taxGroup",
              "saleRates",
              5,
              "taxRate",
              "description"
            ],
            "parentType": "TaxRate",
            "returnType": "String",
            "fieldName": "description",
            "startOffset": 2108209793,
            "duration": 4896
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "state"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "state",
            "startOffset": 2108535645,
            "duration": 4778
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "country"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "country",
            "startOffset": 2108917151,
            "duration": 4570
          },
          {
            "path": [
              "updateSalesReceipt",
              "customer",
              "contactMethods",
              1,
              "address",
              "zipCode"
            ],
            "parentType": "Address",
            "returnType": "String",
            "fieldName": "zipCode",
            "startOffset": 2109282627,
            "duration": 4379
          }
        ]
      }
    },
    "ftv1": "GgwImZrfiQYQ0NnGkgIiDAiXmt+JBhDQh63eAVjIpe7tB3LDU2LAUwoSdXBkYXRlU2FsZXNSZWNlaXB0GgxTYWxlc1JlY2VpcHRA6pGiAUiG6dDhB2IjCgJpZBoDSUQhQJ/61uEHSJ3O1+EHagxTYWxlc1JlY2VpcHRiMQoPdHJhbnNhY3Rpb25EYXRlGgREYXRlQPb02+EHSNWQ3OEHagxTYWxlc1JlY2VpcHRiMwoPcmVmZXJlbmNlTnVtYmVyGgZTdHJpbmdAr7rg4QdIiNvg4QdqDFNhbGVzUmVjZWlwdGIrCgZ2b2lkZWQaB0Jvb2xlYW5A1Zri4QdIx7Pi4QdqDFNhbGVzUmVjZWlwdGIqCgZhbW91bnQaBkFtb3VudEDp4uPhB0ir+ePhB2oMU2FsZXNSZWNlaXB0YnQKCGxvY2F0aW9uGghMb2NhdGlvbkDAn+fhB0jZyefhB2IeCgJpZBoCSURA9dnp4QdIrvPp4QdqCExvY2F0aW9uYiQKBG5hbWUaBlN0cmluZ0C7qevhB0jpvuvhB2oITG9jYXRpb25qDFNhbGVzUmVjZWlwdGJ3Cg5iaWxsaW5nQWRkcmVzcxoPRnJlZUZvcm1BZGRyZXNzQKaE8+EHSOqk8+EHYjoKE2ZyZWVGb3JtQWRkcmVzc0xpbmUaBlN0cmluZ0D+qvXhB0j4xPXhB2oPRnJlZUZvcm1BZGRyZXNzagxTYWxlc1JlY2VpcHRiLwoLcHJpdmF0ZU1lbW8aBlN0cmluZ0CL1/fhB0j67vfhB2oMU2FsZXNSZWNlaXB0YjAKDGN1c3RvbWVyTWVtbxoGU3RyaW5nQIGZ+eEHSOKt+eEHagxTYWxlc1JlY2VpcHRi6AEKCGN1cnJlbmN5GgxDdXJyZW5jeUluZm9Aw+nv4QdIqJmP4gdiKAoEbmFtZRoGU3RyaW5nQMH7xuIHSLy1x+IHagxDdXJyZW5jeUluZm9iLAoIY3VycmVuY3kaBlN0cmluZ0Ch59ziB0jhmN3iB2oMQ3VycmVuY3lJbmZvYioKBnN5bWJvbBoGU3RyaW5nQISOjeMHSMHMjeMHagxDdXJyZW5jeUluZm9iMAoMZXhjaGFuZ2VSYXRlGgZBbW91bnRAkNit4wdI66uu4wdqDEN1cnJlbmN5SW5mb2oMU2FsZXNSZWNlaXB0YscmCgN0YXgaElRyYW5zYWN0aW9uVGF4SW5mb0CVx4/iB0jkhJDiB2I4Cg50b3RhbFRheEFtb3VudBoGQW1vdW50QOq7k+IHSILik+IHahJUcmFuc2FjdGlvblRheEluZm9iMgoHdGF4YWJsZRoHQm9vbGVhbkCS45fiB0ikgZjiB2oSVHJhbnNhY3Rpb25UYXhJbmZvYqARCgh0YXhHcm91cBoIVGF4R3JvdXBA6duV4gdIn7C64gdiHwoCaWQaA0lEIUC5jNbiB0i3xtbiB2oIVGF4R3JvdXBiJAoEbmFtZRoGU3RyaW5nQNupiOMHSJXjiOMHaghUYXhHcm91cGIkCgRjb2RlGgZTdHJpbmdA2JDT4wdI48DT4wdqCFRheEdyb3VwYisKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA6LiB5AdItfWB5AdqCFRheEdyb3VwYs8PCglzYWxlUmF0ZXMaDltUYXhHcm91cFJhdGVdQNShp+QHSPzjp+QHYsICEABivQIKB3RheFJhdGUaB1RheFJhdGVAt/K/5AdIvcDN5AdiHgoCaWQaA0lEIUCP4OzkB0iCpe3kB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA56Ck5QdIl+ek5QdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUCu3uzlB0i6ke3lB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQLi6v+YHSImFwOYHagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQJSs9uYHSLH29uYHagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUCJm+HnB0jszuHnB2oHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA6u3U6AdI56/V6AdqB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLCAhABYr0CCgd0YXhSYXRlGgdUYXhSYXRlQI3e3eQHSLLg7eQHYh4KAmlkGgNJRCFApqGu5QdI+9yu5QdqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQIe74OUHSIj14OUHagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAp+XQ5gdIw6XR5gdqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0DP1pPnB0jTnJTnB2oHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0Cy2OLnB0jlnePnB2oHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVAzuDW6AdIoajX6AdqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQJjApekHSPWIpukHagdUYXhSYXRlagxUYXhHcm91cFJhdGViwgIQAmK9AgoHdGF4UmF0ZRoHVGF4UmF0ZUD7x43lB0jdup3lB2IeCgJpZBoDSUQhQILUyOUHSJaYyeUHagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0D5y4zmB0iQ/4zmB2oHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQPLNzuYHSNWOz+YHagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdAic785gdIhoP95gdqB1RheFJhdGViKwoGc3RhdHVzGgxBY3RpdmVTdGF0dXNA5pLV5wdIxc7V5wdqB1RheFJhdGViJgoJc3RhcnREYXRlGgREYXRlQMCUtugHSKjdtugHagdUYXhSYXRlYiMKBHJhdGUaBlN0cmluZ0D3nZnpB0j70pnpB2oHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlYsICEANivQIKB3RheFJhdGUaB1RheFJhdGVAnK3F5QdI6cvj5QdiHgoCaWQaA0lEIUDWgqTmB0iNyqTmB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA9vnX5gdIpL3Y5gdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUCZ9ZnnB0iVw5rnB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQK76vOcHSNnBvecHagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQObV6ecHSKuc6ucHagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUDMtL7oB0jk+77oB2oHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA96ri6AdIzuDi6AdqB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLCAhAEYr0CCgd0YXhSYXRlGgdUYXhSYXRlQPqbzuYHSLXc2+YHYh4KAmlkGgNJRCFA6KGf5wdI0+Cf5wdqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQJvJiOgHSOaMiegHagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVAxvig6QdIhKuh6QdqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0C3wbzpB0jQ9LzpB2oHVGF4UmF0ZWIrCgZzdGF0dXMaDEFjdGl2ZVN0YXR1c0D2nurpB0i22+rpB2oHVGF4UmF0ZWImCglzdGFydERhdGUaBERhdGVAhIec6gdI5r+c6gdqB1RheFJhdGViIwoEcmF0ZRoGU3RyaW5nQIzvxuoHSNSlx+oHagdUYXhSYXRlagxUYXhHcm91cFJhdGViwgIQBWK9AgoHdGF4UmF0ZRoHVGF4UmF0ZUDs6f7mB0jN5YrnB2IeCgJpZBoDSUQhQIKd0ucHSK3i0ucHagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0CZnKfoB0i05qfoB2oHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQOiyl+kHSMjyl+kHagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA4oO56QdI1Lq56QdqB1RheFJhdGViKwoGc3RhdHVzGgxBY3RpdmVTdGF0dXNA/Z3n6QdI3Ozn6QdqB1RheFJhdGViJgoJc3RhcnREYXRlGgREYXRlQPe8lOoHSJL2lOoHagdUYXhSYXRlYiMKBHJhdGUaBlN0cmluZ0C3iM3qB0iMwM3qB2oHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlaghUYXhHcm91cGoSVHJhbnNhY3Rpb25UYXhJbmZvYoAUCgp0YXhEZXRhaWxzGgxbVGF4RGV0YWlsc11ApsaZ4gdIq9vJ4gdingMQAGIrCgl0YXhBbW91bnQaBkFtb3VudECGoJnjB0j2zJnjB2oKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAosG84wdIkfK84wdqClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVA/7Lv4wdIwpn+4wdiHgoCaWQaA0lEIUCo5bHkB0izoLLkB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA+PDQ5AdI6qvR5AdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDHle/kB0jF3e/kB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQKyaoeUHSKDioeUHagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQPz67uUHSPuz7+UHagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUCh5o/mB0j8ppDmB2oHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA3s/V5gdI143W5gdqB1RheFJhdGVqClRheERldGFpbHNingMQAWIrCgl0YXhBbW91bnQaBkFtb3VudEDHgJTkB0jAtpTkB2oKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAseO75AdIxqG85AdqClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVA6Nvb5AdI1YHr5AdiHgoCaWQaA0lEIUCosazlB0jUi63lB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA1pTT5QdI3dXT5QdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDN3LnmB0jPnrrmB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQJvn7+YHSM6i8OYHagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQNWOxOcHSNDRxOcHagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUDqurHoB0ip/rHoB2oHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdAhqb06AdIteX06AdqB1RheFJhdGVqClRheERldGFpbHNingMQAmIrCgl0YXhBbW91bnQaBkFtb3VudEDY86TlB0jMwaXlB2oKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRA8KTg5QdIw+/g5QdqClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVAxZqb5gdIs8us5gdiHgoCaWQaA0lEIUCHufXmB0jg7vXmB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAl9Cj5wdIwIOk5wdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDV1ennB0irnOrnB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQI+Gk+gHSKfHk+gHagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQN3CxOgHSIH8xOgHagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUCA8aXpB0jStabpB2oHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA66bi6QdIs+Pi6QdqB1RheFJhdGVqClRheERldGFpbHNingMQA2IrCgl0YXhBbW91bnQaBkFtb3VudED23dTmB0jtlNXmB2oKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAwoKI5wdIvLaI5wdqClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVA2+vk5wdIw5z25wdiHgoCaWQaA0lEIUCXuKnoB0jN/anoB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAtZra6AdIzNDa6AdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDrhaXpB0jf0aXpB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQLKUxekHSN/MxekHagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQLTs8ekHSP6d8ukHagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUC6/aHqB0ilv6LqB2oHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdAptHR6gdIwY7S6gdqB1RheFJhdGVqClRheERldGFpbHNingMQBGIrCgl0YXhBbW91bnQaBkFtb3VudEDt47roB0jipLvoB2oKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAy/2j6QdIsbek6QdqClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVArd/N6QdI5Zzg6QdiHgoCaWQaA0lEIUDe45LqB0iNtpPqB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAv8a26gdI4Iq36gdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUD8zunqB0iDi+rqB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQMKakesHSKHVkesHagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQL7WrusHSNiMr+sHagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUD6ztXrB0j2iNbrB2oHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdA54rx6wdIhb/x6wdqB1RheFJhdGVqClRheERldGFpbHNingMQBWIrCgl0YXhBbW91bnQaBkFtb3VudEDBx/TpB0je9/TpB2oKVGF4RGV0YWlsc2IvCg10YXhhYmxlQW1vdW50GgZBbW91bnRAgfKm6gdIlK2n6gdqClRheERldGFpbHNiuwIKB3RheFJhdGUaB1RheFJhdGVA57Pa6gdIuPvm6gdiHgoCaWQaA0lEIUDnroPrB0jE54PrB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdAx7ae6wdIkeie6wdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUCD+MDrB0iktsHrB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQLqo4esHSMPd4esHagdUYXhSYXRlYisKBnN0YXR1cxoMQWN0aXZlU3RhdHVzQLyOluwHSMTVluwHagdUYXhSYXRlYiYKCXN0YXJ0RGF0ZRoERGF0ZUDS1LzsB0j5nr3sB2oHVGF4UmF0ZWIjCgRyYXRlGgZTdHJpbmdAvdPZ7AdIlIna7AdqB1RheFJhdGVqClRheERldGFpbHNqElRyYW5zYWN0aW9uVGF4SW5mb2oMU2FsZXNSZWNlaXB0YqMBCgdhY2NvdW50GgdBY2NvdW50QLDr7eEHSJi+keIHYh0KAmlkGgJJREDS2criB0iTl8viB2oHQWNjb3VudGIjCgRuYW1lGgZTdHJpbmdA97KP4wdIgOeP4wdqB0FjY291bnRiMQoSZnVsbHlRdWFsaWZpZWROYW1lGgZTdHJpbmdA/+rK4wdI5aPL4wdqB0FjY291bnRqDFNhbGVzUmVjZWlwdGKHAgoRZW1haWxEZWxpdmVyeUluZm8aEUVtYWlsRGVsaXZlcnlJbmZvQIu8/OEHSIHwmuIHYi4KAnRvGglbU3RyaW5nIV1AjZ3J4gdIpevJ4gdqEUVtYWlsRGVsaXZlcnlJbmZvYi4KAmNjGglbU3RyaW5nIV1Aysfx4gdIlvrx4gdqEUVtYWlsRGVsaXZlcnlJbmZvYi8KA2JjYxoJW1N0cmluZyFdQIKPnuMHSInHnuMHahFFbWFpbERlbGl2ZXJ5SW5mb2I0CgZzdGF0dXMaC0VtYWlsU3RhdHVzQL2K5eMHSJrB5eMHahFFbWFpbERlbGl2ZXJ5SW5mb2oMU2FsZXNSZWNlaXB0YvgDCghzaGlwcGluZxoPU2hpcHBpbmdEZXRhaWxzQPyH/uEHSNPHruIHYi0KCHNoaXBEYXRlGgREYXRlQIKf0OIHSOjp0OIHag9TaGlwcGluZ0RldGFpbHNiLgoHc2hpcFZpYRoGU3RyaW5nQPHe/eIHSL6p/uIHag9TaGlwcGluZ0RldGFpbHNidwoLc2hpcEFkZHJlc3MaD0ZyZWVGb3JtQWRkcmVzc0Cmja7jB0i63rrjB2I6ChNmcmVlRm9ybUFkZHJlc3NMaW5lGgZTdHJpbmdAiL/t4wdI7/nt4wdqD0ZyZWVGb3JtQWRkcmVzc2oPU2hpcHBpbmdEZXRhaWxzYnsKD3NoaXBGcm9tQWRkcmVzcxoPRnJlZUZvcm1BZGRyZXNzQLOr5uMHSMjh8OMHYjoKE2ZyZWVGb3JtQWRkcmVzc0xpbmUaBlN0cmluZ0DXwJTkB0iD8ZTkB2oPRnJlZUZvcm1BZGRyZXNzag9TaGlwcGluZ0RldGFpbHNiNQoOdHJhY2tpbmdOdW1iZXIaBlN0cmluZ0DmzYTkB0icgIXkB2oPU2hpcHBpbmdEZXRhaWxzYjUKDnNoaXBwaW5nQW1vdW50GgZBbW91bnRA1Kq05AdI1OW05AdqD1NoaXBwaW5nRGV0YWlsc2oMU2FsZXNSZWNlaXB0Yr4KCghjdXN0b21lchoIQ3VzdG9tZXJAqcDx4QdIteav4gdiHgoCaWQaAklEQI2Z0uIHSLvR0uIHaghDdXN0b21lcmIrCgtkaXNwbGF5TmFtZRoGU3RyaW5nQOL+muMHSIyym+MHaghDdXN0b21lcmIpCglmaXJzdE5hbWUaBlN0cmluZ0DZ99fjB0ivxNjjB2oIQ3VzdG9tZXJiKAoIbGFzdE5hbWUaBlN0cmluZ0Dh9//jB0jSv4DkB2oIQ3VzdG9tZXJiKwoLY29tcGFueU5hbWUaBlN0cmluZ0DD27nkB0jhlbrkB2oIQ3VzdG9tZXJiJQoFbm90ZXMaBlN0cmluZ0Drm9rkB0jCz9rkB2oIQ3VzdG9tZXJiJwoHd2Vic2l0ZRoGU3RyaW5nQOTh++QHSMGU/OQHaghDdXN0b21lcmIlCgVlbWFpbBoGU3RyaW5nQLHPveUHSMGTvuUHaghDdXN0b21lcmIlCgVwaG9uZRoGU3RyaW5nQLDG7+UHSOP57+UHaghDdXN0b21lcmImCgZtb2JpbGUaBlN0cmluZ0CJhMTmB0ityMTmB2oIQ3VzdG9tZXJiIwoDZmF4GgZTdHJpbmdAmLb25gdIhOf25gdqCEN1c3RvbWVyYtMGCg5jb250YWN0TWV0aG9kcxoRW0NvbnRhY3RNZXRob2QhXSFArsnN5wdIhaPO5wdiigMQAGIuCgR0eXBlGgtDb250YWN0VHlwZUCqysfoB0jnjMjoB2oNQ29udGFjdE1ldGhvZGItCgdwcmltYXJ5GgdCb29sZWFuQM2mhekHSNn3hekHag1Db250YWN0TWV0aG9kYqYCCgdhZGRyZXNzGgdBZGRyZXNzQPDKrukHSKaRr+kHYi0KDnN0cmVldEFkZHJlc3MxGgZTdHJpbmdAgKTa6QdI/9Ta6QdqB0FkZHJlc3NiLQoOc3RyZWV0QWRkcmVzczIaBlN0cmluZ0DW9JLqB0iRrpPqB2oHQWRkcmVzc2IjCgRjaXR5GgZTdHJpbmdA8ezA6gdI0KfB6gdqB0FkZHJlc3NiJAoFc3RhdGUaBlN0cmluZ0C4reHqB0j13uHqB2oHQWRkcmVzc2ImCgdjb3VudHJ5GgZTdHJpbmdAkPb46gdIj6X56gdqB0FkZHJlc3NiJgoHemlwQ29kZRoGU3RyaW5nQJyWousHSJzUousHagdBZGRyZXNzag1Db250YWN0TWV0aG9kYooDEAFiLgoEdHlwZRoLQ29udGFjdFR5cGVA9off6wdI/8Tf6wdqDUNvbnRhY3RNZXRob2RiLQoHcHJpbWFyeRoHQm9vbGVhbkCcjZnsB0il05nsB2oNQ29udGFjdE1ldGhvZGKmAgoHYWRkcmVzcxoHQWRkcmVzc0DKnsjsB0jTgMnsB2ItCg5zdHJlZXRBZGRyZXNzMRoGU3RyaW5nQM6L6ewHSITD6ewHagdBZGRyZXNzYi0KDnN0cmVldEFkZHJlc3MyGgZTdHJpbmdAz6qF7QdIsNmF7QdqB0FkZHJlc3NiIwoEY2l0eRoGU3RyaW5nQLyHoO0HSKK3oO0HagdBZGRyZXNzYiQKBXN0YXRlGgZTdHJpbmdA9cu27QdIhfm27QdqB0FkZHJlc3NiJgoHY291bnRyeRoGU3RyaW5nQJHwze0HSIadzu0HagdBZGRyZXNzYiYKB3ppcENvZGUaBlN0cmluZ0Cil+TtB0iwwuTtB2oHQWRkcmVzc2oNQ29udGFjdE1ldGhvZGoIQ3VzdG9tZXJqDFNhbGVzUmVjZWlwdGLWEQoJaXRlbUxpbmVzGhpbU2FsZXNUcmFuc2FjdGlvbkl0ZW1MaW5lXUDr2PrhB0j4vtDiB2KSERAAYjgKCHNlcXVlbmNlGgZTdHJpbmdA0aWd4wdIsuqd4wdqGFNhbGVzVHJhbnNhY3Rpb25JdGVtTGluZWI7CgtkZXNjcmlwdGlvbhoGU3RyaW5nQKjW0OMHSPyT0eMHahhTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmViNgoGYW1vdW50GgZBbW91bnRAlPb94wdIorz+4wdqGFNhbGVzVHJhbnNhY3Rpb25JdGVtTGluZWI5Cgl1bml0UHJpY2UaBkFtb3VudEDFvrPkB0iI8bPkB2oYU2FsZXNUcmFuc2FjdGlvbkl0ZW1MaW5lYngKBWNsYXNzGgVDbGFzc0DN5dPkB0jpoOXkB2IfCgJpZBoGU3RyaW5nQJDIuuUHSNmDu+UHagVDbGFzc2IhCgRuYW1lGgZTdHJpbmdAmKOw5gdItN+w5gdqBUNsYXNzahhTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmVirAEKBGl0ZW0aBEl0ZW1A7an25AdI94qI5QdiIwoCaWQaAklEQIKwu+UHSKnvu+UHag1JbnZlbnRvcnlJdGVtYikKBG5hbWUaBlN0cmluZ0CM163mB0iwm67mB2oNSW52ZW50b3J5SXRlbWIoCgNza3UaBlN0cmluZ0D9p+DmB0iB6eDmB2oNSW52ZW50b3J5SXRlbWoYU2FsZXNUcmFuc2FjdGlvbkl0ZW1MaW5lYjUKCHF1YW50aXR5GgNJbnRApZ655QdIxd655QdqGFNhbGVzVHJhbnNhY3Rpb25JdGVtTGluZWLDDAoDdGF4GgdUYXhJbmZvQPr+/uUHSIa0q+YHYigKCXRheEFtb3VudBoGQW1vdW50QMT47uYHSJ617+YHagdUYXhJbmZvYrkLCgh0YXhHcm91cBoIVGF4R3JvdXBAkO+n5wdI9uPE5wdiHwoCaWQaA0lEIUCL4PbnB0j+pPfnB2oIVGF4R3JvdXBiJAoEbmFtZRoGU3RyaW5nQMuelOkHSK3nlOkHaghUYXhHcm91cGIkCgRjb2RlGgZTdHJpbmdAwNaz6QdIzJW06QdqCFRheEdyb3VwYisKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA/rvd6QdItIbe6QdqCFRheEdyb3VwYvMJCglzYWxlUmF0ZXMaDltUYXhHcm91cFJhdGVdQOfxguoHSOS9g+oHYsgBEABiwwEKB3RheFJhdGUaB1RheFJhdGVA05Or6gdI7/u86gdiHgoCaWQaA0lEIUCJ/ujqB0j8tunqB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA38WV6wdIjP2V6wdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDqx9vrB0i3gtzrB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQMbB9usHSKPz9usHagdUYXhSYXRlagxUYXhHcm91cFJhdGViyAEQAWLDAQoHdGF4UmF0ZRoHVGF4UmF0ZUDvsOXqB0i12PLqB2IeCgJpZBoDSUQhQNyPm+sHSKXFm+sHagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0CLsdDrB0jg/tDrB2oHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQIWQ8esHSNTP8esHagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdAtO+c7AdIta+d7AdqB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLIARACYsMBCgd0YXhSYXRlGgdUYXhSYXRlQJTmj+sHSKHunesHYh4KAmlkGgNJRCFAvYDh6wdIqsDh6wdqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQMONlewHSN/VlewHagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVA/vW07AdIlq617AdqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0CRyNHsB0jI+NHsB2oHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlYsgBEANiwwEKB3RheFJhdGUaB1RheFJhdGVAxYLe6wdIiPns6wdiHgoCaWQaA0lEIUD48JrsB0irtJvsB2oHVGF4UmF0ZWIjCgRuYW1lGgZTdHJpbmdA2KTC7AdI3+HC7AdqB1RheFJhdGViJAoHZW5kRGF0ZRoERGF0ZUDwoN7sB0jz0t7sB2oHVGF4UmF0ZWIqCgtkZXNjcmlwdGlvbhoGU3RyaW5nQIe49uwHSKTo9uwHagdUYXhSYXRlagxUYXhHcm91cFJhdGViyAEQBGLDAQoHdGF4UmF0ZRoHVGF4UmF0ZUDf+IjsB0ii05nsB2IeCgJpZBoDSUQhQJrOx+wHSL2OyOwHagdUYXhSYXRlYiMKBG5hbWUaBlN0cmluZ0CKs+XsB0iz6OXsB2oHVGF4UmF0ZWIkCgdlbmREYXRlGgREYXRlQKeTgO0HSKLFgO0HagdUYXhSYXRlYioKC2Rlc2NyaXB0aW9uGgZTdHJpbmdA8LyY7QdIi+2Y7QdqB1RheFJhdGVqDFRheEdyb3VwUmF0ZWLIARAFYsMBCgd0YXhSYXRlGgdUYXhSYXRlQNKhp+wHSKiOt+wHYh4KAmlkGgNJRCFAx97V7AdI7JjW7AdqB1RheFJhdGViIwoEbmFtZRoGU3RyaW5nQNvy7uwHSOql7+wHagdUYXhSYXRlYiQKB2VuZERhdGUaBERhdGVA16OI7QdIr9WI7QdqB1RheFJhdGViKgoLZGVzY3JpcHRpb24aBlN0cmluZ0DX2qLtB0iXlqPtB2oHVGF4UmF0ZWoMVGF4R3JvdXBSYXRlaghUYXhHcm91cGoHVGF4SW5mb2InCgd0YXhhYmxlGgdCb29sZWFuQP6+0ecHSNaA0ucHagdUYXhJbmZvahhTYWxlc1RyYW5zYWN0aW9uSXRlbUxpbmVqDFNhbGVzUmVjZWlwdGL0AQoHcGF5bWVudBoLUGF5bWVudEluZm9A7JKl4gdI64XV4gdiwQEKDXBheW1lbnRNZXRob2QaDVBheW1lbnRNZXRob2RA/Mv14gdIt+qH4wdiIwoCaWQaAklEQJu1veMHSNroveMHag1QYXltZW50TWV0aG9kYikKBG5hbWUaBlN0cmluZ0D6iujjB0iiwOjjB2oNUGF5bWVudE1ldGhvZGI4CgR0eXBlGhVQYXltZW50TWV0aG9kVHlwZUVudW1A5/+I5AdI5LGJ5AdqDVBheW1lbnRNZXRob2RqC1BheW1lbnRJbmZvagxTYWxlc1JlY2VpcHRiXgoIbWV0YWRhdGEaCE1ldGFkYXRhQNjQ2eEHSIDn/eIHYi4KDWVudGl0eVZlcnNpb24aB1N0cmluZyFAiJCv4wdI5b6v4wdqCE1ldGFkYXRhagxTYWxlc1JlY2VpcHRqCE11dGF0aW9u"
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
#### fix later
{
  "data": {
    "deleteSalesReceipt": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6860",
      "success": true
    }
  }
    "ftv1": "GgwIptXkiQYQuLfutgEiDAil1eSJBhD4jezYA1jRiu26AXKfAWKcAQoSZGVsZXRlU2FsZXNSZWNlaXB0GhJEZWxldGVFbnRpdHlSZXN1bHRA4LePA0jMja+5AWIoCgJpZBoCSURAwMWXugFInc6YugFqEkRlbGV0ZUVudGl0eVJlc3VsdGIzCgdzdWNjZXNzGghCb29sZWFuIUDhw+O6AUihjeS6AWoSRGVsZXRlRW50aXR5UmVzdWx0aghNdXRhdGlvbg=="
  }
}
```