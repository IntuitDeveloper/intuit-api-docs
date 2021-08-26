---
layout: default
title: Estimate
nav_order: 5
parent: Use Cases
---

## Estimate

The APIs related to the Estimate entity allow you to manage estimates for your customers.
The Estimate API provides support for create, read, update and delete operations.

### Operations for Estimate entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the estimate scope **[com.intuit.quickbooks.accounting]** for the authorization header 

### Sample query body

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the Estimate entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an Estimate by Id):
```
query fetchEstimate($id: String!) {
  company {
    estimates(filter: {id: {equals: $id}}) {
      nodes {
        id
        metadata {
          entityVersion
        }
        amount
        acceptStatus {
          status
          by
          date
        }
        customer {
          id
          displayName
          firstName
          lastName
          companyName
          active
          notes
          website
          email
          phone
          mobile
          fax
        }
        customerMemo
        billingAddress {
          freeFormAddressLine
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
          shipVia
          shippingAmount
          tax {
            taxAmount
            taxable
            taxGroup {
              id
              name
              code
              description
              purchaseRates {
                taxRate {
                  id
                  name
                  description
                  startDate
                  endDate
                  status
                  rate
                }
              }
              saleRates {
                taxRate {
                  id
                  name
                  description
                  startDate
                  endDate
                  status
                  rate
                }
              }
            }
          }
        }
        transactionDate
        expirationDate
        referenceNumber
        voided
        status
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
        discount {
          amount {
            percentage
            value
          }
          applyTaxAfterDiscount
        }
        project {
          id
          name
          active
          completedDate
          customer {
            id
            displayName
          }
          description
          status
        }
        privateMemo
        currency {
          currency
          symbol
          exchangeRate
          name
        }
        location {
          id
          name
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
          quantity
          class {
            id
            name
          }
          item {
            id
            name
            sku
            active
            category {
              id
              name
              active
              metadata {
                entityVersion
              }
              parentCategory {
                id
                name
              }
              subCategories {
                id
                name
              }
              subLevel
            }
            class {
              id
              name
            }
            purchaseDetails {
              expenseAccount {
                id
                name
                fullyQualifiedName
              }
              description
              cost
              preferredVendor {
                id
                displayName
              }
            }
            salesDetails {
              description
              incomeAccount {
                id
                name
                fullyQualifiedName
              }
              price
            }
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
            fullyQualifiedName
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
	"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:33"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "estimates": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:33",
            "metadata": {
              "entityVersion": "3"
            },
            "amount": 327.38,
            "acceptStatus": {
              "status": "PENDING",
              "by": null,
              "date": null
            },
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:18",
              "displayName": "SC 1 Project 3",
              "firstName": null,
              "lastName": null,
              "companyName": null,
              "active": true,
              "notes": null,
              "website": null,
              "email": null,
              "phone": null,
              "mobile": null,
              "fax": null
            },
            "customerMemo": "Test message on estimate",
            "billingAddress": {
              "freeFormAddressLine": "Alisha Kamat\r\nIntuit\r\n123 Garcia Ave\r\nBoston, MA  02111 US"
            },
            "shipping": {
              "shipDate": "2021-08-18",
              "shipVia": null,
              "shipAddress": {
                "freeFormAddressLine": "Alisha Kamat\r\nIntuit\r\n123 Garcia Ave\r\nBoston, MA  02111 US"
              },
              "shipFromAddress": {
                "freeFormAddressLine": "Boston, MA\r\n"
              },
              "shippingAmount": null,
              "tax": null,
              "trackingNumber": "445677"
            },
            "transactionDate": "2021-08-24",
            "expirationDate": "2021-08-31",
            "referenceNumber": "1002",
            "voided": false,
            "status": "PENDING",
            "customFields": [
              {
                "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
                "fieldName": "Sales rep",
                "value": "302300000000000085792_2",
                "fieldDefinition": {
                  "id": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
                  "name": "Sales rep",
                  "inactive": false,
                  "associatedEntityTypes": [
                    {
                      "type": "/transactions/Transaction",
                      "subtype": [
                        "SALE_INVOICE",
                        "SALE_ESTIMATE",
                        "SALE"
                      ]
                    }
                  ]
                }
              }
            ],
            "discount": null,
            "project": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27391839",
              "name": "SC 1 Project 3",
              "active": true,
              "completedDate": null,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "displayName": "Alisha Kamat"
              },
              "description": "Test project 3 for sub customer 1",
              "status": "IN_PROGRESS"
            },
            "privateMemo": "Test message on statement",
            "currency": {
              "currency": "USD",
              "symbol": "$",
              "exchangeRate": 1.00,
              "name": null
            },
            "location": null,
            "emailDeliveryInfo": {
              "to": [
                "test@intuit.com"
              ],
              "cc": [
                "null"
              ],
              "bcc": [
                "null"
              ],
              "status": "NOT_SET"
            },
            "class": null,
            "tax": {
              "totalTaxAmount": 27.38,
              "taxDetails": [
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:3",
                    "name": "California State",
                    "description": "ST",
                    "rate": "6.25%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  },
                  "taxAmount": 18.75,
                  "taxableAmount": 300.00
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:4",
                    "name": "California, Santa Clara County",
                    "description": "ST",
                    "rate": "1%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  },
                  "taxAmount": 3.00,
                  "taxableAmount": 300.00
                },
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:5",
                    "name": "California, Santa Clara County District",
                    "description": "ST",
                    "rate": "1.875%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  },
                  "taxAmount": 5.63,
                  "taxableAmount": 300.00
                }
              ],
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
                      "rate": "6.25%",
                      "description": "ST",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "endDate": null
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:4",
                      "name": "California, Santa Clara County",
                      "rate": "1%",
                      "description": "ST",
                      "status": "ACTIVE",
                      "startDate": "1970-01-01",
                      "endDate": null
                    }
                  },
                  {
                    "taxRate": {
                      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:5",
                      "name": "California, Santa Clara County District",
                      "rate": "1.875%",
                      "description": "ST",
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
                "description": "Some desc",
                "amount": 300.00,
                "quantity": 3,
                "class": null,
                "item": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:2",
                  "name": "Hours",
                  "sku": null,
                  "active": true,
                  "category": null,
                  "class": null,
                  "purchaseDetails": null,
                  "salesDetails": {
                    "description": null,
                    "incomeAccount": {
                      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
                      "name": "Services",
                      "fullyQualifiedName": "Services"
                    },
                    "price": null
                  }
                },
                "tax": {
                  "taxAmount": 27.38,
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
                          "rate": "6.25%",
                          "description": "ST",
                          "status": "ACTIVE",
                          "startDate": "1970-01-01",
                          "endDate": null
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:4",
                          "name": "California, Santa Clara County",
                          "rate": "1%",
                          "description": "ST",
                          "status": "ACTIVE",
                          "startDate": "1970-01-01",
                          "endDate": null
                        }
                      },
                      {
                        "taxRate": {
                          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:5",
                          "name": "California, Santa Clara County District",
                          "rate": "1.875%",
                          "description": "ST",
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
                "serviceDate": null,
                "unitPrice": 100.00,
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
                  "name": "Services",
                  "fullyQualifiedName": null
                }
              }
            ]
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

You can choose to **query by id** (as shown above) or query for all estimates by removing the filter.

### Create mutation
 
Mutation:
 
```
mutation createEstimate($input: CreateEstimateInput!) {
  createEstimate(estimate: $input) {
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
    project {
      id
      name
      customer {
        id
        displayName
      }
    }
    transactionDate
    referenceNumber
    amount
    voided
    status
    metadata {
      entityVersion
    }
    privateMemo
    customerMemo
    expirationDate
    currency {
      currency
      symbol
      exchangeRate
    }
    acceptStatus {
      status
      by
      date
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
{
    "input": {
      "transactionDate": "2021-08-30",
      "privateMemo": "Test Private Memo",
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:18"
      },
      "customFields": [
      {
        "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
        "value": "302300000000000085792_1",
        "fieldName": "Sales rep"
      }],    
      "currency": {
        "name": "USD",
        "currency": "USD",
        "exchangeRate": 1
      },
      "expirationDate": "2021-09-29",
      "acceptStatus": {
        "status": "PENDING",
        "date": "2021-03-30",
        "by": "Tommy"
      },
      "customerMemo": "Hello Test Customer!",
      "itemLines": [
              {
                "description": "Some desc",
                "amount": 300.00,
                "quantity": 3,
                "class": null,
                "item": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:2"
                },
                "tax": {
                  "taxGroup": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU5MjRiN2U1YjI:3"
                  },
                  "taxable": true
                },
                "serviceDate": null,
                "unitPrice": 100.00,
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5"
                }
              }
      ],
      "billingAddress": {
        "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111"
      },
      "shipping": {
        "shipDate": "2021-08-31",
        "shipVia": "Fedex",
        "shipAddress": {
          "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111"
        },
        "shipFromAddress": {
          "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111"
        },
        "trackingNumber": "12345",
        "shippingAmount": 23.00
      },
      "emailDeliveryInfo": {
              "to": [
                  "test@intuit.com"
            ],
        "cc": [
          "CCcustomerTest@customerTest.com"
        ],
        "bcc": [
          "BCCcustomerTest@customerTest.com"
        ]
      },
      "discount": {
        "amount" : {
          "percentage": false,
          "value": 4.00
        },
        "applyTaxAfterDiscount" : false
      },
      "tax": {
            "taxable": true,
            "totalTaxAmount": 10,           
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
    "createEstimate": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:35",
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
          "value": "302300000000000085792_1",
          "fieldName": "Sales rep",
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
            "name": "Sales rep",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "SALE_ESTIMATE",
                  "SALE"
                ]
              }
            ],
            "allowedValues": [
              {
                "id": "302300000000000085792_1",
                "value": "Alice",
                "inactive": false
              },
              {
                "id": "302300000000000085792_2",
                "value": "Bob",
                "inactive": false
              }
            ]
          }
        }
      ],
      "project": null,
      "transactionDate": "2021-08-30",
      "referenceNumber": null,
      "amount": 329.00,
      "voided": false,
      "status": "PENDING",
      "metadata": {
        "entityVersion": "0"
      },
      "privateMemo": "Test Private Memo",
      "customerMemo": "Hello Test Customer!",
      "expirationDate": "2021-09-29",
      "currency": {
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00
      },
      "acceptStatus": {
        "status": "PENDING",
        "by": "Tommy",
        "date": "2021-03-30"
      },
      "location": null,
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:18",
        "displayName": "SC 1 Project 3",
        "firstName": null,
        "lastName": null,
        "companyName": null,
        "notes": null,
        "website": null,
        "email": null,
        "phone": null,
        "mobile": null,
        "fax": null
      },
      "emailDeliveryInfo": {
        "to": [
          "test@intuit.com"
        ],
        "cc": [
          "CCcustomerTest@customerTest.com"
        ],
        "bcc": [
          "BCCcustomerTest@customerTest.com"
        ],
        "status": "NOT_SET"
      },
      "class": null,
      "shipping": {
        "shipAddress": {
          "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111\r\n"
        },
        "shipFromAddress": {
          "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111\r\n"
        },
        "shipDate": "2021-08-31",
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
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:2",
              "name": "NO TAX SALES",
              "description": "No Tax",
              "rate": "0%",
              "status": "ACTIVE",
              "startDate": "1970-01-01",
              "endDate": null
            },
            "taxAmount": 10.00,
            "taxableAmount": 0.00
          }
        ],
        "taxGroup": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU5MjRiN2U1YjI:2",
          "name": "OUT_OF_SCOPE",
          "code": "OUT_OF_SCOPE",
          "description": "Out of scope",
          "saleRates": [
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:2",
                "name": "NO TAX SALES",
                "rate": "0%",
                "description": "No Tax",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "endDate": null
              }
            }
          ],
          "purchaseRates": [
            {
              "taxRate": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:1",
                "name": "NO TAX PURCHASE",
                "description": "No Tax",
                "rate": "0%",
                "status": "ACTIVE",
                "startDate": "1970-01-01",
                "endDate": null
              }
            }
          ]
        },
        "taxable": null
      },
      "itemLines": [
        {
          "sequence": "1",
          "description": "Some desc",
          "amount": 300.00,
          "class": null,
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:2",
            "name": "Hours",
            "sku": null
          },
          "tax": {
            "taxAmount": 10.00,
            "taxGroup": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU5MjRiN2U1YjI:2",
              "name": "OUT_OF_SCOPE",
              "code": "OUT_OF_SCOPE",
              "description": "Out of scope",
              "saleRates": [
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:2",
                    "name": "NO TAX SALES",
                    "rate": "0%",
                    "description": "No Tax",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  }
                }
              ],
              "purchaseRates": [
                {
                  "taxRate": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:1",
                    "name": "NO TAX PURCHASE",
                    "description": "No Tax",
                    "rate": "0%",
                    "status": "ACTIVE",
                    "startDate": "1970-01-01",
                    "endDate": null
                  }
                }
              ]
            },
            "taxable": true
          },
          "serviceDate": null,
          "quantity": 3,
          "unitPrice": 100.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
            "name": "Services"
          }
        }
      ]
    }
  }
