---
layout: default
title: Bill
nav_order: 1
parent: Schema Entities
---

## Bill

The APIs related to the Bill entity allow you to manage bills so that you can pay your vendors in the future.
The Bill API provides support for create, read, update and delete operations.

### Operations for Bill entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the bill scope **[com.intuit.quickbooks.accounting]** for the authorization header 

### Sample query body

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the Bill entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read a Bill by Id):
```
query fetchBill($id: String!) {
  company {
    bills(filter: {id: {equals: $id}}) {
      nodes {
        id
        metadata {
          entityVersion
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
        dueDate
        billNumber
        referenceNumber
        permitNumber
        location {
          id
          name
        }
        currency {
          name
          currency
          exchangeRate
          symbol
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
        memo
        term {
          id
          name
        }
        class {
          id
          name
        }
        mailingAddress {
          freeFormAddressLine
        }
        vendor {
          id
          firstName
          displayName
          lastName
          companyName
          notes
          website
          email
          phone
          mobile
          fax
          active
          contactMethods {
            type
            primary
            address {
              streetAddress1
              streetAddress2
              city
              state
              zipCode
              country
            }
          }
        }
        accountLines {
          sequence
          description
          amount
          account {
            id
            name
          }
          tax {
            taxable
          }
          billable
          customer {
            id
            displayName
          }
          class {
            id
            name
          }
        }
        itemLines {
          sequence
          description
          quantity
          customer {
            id
            firstName
            displayName
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
                zipCode
                state
                country
              }
            }
          }
          billable
          item {
            id
            name
            sku
          }
          amount
          unitPrice
          class {
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
	"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6494"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "bills": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6494",
            "metadata": {
              "entityVersion": "0"
            },
            "project": null,
            "transactionDate": "2021-03-12",
            "dueDate": "2021-04-11",
            "billNumber": "SomeBillNumber",
            "referenceNumber": "SomeBillNumber",
            "permitNumber": "SomePermitNumber",
            "location": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
              "name": "SomeLocation"
            },
            "currency": {
              "name": "United States Dollar",
              "currency": "USD",
              "exchangeRate": 1.00,
              "symbol": "$"
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
              }
            ],
            "memo": "Some Memo",
            "term": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjE0Yjg0YjBkZmE:3",
              "name": "Net 30"
            },
            "class": null,
            "mailingAddress": {
              "freeFormAddressLine": "2535 Garcia Avenue, Mountain View CA 94043\r\n"
            },
            "vendor": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:375",
              "firstName": "SomeFirstName",
              "displayName": "ASampleVendor",
              "lastName": "SomeLastName",
              "companyName": "SomeCompanyName",
              "notes": "Some notes",
              "website": "https://web.com",
              "email": "somevendor@intuit.com",
              "phone": "(408) 446-8848",
              "mobile": "(408) 446-8848",
              "fax": "(408) 446-8848",
              "active": true,
              "contactMethods": [
                {
                  "type": "BILLING",
                  "primary": true,
                  "address": {
                    "streetAddress1": "2535 Garcia Avenue",
                    "streetAddress2": null,
                    "city": "Mountain View",
                    "state": "CA",
                    "zipCode": "94043",
                    "country": "USA"
                  }
                }
              ]
            },
            "accountLines": [
              {
                "sequence": "2",
                "description": "Some Account description",
                "amount": 12.00,
                "account": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:6",
                  "name": "Advertising & Marketing"
                },
                "tax": {
                  "taxable": true
                },
                "billable": true,
                "customer": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
                  "displayName": "Mr. SomeFirstName SomeLastName"
                },
                "class": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
                  "name": "SomeClass"
                }
              }
            ],
            "itemLines": [
              {
                "sequence": "1",
                "description": "Some item description",
                "quantity": 5,
                "customer": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
                  "firstName": "SomeFirstName",
                  "displayName": "Mr. SomeFirstName SomeLastName",
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
                        "zipCode": "94043",
                        "state": "CA",
                        "country": "USA"
                      }
                    },
                    {
                      "type": "SHIPPING",
                      "primary": false,
                      "address": {
                        "streetAddress1": "2535 Garcia Ave",
                        "streetAddress2": null,
                        "city": "Mountain View",
                        "zipCode": "94043",
                        "state": "CA",
                        "country": "USA"
                      }
                    }
                  ]
                },
                "billable": true,
                "item": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:4",
                  "name": "SomeNewProduct",
                  "sku": "SomeSKU"
                },
                "amount": 62.50,
                "unitPrice": 12.50,
                "class": {
                  "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
                  "name": "SomeClass"
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

You can choose to **query by id** (as shown above) or query for all bills by removing the filter.

### Create mutation
 
Mutation:
 
```
mutation createBill($input: CreateBillInput!) {
  createBill(billDetails: $input) {
    id
    metadata{
   entityVersion
     }
     transactionDate
    billNumber
   referenceNumber
    dueDate
    permitNumber
    location{
      id
      name
    }
    currency{
      name
      currency
      exchangeRate
      symbol
    }
    vendor {
          id
          firstName
          displayName
          lastName
          companyName
          notes
          website
          email
          phone
          mobile
          fax
          active
          contactMethods {
            type
            primary
            address {
              streetAddress1
              streetAddress2
              city
              state
              zipCode
              country
            }
          }
        }
    mailingAddress {
      freeFormAddressLine
    }
    term {
      id
      name
      type
    }
        customFields{
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
   memo
    accountLines{
      sequence
      description
      amount
      account{
        id
        name
      }
      tax{
        taxable
      }
      billable
      customer {
        id
        displayName
      }
      class {
        id
        name
      } 
    }
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
      customer{
            id
            firstName
            displayName
            lastName
            companyName
            notes
            website
            email
            phone
            mobile
            fax
            contactMethods{
              type
              primary
              address{
                streetAddress1
                streetAddress2
                city
                zipCode
                state 
                country       
              }
            }
          }
      class {
        id
        name
      }
      billable
      
    }

  }
}

