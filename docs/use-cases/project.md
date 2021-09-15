---
layout: default
title: Project
nav_order: 11
parent: Use Cases
---

## Project

The APIs related to the Project entity allow you to manage and track projects.
The Project API provides support for create, read, update and delete operations.
You can also add transactions to your project by configuring the ID for the project while creating the transaction.

This page outlines - 
- The CRUD operations for Projects.
- The CRUD operations for Invoice (sales transaction) with Projects. 
- The CRUD operations for Bill (purchase transaction) with Projects.

Currently, we have added support to a few transactions so that you can configure a project ID. 
This will allow you to read back information about the project to which this transaction belongs to (if any).
These include a few transactions like - 
- Supported sales Transactions for your customers -
    - Invoice
    - Invoice payment
    - Estimate
- Supported purchase transactions for your vendors -     
    - Bill
    - Expense
    - Purchase order

### Operations for Project entity

- Read - Query (POST)
- Create - Mutation (POST)
- Update - Mutation (POST)
- Delete - Mutation (POST)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample query header

-   Content-type: **application/json**

### Sample query body

Do an [introspection query](../../graphql-concepts/introspection) to see the current schema for the InvoicePayment entity.
Here's an example query using every possible field. Remember, with GraphQL you only need to query for the data you need:

Sample query (Read all Projects):

```
query fetchProjects {
  company {
    projects{
      nodes {
        id
        name
        status
        active
        customer {
          id
          firstName
          lastName
          displayName
          phone
        }
        description
        completedDate
      }
    }
  }
}
```

Response:
``` 
{
  "data": {
    "company": {
      "projects": [
        {
          "nodes": [
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27063631",
              "name": "New project",
              "status": "IN_PROGRESS",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "firstName": "Alisha",
                "lastName": "Kamat",
                "displayName": "Alisha Kamat",
                "phone": "(123) 456-7890"
              },
              "description": "test description",
              "completedDate": null
            },
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27348352",
              "name": "MyTestProject",
              "status": "IN_PROGRESS",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:15",
                "firstName": "Harry",
                "lastName": "Potter",
                "displayName": "Harry Potter",
                "phone": "(123) 456-7890"
              },
              "description": null,
              "completedDate": null
            },
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27391835",
              "name": "SC 1 Project 3",
              "status": "IN_PROGRESS",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:15",
                "firstName": "Harry",
                "lastName": "Potter",
                "displayName": "Harry Potter",
                "phone": "(123) 456-7890"
              },
              "description": "Test project 3",
              "completedDate": null
            }
          ]
        }
      ]
    }
  }
}

```

### Filter support:

Currently, the filters supported on projects include - 
- `id` - ID for the project.
- `customerId` - ID of the customer, for whom you are creating the project. 
- `status` - Status of the project. Supported values include TODO, OPEN, IN_PROGRESS, COMPLETE, BLOCKED, CANCELLED, DELETED.

You can create a joint filter by including more than one filterable field.
For ex, to read all the projects which have status = 'IN_PROGRESS' for the customer with customerId = 'djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1', you can execute the following query - 

Sample query with filters:

```
query fetchProjects {
  company {
    projects (
      filter : {
        and : [{ 
          customerId : {equals : "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1"}},
          { status : {equals : IN_PROGRESS}
        }]
      }
    ){
      nodes {
        id
        name
        status
        active
        customer {
          id
          firstName
          lastName
          displayName
          phone
        }
        description
        completedDate
      }
    }
  }
}
``` 

Response:

```
{
  "data": {
    "company": {
      "projects": [
        {
          "nodes": [
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27063631",
              "name": "New project",
              "status": "IN_PROGRESS",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "firstName": "Alisha",
                "lastName": "Kamat",
                "displayName": "Alisha Kamat",
                "phone": "(123) 456-7890"
              },
              "description": "test description",
              "completedDate": null
            }
          ]
        }
      ]
    }
  }
}
```

### Create mutation
 
Mutation:
 
```
mutation createProject($input_0: CreateProjectInput!) {
  createProject(project: $input_0) {
    id
    name
    description
    completedDate
    status
    customer {
      id
      displayName  
      firstName
      lastName
    }
  }
}
```

Required fields:
- name: Name for the project
- description: Short description for the project's purpose
- customer.id: ID for the customer for whom you are creating this project
  
Sample Variables: 
``` 
{
	"input_0": {
		"name": "MyProject",
		"description": "My project to track progress for a customer",
		"customer": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1"
		}
	}
}
```    

Sample response:

```
{
  "data": {
    "createProject": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404",
      "name": "MyProject",
      "description": "My project to track progress for a customer",
      "completedDate": null,
      "status": "IN_PROGRESS",
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
        "displayName": "Alisha Kamat",
        "firstName": "Alisha",
        "lastName": "Kamat"
      }
    }
  }
}
```

