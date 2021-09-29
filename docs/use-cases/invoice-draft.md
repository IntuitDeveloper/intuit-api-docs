---
layout: default
title: Invoice Draft
nav_order: 10
parent: Use Cases
---


### Invoice Draft

#### Mutation

```
mutation createInvoiceDraft($invoiceDraftDetails: InvoiceDraftInput!) {
  createInvoiceDraft(invoiceDraftDetails: $invoiceDraftDetails) {
    id
    transactionDraftStatus
  }
}
```
Variables

```
{
    "invoiceDraftDetails": {
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
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:123",
        "displayName": "HubSpot Customer"
      },
      "amount": 22.95,
      "currency": {
        "name": "USD",
        "currency": "USD",
        "exchangeRate": 1.34444
      },
      "privateMemo": "Message displayed on statement",
      "customerMemo": "Message displayed on invoice",
      "itemLines": [
        {
          "description": "2017 model, color steel",
          "amount": 22.95,
          "quantity": 1,
          "item": {
            "id" : "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjExMmRlNzQ2OTk:4"
          },
          "unitPrice": 22.95,
          "serviceDate": "2020-12-09",
          "class": {
            "id": "302300000000001842721"
          }
        },
        {
          "description": "Description only line"
        }
      ],
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
      "billingAddress": {
        "freeFormAddressLine": "1075 Space Parkway\r\nMountain View, CA 94043\r\nUS"
      },
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
      "class": {
        "id": "Misc",
        "name": "Misc"
      },
      "discount": {
        "amount": {
          "value": 10,
          "percentage": false
        },
        "applyTaxAfterDiscount": false
      },
      "dueDate": "2020-12-09",
      "term": {
        "name": "Net 30"
      }
    }
}
```


#### Query

```
{
  company{
    transactionDraft(id: "<id>") {
      ... on InvoiceDraft {
        id
        transactionDraftStatus
        invoiceDraftDetails {
       transactionDate
          dueDate
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
          term {
            id
            name
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
            unitPrice
            class 
            { 
              id 
            }  
          }
          referenceNumber
          emailDeliveryInfo {
            to
            cc
            bcc
          }
          billingAddress{
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
}
```
