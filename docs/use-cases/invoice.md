---
layout: default
title: Invoice
nav_order: 9
parent: Use Cases
---

## Invoice

The APIs related to the Invoice entity allow you to manage invoices for your customer to track pending payments. \
Invoices are issued prior to the customer sending the payment. The invoice acts as a request for payment.\
The Invoice API provides support for create, read, update and delete operations.

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
query fetchInvoice($id: String!) {
  company {
    invoices(filter: {id: {equals: $id}}) {
      nodes {
        id
        metadata {
          entityVersion
        }
        amount
        balance {
          amountPaid
          balance
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
          contactMethods {
            active
            address {
              streetAddress1
              streetAddress2
              city
              county
              state
              zipCode
              country
            }
            email
            mobile
            phone
            fax
            primary
            type
          }
        }
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
              status
            }
          }
        }
        transactionDate
        referenceNumber
        voided
        dueDate
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
        customerMemo
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
            status
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
        term {
          id
          name
          dueDays
          type
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
              status
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
        payment {
          paymentMethod {
            id
            name
            type
          }
        }
        cleared
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
	"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:2"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "invoices": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:2",
            "metadata": {
              "entityVersion": "2"
            },
            "amount": 200.00,
            "balance": {
              "amountPaid": 200.00,
              "balance": 0.00
            },
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
              "displayName": "Alisha Kamat",
              "firstName": "Alisha",
              "lastName": "Kamat",
              "companyName": "Intuit",
              "active": true,
              "notes": null,
              "website": null,
              "email": "test@intuit.com",
              "phone": "(123) 456-7890",
              "mobile": null,
              "fax": null,
              "contactMethods": [
                {
                  "active": null,
                  "address": {
                    "streetAddress1": "123 Garcia Ave",
                    "streetAddress2": null,
                    "city": "Mountain View",
                    "county": null,
                    "state": "CA",
                    "zipCode": "94043",
                    "country": "US"
                  },
                  "email": "test@intuit.com",
                  "mobile": null,
                  "phone": "(123) 456-7890",
                  "fax": null,
                  "primary": true,
                  "type": "BILLING"
                },
                {
                  "active": null,
                  "address": {
                    "streetAddress1": "123 Garcia Ave",
                    "streetAddress2": null,
                    "city": "Mountain View",
                    "county": null,
                    "state": "CA",
                    "zipCode": "94043",
                    "country": "US"
                  },
                  "email": null,
                  "mobile": null,
                  "phone": null,
                  "fax": null,
                  "primary": false,
                  "type": "SHIPPING"
                }
              ]
            },
            "billingAddress": {
              "freeFormAddressLine": "Alisha Kamat\r\nIntuit\r\n123 Garcia Ave\r\nMountain View, CA  94043 US"
            },
            "shipping": {
              "shipDate": null,
              "shipVia": null,
              "shipAddress": {
                "freeFormAddressLine": "Alisha Kamat\r\nIntuit\r\n123 Garcia Ave\r\nMountain View, CA  94043 US"
              },
              "shipFromAddress": null,
              "shippingAmount": null,
              "tax": null,
              "trackingNumber": null
            },
            "transactionDate": "2021-07-26",
            "referenceNumber": "1001",
            "voided": false,
            "dueDate": "2021-08-25",
            "status": null,
            "customFields": [
              {
                "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
                "fieldName": "Sales rep",
                "value": "302300000000000085792_1",
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
              },
              {
                "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085793",
                "fieldName": "Birthday",
                "value": "2021-07-21",
                "fieldDefinition": {
                  "id": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085793",
                  "name": "Birthday",
                  "inactive": false,
                  "associatedEntityTypes": [
                    {
                      "type": "/network/Contact",
                      "subtype": [
                        "CUSTOMER"
                      ]
                    },
                    {
                      "type": "/transactions/Transaction",
                      "subtype": [
                        "SALE_INVOICE",
                        "PURCHASE_BILL"
                      ]
                    }
                  ]
                }
              },
              {
                "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085794",
                "fieldName": "My custom field",
                "value": null,
                "fieldDefinition": {
                  "id": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085794",
                  "name": "My custom field",
                  "inactive": false,
                  "associatedEntityTypes": [
                    {
                      "type": "/transactions/Transaction",
                      "subtype": [
                        "SALE",
                        "SALE_INVOICE"
                      ]
                    }
                  ]
                }
              }
            ],
            "discount": null,
            "project": null,
            "privateMemo": null,
            "customerMemo": null,
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
              "totalTaxAmount": null,
              "taxDetails": [],
              "taxGroup": null,
              "taxable": null
            },
            "term": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjE0Yjg0YjBkZmE:3",
              "name": "Net 30",
              "dueDays": 30,
              "type": "STANDARD"
            },
            "itemLines": [
              {
                "sequence": "1",
                "description": "test description",
                "amount": 200.00,
                "quantity": 4,
                "class": null,
                "item": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4",
                  "name": "Test service",
                  "sku": "Some SKU",
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
                    "price": 50.00
                  }
                },
                "tax": {
                  "taxAmount": null,
                  "taxGroup": null,
                  "taxable": false
                },
                "serviceDate": null,
                "unitPrice": 50.00,
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
                  "name": "Services",
                  "fullyQualifiedName": null
                }
              }
            ],
            "payment": {
              "paymentMethod": null
            },
            "cleared": null
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