### Update mutation

Mutation:

``` 
mutation updateProject($input_0: UpdateProjectInput!) {
  updateProject(project: $input_0) {
    id
    name
    description
    completedDate
    status
    active
    customer {
      id
      displayName
    }
  }
}
```

Required fields:
- id: ID of an existing project

Variables:

```
{
	"input_0": {
		"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27011655",
		"description": "completed Project",
		"status": "COMPLETE"
	}
}
```

Response:

```
{
  "data": {
    "updateProject": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27011655",
      "name": "MyProject",
      "description": "My project to track progress for a customer",
      "completedDate": "2021-07-21T00:09:46.546Z",
      "status": "COMPLETE",
      "active": true,
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
        "displayName": "Alisha Kamat"
      }
    }
  }
}
```

### Delete Mutation

The deleteProjects mutation takes in the ID for the project, and returns the project with active = "false".

Mutation:
``` 
mutation deleteProject($id: ID!) {
  deleteProject(id: $id) {
    id
    name
    description
    completedDate
    active
    status
    customer {
      id
      displayName    
    }
  } 
}
```

Required fields:
- id: ID of an existing project

Variables:
``` 
{
	"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404"
}
```

Response:

```
{
  "data": {
    "deleteProject": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404",
      "name":"MyProject",
      "description": "My project to track progress for a customer",
      "completedDate": null,
      "active": false,
      "status": "IN_PROGRESS",
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
        "displayName": "Alisha Kamat"
      }
    }
  }
}
```

### Operations for Invoice
- Create - Mutation (POST)
    - Create an Invoice for a Project 
- Read - Query (POST)
    - Fetch an Invoice with the details of the Project associated with the Invoice
- Update - Mutation (POST)
    - Update an Invoice created for a Project
- Delete - Mutation (POST)
    - Delete an Invoice

Note: This document shows limited fields from Invoice transaction. For the entire object, please refer to the [Invoice usecase document](./invoice.md)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample header

-   Content-type: **application/json**

### Create an Invoice (Mutation)
Sample mutation:
```
mutation createinvoice($input: CreateInvoiceInput!) {
  createInvoice(invoice: $input) {
    id
    metadata {
      entityVersion
    }
    amount
    customer {
      id
      displayName
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
    itemLines {
      sequence
      description
      amount
      quantity
      item {
        id
        name
        sku
        active            
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
      unitPrice
      account {
        id
        name
        fullyQualifiedName
      }
    }
  }
}
```
Sample variables:
```
{
  "input": {
    "project": {
	  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404"
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
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:31",
      "metadata": {
        "entityVersion": "0"
      },
      "amount": 250,       
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
        "displayName": "Alisha Kamat"
      },      
      "project": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404",
        "name": "MyProject",
        "active": true,
        "completedDate": null,
        "customer": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
          "displayName": "Alisha Kamat"
        },
        "description": "My project to track progress for a customer",
        "status": "IN_PROGRESS"
      },      
      "itemLines": [
        {
          "sequence": "1",
          "description": "some text",
          "amount": 250,
          "quantity": 5,
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4",
            "name": "Test service",
            "sku": "Some SKU",
            "active": true,
            "salesDetails": {
              "description": null,
              "incomeAccount": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
                "name": "Services",
                "fullyQualifiedName": "Services"
              },
              "price": 50
            }
          },
          "unitPrice": 50,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
            "name": "Services",
            "fullyQualifiedName": null
          }
        }
      ],
    }
  }
}
```

