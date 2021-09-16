---
layout: default
title: VendorCredit
nav_order: 21
parent: Use Cases
---

## credit memo

The APIs related to the VendorCredit entity allow you to manage VendorCredit for your Vendors

### Operations for credit memo entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the credit memo scope **[com.intuit.quickbooks.accounting]** for the authorization header

### Sample query body

Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an credit memo by Id):
```
query fetchVendorCredit($id: String!) {
  company{
  vendorCredits (filter: {id: {equals: $id}}){
    nodes {
      id
      metadata{
   entityVersion
     }
      transactionDate
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
      class{
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
      accountLines{
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
        billableAmount
      markup {
        amount
        percent
      account{
        id
        }
     }
      customer{
          id
          displayName
        }
        class{
          id
          name
        }      
      }
      itemLines{
        sequence
        description
        quantity
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
        billable
        billableAmount
      markup {
        amount
        percent
      account{
        id
        }
     }
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
      }
    }
  }
  }
  }

```

Variables:

```
{
	"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6891"
}
```

Response:
``` 
 {
  "data": {
    "company": {
      "vendorCredits": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6891",
            "metadata": {
              "entityVersion": "0"
            },
            "transactionDate": "2021-03-12",
            "permitNumber": "SomePermitNumber",
            "location": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OmJmN2IzNDhiNzk:1",
              "name": "SomeLocation"
            },
            "currency": {
              "name": null,
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
                "billableAmount": 16.80,
                "markup": {
                  "amount": 12.00,
                  "percent": "40%",
                  "account": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:6"
                  }
                },
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
                "billableAmount": 84.38,
                "markup": {
                  "amount": 62.50,
                  "percent": "35%",
                  "account": {
                    "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:28"
                  }
                },
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

You can choose to **query by id of vendorCredit** (as shown above).

### Create mutation

Mutation:

```
mutation createVendorCredit($input: CreateVendorCreditInput!) {
  createVendorCredit(vendorCredit: $input) {
    id
    metadata{
   entityVersion
     }
     transactionDate
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
      billableAmount
      markup {
        amount
        percent
      account{
        id
        }
     }
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
      billableAmount
      markup {
        amount
        percent
      account{
        id
        }
     }
      
    }
    
  }
  }


```

Sample Variables:
``` 
{
	"input": {
		"transactionDate": "2021-03-12",
		"permitNumber": "SomePermitNumber",
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
			"freeFormAddressLine": "2535 Garcia Avenue, Mountain View CA 94043"
		},
		"location": {
			"id": "1"
		},
		"customFields": [
			{
				"fieldId": "djQ6OTEzMDM1MzcyMjI3OTQwNjovY29tbW9uL0N1c3RvbUZpZWxkRGVmaW5pdGlvbjo:302300000000000060446",
				"value": "text cf value"
			}
		],
		"accountLines": [
			{
				"description": "Some Account description",
				"amount": "12",
				"account": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:6"
				},
				"tax": {
					"taxable": true
				},
				"billable": true,
				"markup": {
					"percent": "40%"
				},
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
				"description": "Some item description",
				"item": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:4"
				},
				"tax": {
					"taxable": true
				},
				"unitPrice": "12.5",
				"customer": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:1"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
				},
				"quantity": "5",
				"billable": true,
				"markup": {
					"percent": "35%"
				},
				"amount": "62.5"
			}
		]
	}
}
```    

Sample response:
```
{
  "data": {
    "createVendorCredit": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6891",
      "metadata": {
        "entityVersion": "0"
      },
      "transactionDate": "2021-03-12",
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
          "billableAmount": 16.80,
          "markup": {
            "amount": 12.00,
            "percent": "40%",
            "account": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:6"
            }
          },
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
          "billable": true,
          "billableAmount": 84.38,
          "markup": {
            "amount": 62.50,
            "percent": "35%",
            "account": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:28"
            }
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
mutation updateVendorCredit($input: UpdateVendorCreditInput!) {
  updateVendorCredit(vendorCredit: $input) {
    id
    metadata{
   entityVersion
     }
     transactionDate
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
      billableAmount
      markup {
        amount
        percent
      account{
        id
        }
     }
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
      billableAmount
      markup {
        amount
        percent
      account{
        id
        }
     }
      
    }
    
  }
  }


```

Required fields:
- id: ID of an existing vendorCredit
- metadata: you need to provide the entity version returned from a previous create/update/read operation.
- the entity version must match with the last entity version
  Variables:

```
{
	"input": {
		"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6891",
		"metadata": {
			"entityVersion": "0"
		},
		"transactionDate": "2021-03-12",
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
				"markup": {
					"percent": "40%"
				},
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
				"markup": {
					"percent": "35%"
				},
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
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjlkNjk5ZTk2MDg:0020714ef993c9ed524b0994946be3c4932ff0"
				},
				"class": {
					"id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjIyYzE1MDQ2NzU:302300000000001849620"
				},
				"quantity": "5",
				"billable": false,
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
    "updateVendorCredit": {
      "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjgwMjcxZWRkOGE:6891",
      "metadata": {
        "entityVersion": "1"
      },
      "transactionDate": "2021-03-12",
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
          "billableAmount": 16.80,
          "markup": {
            "amount": 12.00,
            "percent": "40%",
            "account": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:6"
            }
          },
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
          "billable": true,
          "billableAmount": 81.00,
          "markup": {
            "amount": 60.00,
            "percent": "35%",
            "account": {
              "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:28"
            }
          }
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
          "billable": null,
          "billableAmount": null,
          "markup": null
        }
      ]
    }
  }
}
```
### Delete Mutation

Mutation:

``` 
mutation deleteVendorCredit($input : ID!){
  deleteSalesReceipt(id: $input) 
  {
    id
    success
  }
}
```

Required fields:
- id: ID of an existing vendorCredit

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
```