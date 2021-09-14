---
layout: default
title: creditMemo
nav_order: 2
parent: Use Cases
---

## Invoice

The APIs related to the creditMemo entity allow you to manage creditMemos for your customer to track accomplished payments.
The creditMemo API provides support for create, read, update and delete operations.

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
query fetchCreditMemo($id: String!) {
  company{
  creditMemos(filter: {id: { equals: $id}}) {
      nodes {
        id
        customFields {
          fieldId
          value
          fieldName
          fieldDefinition {
            id
            name
            inactive
            associatedEntityTypes {
              type
              subtype
            }
            
            ... on TextField {
              allowedValues {
                id
                value
                inactive
              }
            }
          }
        }
        transactionDate
        referenceNumber
        amount
        voided
        metadata {
          entityVersion
        }
        privateMemo
        customerMemo
      currency {
            currency
            symbol
            exchangeRate
        }
        location {
            id
            name
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
        emailDeliveryInfo {
            to
            cc
            bcc
            status
        }
        class {
            id
            name
        }
        shipping {
            shipAddress {
                freeFormAddressLine
            }
            shipFromAddress {
                freeFormAddressLine
            }
            shipDate
            shipVia
            trackingNumber
            shippingAmount
        }
        discount {
            amount {
                percentage
                value
            }
            applyTaxAfterDiscount
        }
        tax {
            totalTaxAmount
            taxDetails {
                taxRate {
                    id
                    name
                    description
                    rate
                    status
                    startDate
                    endDate
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
                    rate
                    description
                    status
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
                        status
                        startDate
                        endDate
                        }
                }
            }
            taxable
        }
        itemLines {
            sequence
            description
            amount
            class {
                id
                name
            }
            item {
                id
                name
              sku
              }
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
                        rate
                        description
                        status
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
                            status
                            startDate
                            endDate
                            }
                    }
                }
                taxable
            }
            serviceDate
            quantity
            unitPrice
            account {
                id
               name
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
      "creditMemos": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6890",
            "customFields": [
              {
                "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
                "value": "text cf value",
                "fieldName": "Sales Rep",
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
                  ],
                  "allowedValues": []
                }
              },
              {
                "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000061217",
                "value": null,
                "fieldName": "Test SR CF",
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
                  ],
                  "allowedValues": []
                }
              }
            ],
            "transactionDate": "2021-03-30",
            "referenceNumber": null,
            "amount": 1029.00,
            "voided": false,
            "metadata": {
              "entityVersion": "0"
            },
            "privateMemo": "Test Private Memo",
            "customerMemo": "Hello Test Customer!",
            "currency": {
              "currency": "USD",
              "symbol": "$",
              "exchangeRate": 1.00
            },
            "location": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
              "name": "SomeLocation"
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
              "freeFormAddressLine": "Saurabh Jaiswal, 2600 Marine Way, Mountain View, CA 94043\r\n"
            },
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
            "class": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
              "name": "SomeClass"
            },
            "shipping": {
              "shipAddress": {
                "freeFormAddressLine": "Saurabh Jaiswal, 2600 Marine Way, Mountain View, CA 94043\r\n"
              },
              "shipFromAddress": {
                "freeFormAddressLine": "Saurabh Jaiswal, 2500 Marine Way, Mountain View, CA 94043\r\n"
              },
              "shipDate": "2021-01-25",
              "shipVia": "Fedex",
              "trackingNumber": "12345",
              "shippingAmount": 23.00
            },
            "discount": {
              "amount": {
                "percentage": false,
                "value": -4.00
              },
              "applyTaxAfterDiscount": null
            },
            "tax": {
              "totalTaxAmount": 10.00,
              "taxDetails": [
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                    "name": "California State",
                    "description": "Sales Tax",
                    "rate": "6.25%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  },
                  "taxAmount": 0.00,
                  "taxableAmount": 0.00
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                    "name": "California, Santa Clara County",
                    "description": "Sales Tax",
                    "rate": "1%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  },
                  "taxAmount": 1.11,
                  "taxableAmount": 1000.00
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                    "name": "California, Santa Clara County District",
                    "description": "Sales Tax",
                    "rate": "1.75%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  },
                  "taxAmount": 1.95,
                  "taxableAmount": 1000.00
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                    "name": "California, Santa Clara County",
                    "description": "Sales Tax",
                    "rate": "1%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  },
                  "taxAmount": 0.00,
                  "taxableAmount": 0.00
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                    "name": "California, Santa Clara County District",
                    "description": "Sales Tax",
                    "rate": "1.75%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  },
                  "taxAmount": 0.00,
                  "taxableAmount": 0.00
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
                    "name": "California State",
                    "description": "Sales Tax",
                    "rate": "6.25%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  },
                  "taxAmount": 6.94,
                  "taxableAmount": 1000.00
                }
              ],
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
                      "rate": "6.25%",
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "endDate": null
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                      "name": "California, Santa Clara County",
                      "rate": "1%",
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "endDate": null
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                      "name": "California, Santa Clara County District",
                      "rate": "1.75%",
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "endDate": null
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                      "name": "California State",
                      "rate": "6.25%",
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "endDate": null
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                      "name": "California, Santa Clara County",
                      "rate": "1%",
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "endDate": null
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                      "name": "California, Santa Clara County District",
                      "rate": "1.75%",
                      "description": "Sales Tax",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "endDate": null
                    }
                  }
                ],
                "purchaseRates": []
              },
              "taxable": null
            },
            "itemLines": [
              {
                "sequence": "1",
                "description": "Landscaping work",
                "amount": 1000.00,
                "class": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
                  "name": "SomeClass"
                },
                "item": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:6",
                  "name": "Landscaping",
                  "sku": "44-55-66"
                },
                "tax": {
                  "taxAmount": 10.00,
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
                          "rate": "6.25%",
                          "description": "Sales Tax",
                          "status": "ACTIVE",
                          "startDate": "1970-01-01",
                          "endDate": null
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                          "name": "California, Santa Clara County",
                          "rate": "1%",
                          "description": "Sales Tax",
                          "status": "ACTIVE",
                          "startDate": "1970-01-01",
                          "endDate": null
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                          "name": "California, Santa Clara County District",
                          "rate": "1.75%",
                          "description": "Sales Tax",
                          "status": "ACTIVE",
                          "startDate": "1970-01-01",
                          "endDate": null
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                          "name": "California State",
                          "rate": "6.25%",
                          "description": "Sales Tax",
                          "status": "ACTIVE",
                          "startDate": "1970-01-01",
                          "endDate": null
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                          "name": "California, Santa Clara County",
                          "rate": "1%",
                          "description": "Sales Tax",
                          "status": "ACTIVE",
                          "startDate": "1970-01-01",
                          "endDate": null
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                          "name": "California, Santa Clara County District",
                          "rate": "1.75%",
                          "description": "Sales Tax",
                          "status": "ACTIVE",
                          "startDate": "1970-01-01",
                          "endDate": null
                        }
                      }
                    ],
                    "purchaseRates": []
                  },
                  "taxable": true
                },
                "serviceDate": "2021-03-29",
                "quantity": 1,
                "unitPrice": 1000.00,
                "account": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:5",
                  "name": "Sales"
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