```
 
Sample Variables: 
``` 
{
    "input": {
      "billNumber": "SomeBillNumber",
      "transactionDate" : "2021-03-12",
      "dueDate" : "2021-04-11",
      "permitNumber" : "SomePermitNumber",
      "memo": "Some Memo",
      "vendor" : {
        "id" : "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:375"
      },
      "currency" : {
        "name" : "United States Dollar",
        "currency": "USD",
        "exchangeRate": 1
      },
      "mailingAddress" : {
        "freeFormAddressLine" : "2535 Garcia Avenue, Mountain View CA 94043"
      },
      "term" : {
        "id" : "3"
      },
      "location" : {
        "id" : "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1"
      },
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
          "value": "text cf value"
        }],
      "accountLines" :[
        {
          "description" : "Some Account description",
          "amount" : "12",
          "account": {
            "id" : "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:6"
          },
          "tax" : {
            "taxable": true
          },
          "billable": true,
          "customer": {
            "id" : "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1"
          },
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
          }
        }
      ],
      "itemLines" : [
        {
          "description" : "Some item description",
          "item" : {
            "id" : "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:4"
          },
          "tax" : {
            "taxable" : true
          },
          "unitPrice" : "12.5",
          "customer" : {
            "id" : "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1"
          },
          "class" : {
            "id" : "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
          },
          "quantity" : "5",
          "billable" : true,
          "amount" : "62.5"
        }
      ]
    }
  }