```

### Update mutation

Mutation:

``` 
mutation updateEstimate($input: UpdateEstimateInput!) {
  updateEstimate(estimate: $input) {
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
    status
    metadata {
      entityVersion
    }
    privateMemo
    customerMemo
    expirationDate
    currency {
      currency
      symbol
      exchangeRate
    }
    acceptStatus {
      status
      by
      date
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

Variables:

```
{
"input": {
    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:35",
    "metadata": {
        "entityVersion": "1"
    },
    "transactionDate": "2021-08-30",
    "privateMemo": "Updated Test Private Memo",
    "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:18"
    },
    "customFields": [
        {
            "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
            "value": "302300000000000085792_2",
            "fieldName": "Sales rep"
        }
    ],
    "currency": {
        "name": "USD",
        "currency": "USD",
        "exchangeRate": 1
    },
    "expirationDate": "2021-09-29",
    "acceptStatus": {
        "status": "PENDING",
        "date": "2021-03-30",
        "by": "Tommy"
    },
    "customerMemo": "Hello Test Customer!",
    "itemLines": [
        {
            "description": "Some desc",
            "amount": 300,
            "quantity": 3,
            "item": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:2"
            },
            "tax": {
                "taxGroup": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU5MjRiN2U1YjI:3"
                },
                "taxable": true
            },
            "serviceDate": null,
            "unitPrice": 100,
            "account": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5"
            }
        }
    ],
    "billingAddress": {
        "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111"
    },
    "shipping": {
        "shipDate": "2021-08-31",
        "shipVia": "Fedex",
        "shipAddress": {
            "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111"
        },
        "shipFromAddress": {
            "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111"
        },
        "trackingNumber": "12345",
        "shippingAmount": 23
    },
    "emailDeliveryInfo": {
        "to": [
            "test@intuit.com"
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

Response:
```
{
 "data": {
   "updateEstimate": {
     "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:35",
     "customFields": [
       {
         "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
         "value": "302300000000000085792_2",
         "fieldName": "Sales rep",
         "fieldDefinition": {
           "id": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
           "name": "Sales rep",
           "inactive": false,
           "associatedEntityTypes": [
             {
               "type": "/transactions/Transaction",
               "subtype": [
                 "SALE_INVOICE",
                 "SALE_ESTIMATE",
                 "SALE"
               ]
             }
           ],
           "allowedValues": [
             {
               "id": "302300000000000085792_1",
               "value": "Alice",
               "inactive": false
             },
             {
               "id": "302300000000000085792_2",
               "value": "Bob",
               "inactive": false
             }
           ]
         }
       }
     ],
     "transactionDate": "2021-08-30",
     "referenceNumber": null,
     "amount": 329.00,
     "voided": false,
     "status": "PENDING",
     "metadata": {
       "entityVersion": "2"
     },
     "privateMemo": "Updated Test Private Memo",
     "customerMemo": "Hello Test Customer!",
     "expirationDate": "2021-09-29",
     "currency": {
       "currency": "USD",
       "symbol": "$",
       "exchangeRate": 1.00
     },
     "acceptStatus": {
       "status": "PENDING",
       "by": "Tommy",
       "date": "2021-03-30"
     },
     "location": null,
     "customer": {
       "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:18",
       "displayName": "SC 1 Project 3",
       "firstName": null,
       "lastName": null,
       "companyName": null,
       "notes": null,
       "website": null,
       "email": null,
       "phone": null,
       "mobile": null,
       "fax": null
     },
     "emailDeliveryInfo": {
       "to": [
         "test@intuit.com"
       ],
       "cc": [
         "CCcustomerTest@customerTest.com"
       ],
       "bcc": [
         "BCCcustomerTest@customerTest.com"
       ],
       "status": "NOT_SET"
     },
     "class": null,
     "shipping": {
       "shipAddress": {
         "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111\r\n"
       },
       "shipFromAddress": {
         "freeFormAddressLine": "Alisha Kamat, 123 Garcia Ave, Boston, MA 02111\r\n"
       },
       "shipDate": "2021-08-31",
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
             "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:2",
             "name": "NO TAX SALES",
             "description": "No Tax",
             "rate": "0%",
             "status": "ACTIVE",
             "startDate": "1970-01-01",
             "endDate": null
           },
           "taxAmount": 10.00,
           "taxableAmount": 0.00
         }
       ],
       "taxGroup": {
         "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU5MjRiN2U1YjI:2",
         "name": "OUT_OF_SCOPE",
         "code": "OUT_OF_SCOPE",
         "description": "Out of scope",
         "saleRates": [
           {
             "taxRate": {
               "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:2",
               "name": "NO TAX SALES",
               "rate": "0%",
               "description": "No Tax",
               "status": "ACTIVE",
               "startDate": "1970-01-01",
               "endDate": null
             }
           }
         ],
         "purchaseRates": [
           {
             "taxRate": {
               "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:1",
               "name": "NO TAX PURCHASE",
               "description": "No Tax",
               "rate": "0%",
               "status": "ACTIVE",
               "startDate": "1970-01-01",
               "endDate": null
             }
           }
         ]
       },
       "taxable": null
     },
     "itemLines": [
       {
         "sequence": "6",
         "description": "Some desc",
         "amount": 300.00,
         "class": null,
         "item": {
           "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:2",
           "name": "Hours",
           "sku": null
         },
         "tax": {
           "taxAmount": 10.00,
           "taxGroup": {
             "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU5MjRiN2U1YjI:2",
             "name": "OUT_OF_SCOPE",
             "code": "OUT_OF_SCOPE",
             "description": "Out of scope",
             "saleRates": [
               {
                 "taxRate": {
                   "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:2",
                   "name": "NO TAX SALES",
                   "rate": "0%",
                   "description": "No Tax",
                   "status": "ACTIVE",
                   "startDate": "1970-01-01",
                   "endDate": null
                 }
               }
             ],
             "purchaseRates": [
               {
                 "taxRate": {
                   "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjU1NWM4N2YzYWQ:1",
                   "name": "NO TAX PURCHASE",
                   "description": "No Tax",
                   "rate": "0%",
                   "status": "ACTIVE",
                   "startDate": "1970-01-01",
                   "endDate": null
                 }
               }
             ]
           },
           "taxable": true
         },
         "serviceDate": null,
         "quantity": 3,
         "unitPrice": 100.00,
         "account": {
           "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
           "name": "Services"
         }
       }
     ]
   }
 }
```
### Delete Mutation

Mutation:

``` 
mutation deleteEstimate($input: ID!) {
  deleteEstimate(id: $input){
    id
    success
  }
}
```

Variables:
``` 
{
	"input": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:35"
}
```

Response:
```
{
  "data": {
    "deleteEstimate": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:35",
      "success": true
    }
  }
}
```