You can choose to **query by id of creditMemo** (as shown above).

### Create mutation

Mutation:

```
mutation createCreditMemo($input : CreateCreditMemoInput!){
  createCreditMemo(creditMemo: $input) {
        id
        customFields {
          fieldId
          value
          fieldName
          fieldDefinition {
            id
            name
            inactive
            associatedEntityTypes {
              type
              subtype
            }
            
            ... on TextField {
              allowedValues {
                id
                value
                inactive
              }
            }
          }
        }
        transactionDate
        referenceNumber
        amount
        voided
        metadata {
          entityVersion
        }
        privateMemo
        customerMemo
      currency {
            currency
            symbol
            exchangeRate
        }
        location {
            id
            name
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
        emailDeliveryInfo {
            to
            cc
            bcc
            status
        }
        class {
            id
            name
        }
        shipping {
            shipAddress {
                freeFormAddressLine
            }
            shipFromAddress {
                freeFormAddressLine
            }
            shipDate
            shipVia
            trackingNumber
            shippingAmount
        }
        discount {
            amount {
                percentage
                value
            }
            applyTaxAfterDiscount
        }
        tax {
            totalTaxAmount
            taxDetails {
                taxRate {
                    id
                    name
                    description
                    rate
                    status
                    startDate
                    endDate
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
                    rate
                    description
                    status
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
                        status
                        startDate
                        endDate
                        }
                }
            }
            taxable
        }
        itemLines {
            sequence
            description
            amount
            class {
                id
                name
            }
            item {
                id
                name
             sku
           }
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
                        rate
                        description
                        status
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
                            status
                            startDate
                            endDate
                            }
                    }
                }
                taxable
            }
            serviceDate
            quantity
            unitPrice
            account {
                id
               name
            }
        }
    }
    }

```