### Read an Invoice (Query)
Sample query:
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
        customer {
          id
          displayName         
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
        itemLines {
          sequence
          description
          amount
          quantity
          item {
            id
            name
            sku
            active            
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
          quantity
          unitPrice
          account {
            id
            name
            fullyQualifiedName
          }
        }
      }     
    }
  }
}
```
Sample variables:
```
{
	"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:31"
}
```

Sample response:
```
{
  "data": {
    "company": {
      "invoices": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:31",
            "metadata": {
              "entityVersion": "0"
            },
            "amount": 250.00,            
            "customer": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
              "displayName": "Alisha Kamat"
            },            
            "project": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404",
              "name": "MyProject",
              "active": true,
              "completedDate": null,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "displayName": "Alisha Kamat"
              },
              "description": "My project to track progress for a customer",
              "status": "IN_PROGRESS"
            },               
            "itemLines": [
              {
                "sequence": "1",
                "description": "some text",
                "amount": 250.00,
                "quantity": 5,
                "item": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4",
                  "name": "Test service",
                  "sku": "Some SKU",
                  "active": true,                  
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
                "unitPrice": 50.00,
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
                  "name": "Services",
                  "fullyQualifiedName": null
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

### Update an Invoice (Mutation)
 
Sample query:
```
mutation updateinvoice($input: UpdateInvoiceInput!) {
  updateInvoice(invoice: $input) {
    id
    metadata {
      entityVersion
    }
    amount
    customer {
      id
      displayName
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
    itemLines {
      sequence
      description
      amount
      quantity
      item {
        id
        name
        sku
        active            
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
      unitPrice
      account {
        id
        name
        fullyQualifiedName
      }
    }
  }
}

```

Sample variables:
```
{
  "input": {
    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:31",
    "metadata": {
      "entityVersion": "0"
    }
    "amount": "100",
    "project": {
	  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404"
	},		
	"itemLines": [
	  {	
		"description": "some updated text",
		"amount": 100,
		"quantity": 2,
		"item": {
		  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4"
		},
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
    "updateinvoice": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:31",
      "metadata": {
        "entityVersion": "1"
      },
      "amount": 100,       
      "customer": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
        "displayName": "Alisha Kamat"
      },      
      "project": {
        "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404",
        "name": "MyProject",
        "active": true,
        "completedDate": null,
        "customer": {
          "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
          "displayName": "Alisha Kamat"
        },
        "description": "My project to track progress for a customer",
        "status": "IN_PROGRESS"
      },      
      "itemLines": [
        {
          "sequence": "1",
		  "description": "some updated text",
          "amount": 100,
          "quantity": 2,
          "item": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjExMmRlNzQ2OTk:4",
            "name": "Test service",
            "sku": "Some SKU",
            "active": true,
            "salesDetails": {
              "description": null,
              "incomeAccount": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
                "name": "Services",
                "fullyQualifiedName": "Services"
              },
              "price": 50
            }
          },
          "unitPrice": 50,
          "account": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:5",
            "name": "Services",
            "fullyQualifiedName": null
          }
        }
      ],
    }
  }
}
```

### Delete an Invoice (Mutation)
Sample mutation:
```
mutation deleteInvoice($input: ID!) {
  deleteInvoice(id: $input){
    id
    success
  }
}
```

Sample variables:
```
{
	"input": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:31"
}
```

Sample response:
```
{
  "data": {
    "deleteInvoice": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:31",
      "success": true
    }
  }
}
```

### Operations for Bill
- Create - Mutation (POST)
    - Create a Bill for a Project 
- Read - Query (POST)
    - Fetch a Bill with the details of the Project associated with the Bil
- Update - Mutation (POST)
    - Update a Bill created for a Project
- Delete - Mutation (POST)
    - Delete a Bill

Note: This document shows limited fields from Bill transaction. For the entire object, please refer to the [Bill usecase document](./bill.md)

### Endpoints

-   For production apps:  https://public.api.intuit.com/2020-04/graphql
-   For sandbox environments and testing: https://public-e2e.api.intuit.com/2020-04/graphql

### Sample header

-   Content-type: **application/json**

### Create a Bill (Mutation)
Sample mutation:
``` 
mutation createBill($input: CreateBillInput!) {
  createBill(billDetails: $input) {
    id
    metadata {
      entityVersion
    }
    term {
      id
      name
      dueDays
      type
    }
    vendor {
      id
      displayName
    }
    accountLines {
      sequence
      description
      amount
      account {
        id
        name
      }
      customer {
        id
        displayName
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
      unitPrice
      customer {
        id
        displayName
      }
      project {
        id
        name
        description
        status
        customer {
          id
          displayName
        }
      }
    }
  }
}
```

Sample variables:
```
{
	"input": {
		"billNumber": "SomeBillNumber",
		"transactionDate": "2021-09-08",
		"dueDate": "2021-09-08",
        "term": {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjE0Yjg0YjBkZmE:2"
        },
		"vendor": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:23"
		},	
        "accountLines": [
            {
                "description": null,
                "amount": 45.00,
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:75"
                },
                "project": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404"              
                }
              }
            ],
        "itemLines": []	
	}
}
```
Sample response:
``` 
{
 "data": {
   "createBill": {
     "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:53",
     "metadata": {
       "entityVersion": "0"
     },
     "term": {
       "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjE0Yjg0YjBkZmE:2",
       "name": "Net 15",
       "dueDays": null,
       "type": null
     },
     "transactionDate": "2021-09-08",
     "dueDate": "2021-09-08",
     "billNumber": "SomeBillNumber",
     "vendor": {
       "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:23",
       "displayName": "Sheldon Cooper"
     },
     "accountLines": [
       {
         "sequence": "1",
         "description": null,
         "amount": 45.00,
         "account": {
           "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:75",
           "name": "Website ads"
         },
         "project": {
           "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404",
           "name": "MyProject",
           "active": true,
           "completedDate": null,
           "customer": {
             "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
             "displayName": "Alisha Kamat"
           },
           "description": "My project to track progress for a customer",
           "status": "IN_PROGRESS"
           }, 
         "customer": {
           "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
           "displayName": "Alisha Kamat"
         }
       }
     ],
     "itemLines": []
   }
 }
}
```

### Read a Bill (Query)
 
Sample query:
``` 
query fetchBill($id: String!) {
  company {
    bills(filter: {id: {equals: $id}}) {
      nodes {
        id
        metadata {
          entityVersion
        }
        term {
          id
          name
          dueDays
          type 
        }
        transactionDate
        dueDate
        billNumber
        vendor {
          id
          displayName
        }
        accountLines {
          sequence
          description
          amount
          account {
            id
            name
          }
          customer {
            id
            displayName
          }
        }
        itemLines {
          sequence
          description
          quantity
          customer {
            id
            displayName
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

Sample variables:
``` 
{
    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:53"
}
```

Sample response:
``` 
{
  "data": {
    "company": {
      "bills": {
        "nodes": [
          {
            "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:53",
            "metadata": {
              "entityVersion": "0"
            },
            "term": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjE0Yjg0YjBkZmE:2",
              "name": "Net 15",
              "dueDays": null,
              "type": null
            },
            "transactionDate": "2021-09-08",
            "dueDate": "2021-09-08",
            "billNumber": "SomeBillNumber",
            "vendor": {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:23",
              "displayName": "Sheldon Cooper"
            },
            "accountLines": [
              {
                "sequence": "1",
                "description": null,
                "amount": 45.00,
                "account": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:75",
                  "name": "Website ads"
                },
                "project": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404",
                  "name": "MyProject",
                  "active": true,
                  "completedDate": null,
                  "customer": {
                    "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                    "displayName": "Alisha Kamat"
                  },
                  "description": "My project to track progress for a customer",
                  "status": "IN_PROGRESS"
                  }, 
                "customer": {
                  "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                  "displayName": "Alisha Kamat"
                }
              }
            ],
            "itemLines": []
          }
        ]
      }
    }
  }
}
```

### Update a Bill (Mutation)
Sample mutation:
``` 
mutation updateBill($input: UpdateBillInput!) {
  updateBill(billDetails: $input) {
    id
    metadata {
      entityVersion
    }
    term {
      id
      name
      dueDays
      type
    }
    vendor {
      id
      displayName
    }
    accountLines {
      sequence
      description
      amount
      account {
        id
        name
      }
      customer {
        id
        displayName
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
      unitPrice
      customer {
        id
        displayName
      }
      project {
        id
        name
        description
        status
        customer {
          id
          displayName
        }
      }
    }
  }
}
```
Sample variables:
```
{
	"input": {
		"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:53",
		"metadata": {
			"entityVersion": "1"
		},
    "term": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjE0Yjg0YjBkZmE:2"
    },
		"billNumber": "UpdatedBillNumber",
		"transactionDate": "2021-08-08",
		"dueDate": "2021-08-10",
		"vendor": {
			"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:23"
		},
		"accountLines": [
			{
				"description": "update description",
				"amount": 45,
				"account": {
					"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:75"
				},
				"project": {
					"id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404"
				}
			}
		],
		"itemLines": []
	}
}
```

Sample response:
``` 
{
 "data": {
   "updateBill": {
     "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:53",
     "metadata": {
       "entityVersion": "1"
     },
     "term": {
       "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjE0Yjg0YjBkZmE:2",
       "name": "Net 15",
       "dueDays": null,
       "type": null
     },
     "transactionDate": "2021-08-08",
     "dueDate": "2021-08-10",
     "billNumber": "UpdatedBillNumber",
     "vendor": {
       "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:23",
       "displayName": "Sheldon Cooper"
     },
     "accountLines": [
       {
         "sequence": "1",
         "description": "update description",
         "amount": 45.00,
         "account": {
           "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjUxY2VkODUzNmM:75",
           "name": "Website ads"
         },
         "project": {
           "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27462404",
           "name": "MyProject",
           "active": true,
           "completedDate": null,
           "customer": {
             "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
             "displayName": "Alisha Kamat"
           },
           "description": "My project to track progress for a customer",
           "status": "IN_PROGRESS"
           }, 
         "customer": {
           "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
           "displayName": "Alisha Kamat"
         }
       }
     ],
     "itemLines": []
   }
 }
}
```

### Delete a Bill (Mutation)
Sample mutation:
```
mutation deleteBill($input: ID!) {
  deleteBill(id: $input){
    id
    success
  }
}
```

Sample variables:
```
{
	"input": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:53"
}
```

Sample response:
```
{
  "data": {
    "deleteBill": {
      "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjgwMjcxZWRkOGE:53",
      "success": true
    }
  }
}
```
