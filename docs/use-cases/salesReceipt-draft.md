---
layout: default
title: Sales Receipt Draft
nav_order: 7
parent: Use Cases
---

### Sales Receipt Draft

#### Mutation

```
mutation createSalesReceiptDraft($salesReceiptDraftDetails: SalesReceiptDraftInput!) {
  createSalesReceiptDraft(salesReceiptDraftDetails: $salesReceiptDraftDetails) {
    id
    transactionDraftStatus
  }
}
```
Variables

```
{
    "salesReceiptDraftDetails": {
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
        "id": "djQuMTo5MTMwMzUyMzI1NzU4Mjk2OjlkNjk5ZTk2MDg:123"
      },
      "amount": 22.95,
      "currency": {
        "name": "USD",
        "currency": "USD",
        "exchangeRate": 1.34444
      },
      "privateMemo": "Message displayed on statement",
      "customerMemo": "Message displayed on sales receipt",
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
      "referenceNumber": "SomeReferenceNumber",
      "shipping": {
        "shipDate": "2020-12-25",
        "shipVia": "FedEx1234",
        "shipAddress": {
          "freeFormAddressLine": "201 S 4th St\r\nSan Jose, CA 95112\r\nUS"
        },
        "shipFromAddress": {
          "freeFormAddressLine": "2700 Coast Ave., Mountain View, CA, 94043, USA"
        },
        "trackingNumber": "SomeTrackingNumber"
      },
      "department": {
        "id": "1",
        "name": "SomeDepartment"
      },
      "billingAddress": {
        "freeFormAddressLine": "1075 Space Parkway\r\nMountain View, CA 94043\r\nUS"
      },
      "class": {
        "id": "302300000000001842721",
        "name": "Abcd"
      },
      "account": {
        "id": "123",
        "name": "Undeposited Funds"
      },
      "payment": {
        "paymentMethod": {
          "type": "CASH",
          "name": "Cash"
        }
      },
      "discount": {
        "amount": {
          "value": 10,
          "percentage": false
        },
        "applyTaxAfterDiscount": false
      }
    }
}
```


#### Query

```
{
  company{
    transactionDraft(id: "<id>") {
      ... on SalesReceiptDraft {
        id
        transactionDraftStatus
        salesReceiptDraftDetails {
          transactionDate
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
          privateMemo
          customerMemo
          itemLines {
            sequence
            description
            amount
            serviceDate
            item {
              id
              name
              sku
            }
            quantity
            unitPrice
            class {
              id 
            } 
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
          billingAddress {
            freeFormAddressLine
          }
          department {
            id
            name
          }
          class {
            id
            name
          }
          payment {
            paymentMethod {
              id
              name
              type
            }
          }
          account {
            id
            name
            fullyQualifiedName
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