You can choose to **query by id** (as shown above) or query for all invoice by removing the filter.

### Create mutation
 
Mutation:
 
```
mutation createinvoice($input: CreateInvoiceInput!) {
  createInvoice(invoice: $input) {
    id
    metadata {
      entityVersion
    }
    amount
    balance {
      amountPaid
      balance
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
      contactMethods {
        active
        address {
          streetAddress1
          streetAddress2
          city
          county
          state
          zipCode
          country
        }
        email
        mobile
        phone
        fax
        primary
        type
      }
    }
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
          status
        }
      }
    }
    transactionDate
    referenceNumber
    voided
    dueDate
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
    customerMemo
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
        status
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
    term {
      id
      name
      dueDays
      type
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
          status
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
    payment {
      paymentMethod {
        id
        name
        type
      }
    }
    cleared
  }
}
```
 
Sample Variables: 
``` 
{
	"input": {
		"amount": "50",
		"billingAddress": {
			"freeFormAddressLine": "Saurabh Jaiswal, 2600 Marine Way, Mountain View, CA 94043"
		},
		"customer": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1"
		},
		"customerMemo": "",
		"customFields": {
			"fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
			"value": "302300000000000085792_1"
		},
		"dueDate": "2021-09-10",
		"emailDeliveryInfo": {
			"to": [
				"test@intuit.com"
			]
		},
		"privateMemo": "test memo",
		"referenceNumber": "103475",
		"shipping": {
			"shipDate": "2021-01-25",
			"shipVia": "Fedex",
			"shipAddress": {
				"freeFormAddressLine": "Alisha Kamat, 2600 Marine Way, Mountain View, CA 94043"
			},
			"trackingNumber": "12345",
			"shipFromAddress": {
				"freeFormAddressLine": "Alisha Kamat, 2500 Marine Way, Mountain View, CA 94043"
			}
		},
		"transactionDate": "2021-08-09",
    "term": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjE0Yjg0YjBkZmE:3",
      "name": "Net 30"
    },
    "itemLines": [
      {
        "description": "some text",
        "amount": 250,
        "quantity": 5,
        "class": null,
        "item": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4"
        },       
        "serviceDate": "2021-09-09",
        "unitPrice": 50,
        "account": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5"
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
    "createInvoice": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:32",
      "metadata": {
        "entityVersion": "0"
      },
      "amount": 250.00,
      "balance": {
        "amountPaid": null,
        "balance": 250.00
      },
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
        "displayName": "Alisha Kamat",
        "firstName": "Alisha",
        "lastName": "Kamat",
        "companyName": "Intuit",
        "active": true,
        "notes": null,
        "website": null,
        "email": "test@intuit.com",
        "phone": "(123) 456-7890",
        "mobile": null,
        "fax": null,
        "contactMethods": [
          {
            "active": null,
            "address": {
              "streetAddress1": "123 Garcia Ave",
              "streetAddress2": null,
              "city": "Mountain View",
              "county": null,
              "state": "CA",
              "zipCode": "94043",
              "country": "US"
            },
            "email": "test@intuit.com",
            "mobile": null,
            "phone": "(123) 456-7890",
            "fax": null,
            "primary": true,
            "type": "BILLING"
          },
          {
            "active": null,
            "address": {
              "streetAddress1": "123 Garcia Ave",
              "streetAddress2": null,
              "city": "Mountain View",
              "county": null,
              "state": "CA",
              "zipCode": "94043",
              "country": "US"
            },
            "email": null,
            "mobile": null,
            "phone": null,
            "fax": null,
            "primary": false,
            "type": "SHIPPING"
          }
        ]
      },
      "billingAddress": {
        "freeFormAddressLine": null
      },
      "shipping": {
        "shipDate": null,
        "shipVia": null,
        "shipAddress": {
          "freeFormAddressLine": "Alisha Kamat, 2600 Marine Way, Mountain View, CA 94043\r\n"
        },
        "shipFromAddress": {
          "freeFormAddressLine": "Alisha Kamat, 2500 Marine Way, Mountain View, CA 94043\r\n"
        },
        "shippingAmount": null,
        "tax": null,
        "trackingNumber": null
      },
      "transactionDate": "2021-08-09",
      "referenceNumber": "103475",
      "voided": false,
      "dueDate": "2021-09-10",
      "status": null,
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
          "fieldName": "Sales rep",
          "value": "302300000000000085792_1",
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
        },
        {
          "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085793",
          "fieldName": "Birthday",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085793",
            "name": "Birthday",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/network/Contact",
                "subtype": [
                  "CUSTOMER"
                ]
              },
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "PURCHASE_BILL"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085794",
          "fieldName": "My custom field",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085794",
            "name": "My custom field",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE",
                  "SALE_INVOICE"
                ]
              }
            ]
          }
        }
      ],
      "discount": null,
      "project": null,
      "privateMemo": "test memo",
      "customerMemo": null,
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
        "totalTaxAmount": null,
        "taxDetails": [],
        "taxGroup": null,
        "taxable": null
      },
      "term": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjE0Yjg0YjBkZmE:3",
        "name": "Net 30",
        "dueDays": 30,
        "type": "STANDARD"
      },
      "itemLines": [
        {
          "sequence": "1",
          "description": "some text",
          "amount": 250.00,
          "quantity": 5,
          "class": null,
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4",
            "name": "Test service",
            "sku": "Some SKU",
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
              "price": 50.00
            }
          },
          "tax": {
            "taxAmount": null,
            "taxGroup": null,
            "taxable": false
          },
          "serviceDate": "2021-09-09",
          "unitPrice": 50.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
            "name": "Services",
            "fullyQualifiedName": null
          }
        }
      ],
      "payment": {
        "paymentMethod": null
      },
      "cleared": null
    }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updateInvoice($input : UpdateInvoiceInput!){
  updateInvoice(invoice: $input) {
    id
        metadata {
          entityVersion
        }
        amount
        balance {
          amountPaid
          balance
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
          contactMethods {
            active
            address {
              streetAddress1
              streetAddress2
              city
              county
              state
              zipCode
              country
            }
            email
            mobile
            phone
            fax
            primary
            type
          }
        }
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
              status
            }
          }
        }
        transactionDate
        referenceNumber
        voided
        dueDate
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
        customerMemo
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
            status
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
        term {
          id
          name
          dueDays
          type
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
              status
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
        payment {
          paymentMethod {
            id
            name
            type
          }
        }
        cleared
  }
}
```

