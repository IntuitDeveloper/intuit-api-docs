---
layout: default
title: Estimate Draft
nav_order: 4
parent: Use Cases
---


### Estimate Draft

#### Mutation

```
mutation createEstimateDraft($estimateDraftDetails: EstimateDraftInput!) {
  createEstimateDraft(estimateDraftDetails: $estimateDraftDetails) {
    id
    transactionDraftStatus
  }
}
```
Variables

```
{
	"estimateDraftDetails": {
		"externalMetadata": [
			{
				"name": "account_id",
				"value": "a-1234"
			},
			{
				"name": "deal_id",
				"value": "d-12345"
			}
		],
		"transactionDate": "2020-09-16",
		"customer": {
			"id": "123",
			"displayName": "HubSpot Customer"
		},
		"currency": {
			"name": "USD",
			"currency": "USD",
			"exchangeRate": 1.34444
		},
		"privateMemo": "Message displayed on statement",
		"customerMemo": "Message displayed on estimate",
		"itemLines": [
			{
				"description": "2017 model, color steel",
				"amount": 22.95,
				"quantity": 1,
				"item": {
					"name": "Legrand radiant 15 Amp Receptacle Decorator Outlet",
					"sku": "885WCP8"
				},
				"rate": {
					"value": 10,
					"percentage": false
				},
				"taxable": true,
				"serviceDate": "2020-12-09",
				"class": {
					"id": "302300000000001842721",
					"name": "Abcd"
				}
			},
			{
				"description": "Description only line"
			}
		],
		"expirationDate": "2020-07-20",
		"emailDeliveryInfo": {
			"to": [
				"a@to.com",
				"b@to.com"
			],
			"cc": [
				"a@cc.com",
				"b@cc.com"
			],
			"bcc": [
				"a@bcc.com",
				"b@bcc.com"
			]
		},
		"referenceNumber": "Test 123",
		"shipping": {
			"shipDate": "2020-12-25",
			"shipVia": "FedEx1234",
			"shipAddress": {
				"freeFormAddressLine": "201 S 4th St\r\nSan Jose, CA 95112\r\nUS"
			},
			"shipFromAddress": {
				"freeFormAddressLine": "2700 Coast Ave., Mountain View, CA, 94043, USA"
			},
			"trackingNumber": "1234567"
		},
		"department": {
			"id": "Dept 123",
			"name": "Dept 123"
		},
		"billingAddress": {
			"freeFormAddressLine": "1075 Space Parkway\r\nMountain View, CA 94043\r\nUS"
		},
		"acceptStatus": {
			"status": "PENDING",
			"by": "Rohit1234",
			"date": "2020-12-17"
		},
		"class": {
			"id": "Misc",
			"name": "Misc"
		},
		"discount": {
			"value": 10,
			"percentage": false
		}
	}
}
```


#### Query

```
{
  transactionDraft(id: "<id>") {
    ... on EstimateDraft {
      id
      transactionDraftStatus
      estimateDraftDetails {
        transactionDate
        expirationDate
        amount
        customer {
          id
          displayName
        }
        currency {
          name
          currency
          exchangeRate
        }
        acceptStatus {
          status
          by
          date
        }
        privateMemo
        customerMemo
        itemLines {
          sequence
          description
          serviceDate
          amount
          item {
            id
            name
            sku
          }
          quantity
          rate {
            percentage
            percentage
          }
          taxable
        }
        referenceNumber
        emailDeliveryInfo {
          to
          cc
          bcc
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
        }
        department {
          id
          name
        }
        class {
          id
          name
        }
        discount {
          percentage
          value
        }
      }
    }
  }
}


```