Sample Variables:
``` 
{"input": {
      "transactionDate": "2021-03-30",
      "privateMemo": "Test Private Memo",
      "customer": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:418"
      },
      "customFields": [
      {
        "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
        "value": "text cf value",
        "fieldName": "textCF"
      }],
      "currency": {
        "name": "USD",
        "currency": "USD",
        "exchangeRate": 1
      },
      "location": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1"
      },
      "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
      },
      "customerMemo": "Hello Test Customer!",
      "itemLines": [
        {
          "description": "Landscaping work",
          "amount": 1000,
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:6"
          },
          "quantity": 1,
          "unitPrice": 1000.00,
          "serviceDate": "2021-03-29",
          "class": {
               "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"         
          },
          "account": {
               "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:5" 
          },
          "tax": {
               "totalTaxAmount": 5.15,
               "taxGroup": {
                     "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6"       
               },
               "taxable": true
          }
        }
      ],
      "billingAddress": {
        "freeFormAddressLine": "Saurabh Jaiswal, 2600 Marine Way, Mountain View, CA 94043"
      },
      "shipping": {
        "shipDate": "2021-01-25",
        "shipVia": "Fedex",
        "shipAddress": {
          "freeFormAddressLine": "Saurabh Jaiswal, 2600 Marine Way, Mountain View, CA 94043"
        },
        "shipFromAddress": {
          "freeFormAddressLine": "Saurabh Jaiswal, 2500 Marine Way, Mountain View, CA 94043"
        },
        "trackingNumber": "12345",
        "shippingAmount": 23.00
      },
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
      "discount": {
        "amount": {
          "percentage": false,
          "value": 4.00
        },
        "applyTaxAfterDiscount": false
      },
      "tax": {
            "taxable": true,
            "totalTaxAmount": 10,
            "taxGroup": { 
                "id": "djQuMTo5MTMwMzU0MTc2ODM1MDM2OjU5MjRiN2U1YjI:3"
            },
            "taxDetails": [{
                "taxAmount": 10,
                "taxableAmount": 100
            }]
        }
    }
  }
```    