Required fields:
- id: ID of an existing invoice
- metadata: you need to provide the entity version returned from a previous create/update/read operation. 

Variables:

```
{
	"input": {
		"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:32",
		"metadata": {
			"entityVersion": "0"
		},
		"customFields": [
			{
				"fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085793",
				"value": "1994-04-04"
			}
		],
		"transactionDate": "2021-09-30",
		"privateMemo": "Updated memo",
		"amount": 100,
		"customer": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1"
		},
		"currency": {
			"name": "USD",
			"currency": "USD",
			"exchangeRate": 1
		},
		"customerMemo": "Hello world",
		"dueDate": "2021-09-29",
    "itemLines": [
        {
          "sequence": "1",
          "description": "some text",
          "amount": 250.00,
          "quantity": 5,
          "class": null,
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4"  
          },
          "serviceDate": "2021-09-09",
          "unitPrice": 50.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5"
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
    "updateInvoice": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:32",
      "metadata": {
        "entityVersion": "1"
      },
      "amount": 250.00,
      "balance": {
        "amountPaid": null,
        "balance": 250.00
      },
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
        "displayName": "Alisha Kamat",
        "firstName": "Alisha",
        "lastName": "Kamat",
        "companyName": "Intuit",
        "active": true,
        "notes": null,
        "website": null,
        "email": "test@intuit.com",
        "phone": "(123) 456-7890",
        "mobile": null,
        "fax": null,
        "contactMethods": [
          {
            "active": null,
            "address": {
              "streetAddress1": "123 Garcia Ave",
              "streetAddress2": null,
              "city": "Mountain View",
              "county": null,
              "state": "CA",
              "zipCode": "94043",
              "country": "US"
            },
            "email": "test@intuit.com",
            "mobile": null,
            "phone": "(123) 456-7890",
            "fax": null,
            "primary": true,
            "type": "BILLING"
          },
          {
            "active": null,
            "address": {
              "streetAddress1": "123 Garcia Ave",
              "streetAddress2": null,
              "city": "Mountain View",
              "county": null,
              "state": "CA",
              "zipCode": "94043",
              "country": "US"
            },
            "email": null,
            "mobile": null,
            "phone": null,
            "fax": null,
            "primary": false,
            "type": "SHIPPING"
          }
        ]
      },
      "billingAddress": {
        "freeFormAddressLine": null
      },
      "shipping": {
        "shipDate": null,
        "shipVia": null,
        "shipAddress": {
          "freeFormAddressLine": "Alisha Kamat, 2600 Marine Way, Mountain View, CA 94043\r\n"
        },
        "shipFromAddress": {
          "freeFormAddressLine": "Alisha Kamat, 2500 Marine Way, Mountain View, CA 94043\r\n"
        },
        "shippingAmount": null,
        "tax": null,
        "trackingNumber": null
      },
      "transactionDate": "2021-09-30",
      "referenceNumber": null,
      "voided": false,
      "dueDate": "2021-09-29",
      "status": null,
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085792",
          "fieldName": "Sales rep",
          "value": "302300000000000085792_1",
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
        },
        {
          "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085793",
          "fieldName": "Birthday",
          "value": "1994-04-04",
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085793",
            "name": "Birthday",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/network/Contact",
                "subtype": [
                  "CUSTOMER"
                ]
              },
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE_INVOICE",
                  "PURCHASE_BILL"
                ]
              }
            ]
          }
        },
        {
          "fieldId": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085794",
          "fieldName": "My custom field",
          "value": null,
          "fieldDefinition": {
            "id": "djQ6OTEzMDM1NTIwMjAyODQ2NjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000085794",
            "name": "My custom field",
            "inactive": false,
            "associatedEntityTypes": [
              {
                "type": "/transactions/Transaction",
                "subtype": [
                  "SALE",
                  "SALE_INVOICE"
                ]
              }
            ]
          }
        }
      ],
      "discount": null,
      "project": null,
      "privateMemo": "Updated memo",
      "customerMemo": "Hello world",
      "currency": {
        "currency": "USD",
        "symbol": "$",
        "exchangeRate": 1.00,
        "name": null
      },
      "location": null,
      "emailDeliveryInfo": {
        "to": [
          "null"
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
        "totalTaxAmount": null,
        "taxDetails": [],
        "taxGroup": null,
        "taxable": null
      },
      "term": null,
      "itemLines": [
        {
          "sequence": "1",
          "description": "some text",
          "amount": 250.00,
          "quantity": 5,
          "class": null,
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4",
            "name": "Test service",
            "sku": "Some SKU",
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
              "price": 50.00
            }
          },
          "tax": {
            "taxAmount": null,
            "taxGroup": null,
            "taxable": false
          },
          "serviceDate": "2021-09-09",
          "unitPrice": 50.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
            "name": "Services",
            "fullyQualifiedName": null
          }
        }
      ],
      "payment": {
        "paymentMethod": null
      },
      "cleared": null
    }
  }
}
```

### Delete Mutation

Mutation:

``` 
mutation deleteInvoice($input: ID!) {
  deleteInvoice(id: $input){
    id
    success
  }
}
```

Required fields:
- id: ID of an existing invoice

Variables:
``` 
{
	"input": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:32"
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
```