```    

Sample response:
```
{
  "data": {
    "createBill": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6494",
      "metadata": {
        "entityVersion": "0"
      },
      "transactionDate": "2021-03-12",
      "billNumber": "SomeBillNumber",
      "referenceNumber": null,
      "dueDate": "2021-04-11",
      "permitNumber": "SomePermitNumber",
      "location": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
        "name": "SomeLocation"
      },
      "currency": {
        "name": "United States Dollar",
        "currency": "USD",
        "exchangeRate": 1.00,
        "symbol": "$"
      },
      "vendor": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:375",
        "firstName": "SomeFirstName",
        "displayName": "ASampleVendor",
        "lastName": "SomeLastName",
        "companyName": "SomeCompanyName",
        "notes": "Some notes",
        "website": "https://web.com",
        "email": "somevendor@intuit.com",
        "phone": "(408) 446-8848",
        "mobile": "(408) 446-8848",
        "fax": "(408) 446-8848",
        "active": true,
        "contactMethods": [
          {
            "type": "BILLING",
            "primary": true,
            "address": {
              "streetAddress1": "2535 Garcia Avenue",
              "streetAddress2": null,
              "city": "Mountain View",
              "state": "CA",
              "zipCode": "94043",
              "country": "USA"
            }
          }
        ]
      },
      "mailingAddress": {
        "freeFormAddressLine": "2535 Garcia Avenue, Mountain View CA 94043\r\n"
      },
      "term": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjE0Yjg0YjBkZmE:3",
        "name": "Net 30",
        "type": "STANDARD"
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
        }
      ],
      "memo": "Some Memo",
      "accountLines": [
        {
          "sequence": "2",
          "description": "Some Account description",
          "amount": 12.00,
          "account": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:6",
            "name": "Advertising & Marketing"
          },
          "tax": {
            "taxable": true
          },
          "billable": true,
          "customer": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
            "displayName": "Mr. SomeFirstName SomeLastName"
          },
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
          }
        }
      ],
      "itemLines": [
        {
          "sequence": "1",
          "description": "Some item description",
          "amount": 62.50,
          "quantity": 5,
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:4",
            "name": "SomeNewProduct",
            "sku": "SomeSKU"
          },
          "tax": {
            "taxable": true
          },
          "unitPrice": 12.50,
          "customer": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
            "firstName": "SomeFirstName",
            "displayName": "Mr. SomeFirstName SomeLastName",
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
                  "zipCode": "94043",
                  "state": "CA",
                  "country": "USA"
                }
              },
              {
                "type": "SHIPPING",
                "primary": false,
                "address": {
                  "streetAddress1": "2535 Garcia Ave",
                  "streetAddress2": null,
                  "city": "Mountain View",
                  "zipCode": "94043",
                  "state": "CA",
                  "country": "USA"
                }
              }
            ]
          },
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
          },
          "billable": true
        }
      ]
    }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updateBill($input: UpdateBillInput!) {
  updateBill(billDetails: $input) {
    id
    metadata {
      entityVersion
    }
    transactionDate
    billNumber
    referenceNumber
    dueDate
    permitNumber
    location {
      id
      name
    }
    currency {
      name
      currency
      exchangeRate
      symbol
    }
    vendor {
      id
      firstName
      displayName
      lastName
      companyName
      notes
      website
      email
      phone
      mobile
      fax
      active
      contactMethods {
        type
        primary
        address {
          streetAddress1
          streetAddress2
          city
          state
          zipCode
          country
        }
      }
    }
    mailingAddress {
      freeFormAddressLine
    }
    term {
      id
      name
      type
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
    memo
    accountLines {
      sequence
      description
      amount
      account {
        id
        name
      }
      tax {
        taxable
      }
      billable
      customer {
        id
        displayName
      }
      class {
        id
        name
      }
    }
    itemLines {
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
      customer {
        id
        firstName
        displayName
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
            zipCode
            state
            country
          }
        }
      }
      class {
        id
        name
      }
      billable
    }
  }
}
```
Required fields:
- id: ID of an existing bill
- metadata: you need to provide the entity version returned from a previous create/update/read operation. 

Variables:
```
{
	"input": {
		"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6494",
		"metadata": {
			"entityVersion": "0"
		},
		"billNumber": "SomeUpdatedBillNumber",
		"transactionDate": "2021-03-12",
		"dueDate": "2021-04-11",
		"permitNumber": "SomeUpdatedPermitNumber",
		"memo": "Some Memo",
		"vendor": {
			"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:375"
		},
		"currency": {
			"name": "United States Dollar",
			"currency": "USD",
			"exchangeRate": 1
		},
		"mailingAddress": {
			"freeFormAddressLine": "2700 Coast Avenue, Mountain View CA 94043"
		},
		"term": {
			"id": "3"
		},
		"location": {
			"id": "1"
		},
		"customFields": [
			{
				"fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
				"value": "text cf value updated",
				"fieldName": "textCF"
			}
		],
		"accountLines": [
			{
				"sequence": "2",
				"description": "Some Updated Account description",
				"amount": "12",
				"account": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:6"
				},
				"tax": {
					"taxable": true
				},
				"billable": true,
				"customer": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
				}
			}
		],
		"itemLines": [
			{
				"sequence": "1",
				"description": "Some updated item description",
				"item": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:4"
				},
				"tax": {
					"taxable": true
				},
				"unitPrice": "12",
				"customer": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
				},
				"quantity": "5",
				"billable": true,
				"amount": "60"
			},
			{
				"description": "Some new item description ",
				"item": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:4"
				},
				"tax": {
					"taxable": true
				},
				"unitPrice": "13",
				"customer": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
				},
				"quantity": "5",
				"billable": true,
				"amount": "65"
			}
		]
	}
}
```

Response:
```
{
  "data": {
    "updateBill": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6494",
      "metadata": {
        "entityVersion": "1"
      },
      "transactionDate": "2021-03-12",
      "billNumber": "SomeUpdatedBillNumber",
      "referenceNumber": "SomeUpdatedBillNumber",
      "dueDate": "2021-04-11",
      "permitNumber": "SomeUpdatedPermitNumber",
      "location": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
        "name": "SomeLocation"
      },
      "currency": {
        "name": "United States Dollar",
        "currency": "USD",
        "exchangeRate": 1.00,
        "symbol": "$"
      },
      "vendor": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:375",
        "firstName": "SomeFirstName",
        "displayName": "ASampleVendor",
        "lastName": "SomeLastName",
        "companyName": "SomeCompanyName",
        "notes": "Some notes",
        "website": "https://web.com",
        "email": "somevendor@intuit.com",
        "phone": "(408) 446-8848",
        "mobile": "(408) 446-8848",
        "fax": "(408) 446-8848",
        "active": true,
        "contactMethods": [
          {
            "type": "BILLING",
            "primary": true,
            "address": {
              "streetAddress1": "2535 Garcia Avenue",
              "streetAddress2": null,
              "city": "Mountain View",
              "state": "CA",
              "zipCode": "94043",
              "country": "USA"
            }
          }
        ]
      },
      "mailingAddress": {
        "freeFormAddressLine": "2700 Coast Avenue, Mountain View CA 94043\r\n"
      },
      "term": {
        "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjE0Yjg0YjBkZmE:3",
        "name": "Net 30",
        "type": "STANDARD"
      },
      "customFields": [
        {
          "fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
          "fieldName": "Sales Rep",
          "value": "text cf value updated",
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
        }
      ],
      "memo": "Some Memo",
      "accountLines": [
        {
          "sequence": "2",
          "description": "Some Updated Account description",
          "amount": 12.00,
          "account": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:6",
            "name": "Advertising & Marketing"
          },
          "tax": {
            "taxable": true
          },
          "billable": true,
          "customer": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
            "displayName": "Mr. SomeFirstName SomeLastName"
          },
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
          }
        }
      ],
      "itemLines": [
        {
          "sequence": "1",
          "description": "Some updated item description",
          "amount": 60.00,
          "quantity": 5,
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:4",
            "name": "SomeNewProduct",
            "sku": "SomeSKU"
          },
          "tax": {
            "taxable": true
          },
          "unitPrice": 12.00,
          "customer": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
            "firstName": "SomeFirstName",
            "displayName": "Mr. SomeFirstName SomeLastName",
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
                  "zipCode": "94043",
                  "state": "CA",
                  "country": "USA"
                }
              },
              {
                "type": "SHIPPING",
                "primary": false,
                "address": {
                  "streetAddress1": "2535 Garcia Ave",
                  "streetAddress2": null,
                  "city": "Mountain View",
                  "zipCode": "94043",
                  "state": "CA",
                  "country": "USA"
                }
              }
            ]
          },
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
          },
          "billable": true
        },
        {
          "sequence": "3",
          "description": "Some new item description",
          "amount": 65.00,
          "quantity": 5,
          "item": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:4",
            "name": "SomeNewProduct",
            "sku": "SomeSKU"
          },
          "tax": {
            "taxable": true
          },
          "unitPrice": 13.00,
          "customer": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1",
            "firstName": "SomeFirstName",
            "displayName": "Mr. SomeFirstName SomeLastName",
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
                  "zipCode": "94043",
                  "state": "CA",
                  "country": "USA"
                }
              },
              {
                "type": "SHIPPING",
                "primary": false,
                "address": {
                  "streetAddress1": "2535 Garcia Ave",
                  "streetAddress2": null,
                  "city": "Mountain View",
                  "zipCode": "94043",
                  "state": "CA",
                  "country": "USA"
                }
              }
            ]
          },
          "class": {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620",
            "name": "SomeClass"
          },
          "billable": true
        }
      ]
    }
  }
}
```
### Delete Mutation

Mutation:

``` 
mutation deleteBill($input: ID!) {
  deleteBill(id: $input){
    id
    success
  }
}
```

Required fields:
- id: ID of an existing bill
- metadata: you need to provide the entity version returned from a previous create/update/read operation. 

Variables:
``` 
{
	"input": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6494"
}
```

Response:
```
{
  "data": {
    "deleteBill": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6494",
      "success": true
    }
  }
}
```