Sample response:
```
{
  "data": {
    "createCreditMemo": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6890",
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
          "value": "text cf value",
          "fieldName": "Sales Rep",
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
            ],
            "allowedValues": []
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000061217",
          "value": null,
          "fieldName": "Test SR CF",
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
            ],
            "allowedValues": []
          }
        }
      ],
      "transactionDate": "2021-03-30",
      "referenceNumber": null,
      "amount": 1029.00,
      "voided": false,
      "metadata": {
        "entityVersion": "0"
      },
      "privateMemo": "Test Private Memo",
      "customerMemo": "Hello Test Customer!",
      "currency": {
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "location": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
        "name": "SomeLocation"
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
      "class": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
        "name": "SomeClass"
      },
      "shipping": {
        "shipAddress": {
          "freeFormAddressLine": "Saurabh Jaiswal, 2600 Marine Way, Mountain View, CA 94043\r\n"
        },
        "shipFromAddress": {
          "freeFormAddressLine": "Saurabh Jaiswal, 2500 Marine Way, Mountain View, CA 94043\r\n"
        },
        "shipDate": "2021-01-25",
        "shipVia": "Fedex",
        "trackingNumber": "12345",
        "shippingAmount": 23.00
      },
      "discount": {
        "amount": {
          "percentage": false,
          "value": -4.00
        },
        "applyTaxAfterDiscount": null
      },
      "tax": {
        "totalTaxAmount": 10.00,
        "taxDetails": [
          {
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
              "name": "California State",
              "description": "Sales Tax",
              "rate": "6.25%",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "endDate": null
            },
            "taxAmount": 0.00,
            "taxableAmount": 0.00
          },
          {
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
              "name": "California, Santa Clara County",
              "description": "Sales Tax",
              "rate": "1%",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "endDate": null
            },
            "taxAmount": 1.11,
            "taxableAmount": 1000.00
          },
          {
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
              "name": "California, Santa Clara County District",
              "description": "Sales Tax",
              "rate": "1.75%",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "endDate": null
            },
            "taxAmount": 1.95,
            "taxableAmount": 1000.00
          },
          {
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
              "name": "California, Santa Clara County",
              "description": "Sales Tax",
              "rate": "1%",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "endDate": null
            },
            "taxAmount": 0.00,
            "taxableAmount": 0.00
          },
          {
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
              "name": "California, Santa Clara County District",
              "description": "Sales Tax",
              "rate": "1.75%",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "endDate": null
            },
            "taxAmount": 0.00,
            "taxableAmount": 0.00
          },
          {
            "taxRate": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:11",
              "name": "California State",
              "description": "Sales Tax",
              "rate": "6.25%",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "endDate": null
            },
            "taxAmount": 6.94,
            "taxableAmount": 1000.00
          }
        ],
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
                "rate": "6.25%",
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "endDate": null
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                "name": "California, Santa Clara County",
                "rate": "1%",
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "endDate": null
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                "name": "California, Santa Clara County District",
                "rate": "1.75%",
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "endDate": null
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                "name": "California State",
                "rate": "6.25%",
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "endDate": null
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                "name": "California, Santa Clara County",
                "rate": "1%",
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "endDate": null
              }
            },
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                "name": "California, Santa Clara County District",
                "rate": "1.75%",
                "description": "Sales Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "endDate": null
              }
            }
          ],
          "purchaseRates": []
        },
        "taxable": null
      },
      "itemLines": [
        {
          "sequence": "1",
          "description": "Landscaping work",
          "amount": 1000.00,
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
          },
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:6",
            "name": "Landscaping",
            "sku": "44-55-66"
          },
          "tax": {
            "taxAmount": 10.00,
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
                    "rate": "6.25%",
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:12",
                    "name": "California, Santa Clara County",
                    "rate": "1%",
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:13",
                    "name": "California, Santa Clara County District",
                    "rate": "1.75%",
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:14",
                    "name": "California State",
                    "rate": "6.25%",
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:15",
                    "name": "California, Santa Clara County",
                    "rate": "1%",
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  }
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU1NWM4N2YzYWQ:16",
                    "name": "California, Santa Clara County District",
                    "rate": "1.75%",
                    "description": "Sales Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  }
                }
              ],
              "purchaseRates": []
            },
            "taxable": true
          },
          "serviceDate": "2021-03-29",
          "quantity": 1,
          "unitPrice": 1000.00,
          "account": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:5",
            "name": "Sales"
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
mutation updateCreditMemo($input : UpdateCreditMemoInput!){
  updateCreditMemo(creditMemo: $input) {
        id
        customFields {
          fieldId
          value
          fieldName
          fieldDefinition {
            id
            name
            inactive
            associatedEntityTypes {
              type
              subtype
            }
            
            ... on TextField {
              allowedValues {
                id
                value
                inactive
              }
            }
          }
        }
        transactionDate
        referenceNumber
        amount
        voided
        metadata {
          entityVersion
        }
        privateMemo
        customerMemo
      currency {
            currency
            symbol
            exchangeRate
        }
        location {
            id
            name
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
          emailDeliveryInfo {
            to
            cc
            bcc
            status
        }
        class {
            id
            name
        }
        shipping {
            shipAddress {
                freeFormAddressLine
            }
            shipFromAddress {
                freeFormAddressLine
            }
            shipDate
            shipVia
            trackingNumber
            shippingAmount
        }
        discount {
            amount {
                percentage
                value
            }
            applyTaxAfterDiscount
        }
        tax {
            totalTaxAmount
            taxDetails {
                taxRate {
                    id
                    name
                    description
                    rate
                    status
                    startDate
                    endDate
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
                    rate
                    description
                    status
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
                        status
                        startDate
                        endDate
                        }
                }
            }
            taxable
        }
        itemLines {
            sequence
            description
            amount
            class {
                id
                name
            }
            item {
                id
                name
             sku
            }
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
                        rate
                        description
                        status
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
                            status
                            startDate
                            endDate
                            }
                    }
                }
                taxable
            }
            serviceDate
            quantity
            unitPrice
            account {
                id
               name
            }
        }
    }
}
```

