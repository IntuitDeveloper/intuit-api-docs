---
layout: default
title: Journal Entry
nav_order: 13
parent: Schema Entities
---

## Journal Entry

The APIs related to the Journal entries entity allow you to manage journal entries.
You can add journal entries to move money between accounts and force balance your books in specific ways.
Use journal entries only if you understand accounting and understand debits and credits well OR if you are following the advice of your accountant.
The JournalEntry API provides support for create, read, update and delete operations.

### Operations for JournalEntry entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**
-   Use the accounting scope **[com.intuit.quickbooks.accounting]** for the authorization header 

### Sample query body

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the JournalEntry entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read an JournalEntry by Id):
```
query fetchJournalEntry($id: String!) {
  company {
    journalEntries(filter: {id: {equals: $id}}) {
      nodes {
        id
        __typename
        metadata {
          entityVersion
        }
        memo
        referenceNumber
        transactionDate
        entryLines {
          entryLineType
          sequence
          description
          amount
          account {
            id
            name
          }
          billable
          billableAmount
          payee {
            ... on Customer {
              id 
              displayName
            }
            ... on Vendor {
              id
              displayName
            }
            __typename
          }
         project {
            id
            name
            customer {
              id
              displayName
            }
            description
          }
          class {
            id
            name
          }
          markup {
            account {
              id
              name
            }
            amount
            percent
          }
          tax {
            taxAmount
            taxable
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
                  status
                  startDate
                  endDate
                }
              }
            }
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
  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:96"
}
```