Required fields:
- id: ID of an existing creditMemo
- metadata: you need to provide the entity version returned from a previous create/update/read operation.
- the entity version must match with the last entity version
  Variables:

```
{
	"input": {
		"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6890",
		"metadata": {
			"entityVersion": "0"
		},
		"transactionDate": "2021-03-30",
		"privateMemo": "<privateMemo>",
		"customer": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:418"
		},
		"customFields": [
			{
				"fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
				"value": "text cf value",
				"fieldName": "textCF"
			}
		],
		"currency": {
			"name": "USD",
			"currency": "USD",
			"exchangeRate": 1
		},
		"location": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1"
		},
		"class": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
		},
		"customerMemo": "Hello Test Customer!",
		"itemLines": [
			{
				"sequence": "1",
				"description": "Landscaping work",
				"amount": 1000,
				"item": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:6"
				},
				"quantity": 1,
				"unitPrice": 1000,
				"serviceDate": "2021-03-29",
				"class": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
				},
				"account": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:5"
				},
				"tax": {
					"totalTaxAmount": 5.15,
					"taxGroup": {
						"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjU5MjRiN2U1YjI:6"
					},
					"taxable": true
				}
			}
		],
		"billingAddress": {
			"freeFormAddressLine": "Saurabh Jaiswal, 2600 Marine Way, Mountain View, CA 94043"
		},
		"shipping": {
			"shipDate": "2021-01-25",
			"shipVia": "Fedex",
			"shipAddress": {
				"freeFormAddressLine": "Saurabh Jaiswal, 2600 Marine Way, Mountain View, CA 94043"
			},
			"shipFromAddress": {
				"freeFormAddressLine": "Saurabh Jaiswal, 2500 Marine Way, Mountain View, CA 94043"
			},
			"trackingNumber": "12345",
			"shippingAmount": 23
		},
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
		"discount": {
			"amount": {
				"percentage": false,
				"value": 4
			},
			"applyTaxAfterDiscount": false
		},
		"tax": {
			"taxable": true,
			"totalTaxAmount": 10,
			"taxGroup": {
				"id": "djQuMTo5MTMwMzU0MTc2ODM1MDM2OjU5MjRiN2U1YjI:3"
			},
			"taxDetails": [
				{
					"taxAmount": 10,
					"taxableAmount": 100
				}
			]
		}
	}
}
```

### Delete Mutation

Mutation:

``` 
mutation deleteCreditMemo($input: ID!) {
  deleteCreditMemo(id: $input){
    id
    success
  }
}
```

Required fields:
- id: ID of an existing creditMemo

Variables:
``` 
{
	"input": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6890"
}
```

Response:
```
{
  "data": {
    "deleteCreditMemo": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6890",
      "success": true
    }
  }
}
```