Response:
``` 
{
  "data": {
    "company": {
      "journalEntries": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:96",
            "__typename": "JournalEntry",
            "metadata": {
              "entityVersion": "0"
            },
            "memo": null,
            "referenceNumber": "SomeJENumber13",
            "transactionDate": "2021-09-22",
            "entryLines": [
              {
                "entryLineType": null,
                "sequence": "0",
                "description": "test debit",
                "amount": 45.00,
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:35",
                  "name": "Depreciation"
                },
                "billable": null,
                "billableAmount": null,
                "payee": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:13",
                  "displayName": "New project - demo3",
                  "__typename": "Customer"
                },
                "project": null,
                "class": null,
                "markup": null,
                "tax": {
                  "taxAmount": null,
                  "taxable": false,
                  "taxGroup": null
                }
              },
              {
                "entryLineType": null,
                "sequence": "1",
                "description": "test credit",
                "amount": 45.00,
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:44",
                  "name": "Meals"
                },
                "billable": null,
                "billableAmount": null,
                "payee": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:9",
                  "displayName": "New project - demo",
                  "__typename": "Customer"
                },
                "project": null,
                "class": null,
                "markup": null,
                "tax": {
                  "taxAmount": null,
                  "taxable": false,
                  "taxGroup": null
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

You can choose to **query by id** (as shown above) or query for all journal entries by removing the filter.

### Create mutation
 
Mutation:
 
```
mutation createJournalEntry($input: CreateJournalEntryInput!) {
  createJournalEntry(journalEntry: $input) {
    id
    __typename
    metadata {
      entityVersion
    }
    memo
    referenceNumber
    transactionDate
    entryLines {
      entryLineType
      sequence
      description
      amount
      account {
        id
        name
      }
      billable
      billableAmount
      payee {
         ... on Customer {
            id
            displayName
         }
      }
      class {
        id
        name
      }
      markup {
        account {
          id
          name
        }
        amount
        percent
      }
      tax {
        taxAmount
        taxable
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
              status
              startDate
              endDate
            }
          }
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
    "referenceNumber": "11",
    "transactionDate": "2021-09-09",
    "memo": "some memo for journal entry",
    "entryLines": [
      {
        "entryLineType": "DEBIT",
        "description": "test debit",
        "account": {
          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:26"
        },
        "amount": "200"
      },
      {
        "entryLineType": "CREDIT",
        "description": "test credit",
        "account": {
          "id": "djQuMTo5MTMwMzUzNzIyMjc5NDA2OjUxY2VkODUzNmM:31"
        },
        "amount": "200",
        "payee": {
          "id": "35"
        },
        "project": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:28392628"
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
    "createJournalEntry": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:84",
      "__typename": "JournalEntry",
      "metadata": {
        "entityVersion": "0"
      },
      "memo": "some memo for journal entry",
      "referenceNumber": "11",
      "transactionDate": "2021-09-09",
      "entryLines": [
        {
          "entryLineType": null,
          "sequence": "0",
          "description": "test debit",
          "amount": 200.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:26",
            "name": "Sales of Product Income"
          },
          "billable": null,
          "billableAmount": null,
          "payee": null,
          "project": null,
          "class": null,
          "markup": null,
          "tax": {
            "taxAmount": null,
            "taxable": false,
            "taxGroup": null
          }
        },
        {
          "entryLineType": null,
          "sequence": "1",
          "description": "test credit",
          "amount": 200.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:31",
            "name": "Business licences"
          },
          "billable": null,
          "billableAmount": null,
          "project": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:28392628",
            "name": "Ata Bi Pro",
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:34",
              "displayName": "Tanmay B"
            },
            "description": "Test project for Transactions"
          },          
          "payee": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:35",
            "displayName": "Ata Bi Pro"
           }
          "class": null,
          "markup": null,
          "tax": {
            "taxAmount": null,
            "taxable": false,
            "taxGroup": null
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
mutation updatejournalEntry($input: UpdateJournalEntryInput!) {
  updateJournalEntry(journalEntry: $input) {
    id
    __typename
    metadata {
      entityVersion
    }
    privateMemo
    referenceNumber
    transactionDate
    entryLines {
      entryLineType
      sequence
      description
      amount
      account {
        id
        name
      }
      billable
      billableAmount
      payee {
        ... on Customer {
          id
          displayName
        }
      }
      class {
        id
        name
      }
      markup {
        account {
          id
          name
        }
        amount
        percent
      }
      tax {
        taxAmount
        taxable
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
              status
              startDate
              endDate
            }
          }
        }
      }
    }
  }
}
```

Required fields:
- id: ID of an existing JournalEntry
- metadata: you need to provide the entity version returned from a previous create/update/read operation. 

Variables:

```
{
  "input": {
    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:82",
    "metadata": {
      "entityVersion": "0"
    },
    "referenceNumber": "11",
    "transactionDate": "2021-04-09",
    "entryLines": [
      {
        "entryLineType": "DEBIT",
        "description": "test debit",
        "account": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:35"
        },
        "amount": "35"
      },
      {
        "entryLineType": "CREDIT",
        "description": "test credit",
        "account": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:13"
        },
        "amount": "35"
      }
    ]
  }
}
```

Response:
```
{
  "data": {
    "updateJournalEntry": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:82",
      "__typename": "JournalEntry",
      "metadata": {
        "entityVersion": "5"
      },
      "memo": "add test memo",
      "referenceNumber": "11",
      "transactionDate": "2021-04-09",
      "entryLines": [
        {
          "entryLineType": null,
          "sequence": "10",
          "description": "test update debit",
          "amount": 45.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:35",
            "name": "Depreciation"
          },
          "billable": null,
          "billableAmount": null,
          "customer": null,
          "class": null,
          "markup": null,
          "tax": {
            "taxAmount": null,
            "taxable": false,
            "taxGroup": null
          }
        },
        {
          "entryLineType": null,
          "sequence": "11",
          "description": "test update credit",
          "amount": 45.00,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:13",
            "name": "Inventory Asset"
          },
          "billable": null,
          "billableAmount": null,
          "customer": null,
          "class": null,
          "markup": null,
          "tax": {
            "taxAmount": null,
            "taxable": false,
            "taxGroup": null
          }
        }
      ]
    }
  }
}
```

### Delete Mutation

Mutation:

``` 
mutation deleteJournalEntry($id: ID!) {
  deleteJournalEntry(id: $id) {
    id
    success
  }  
}
```

Required fields:
- id: ID of an existing JournalEntry

Variables:
``` 
{
  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:80"
}
```

Response:
```
{
  "data": {
    "deleteJournalEntry": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:80",
      "success": true
    }
  }
}
```