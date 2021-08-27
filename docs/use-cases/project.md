---
layout: default
title: Project
nav_order: 5
parent: Use Cases
---

## Project

The APIs related to the Project entity allow you to manage and track projects.
The Project API provides support for create, read, update and delete operations.
You can also add transactions to your project by configuring the ID for the project while creating 
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
-   Scopes: TBD

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
              "name": "New project - demo3",
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
              "name": "Test_01",
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
              "description": "Test project 3 for sub customer 1",
              "completedDate": null
            },
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27391839",
              "name": "SC 1 Project 3",
              "status": "IN_PROGRESS",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "firstName": "Alisha",
                "lastName": "Kamat",
                "displayName": "Alisha Kamat",
                "phone": "(123) 456-7890"
              },
              "description": "Test project 3 for sub customer 1",
              "completedDate": null
            },
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27463492",
              "name": "Test_complete",
              "status": "COMPLETE",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "firstName": "Alisha",
                "lastName": "Kamat",
                "displayName": "Alisha Kamat",
                "phone": "(123) 456-7890"
              },
              "description": "Test project for complete status",
              "completedDate": "2021-07-27T23:08:54.875Z"
            },
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27565069",
              "name": "test_project_123",
              "status": "IN_PROGRESS",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "firstName": "Alisha",
                "lastName": "Kamat",
                "displayName": "Alisha Kamat",
                "phone": "(123) 456-7890"
              },
              "description": null,
              "completedDate": null
            },
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27873739",
              "name": "My project",
              "status": "IN_PROGRESS",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:15",
                "firstName": "Harry",
                "lastName": "Potter",
                "displayName": "Harry Potter",
                "phone": "(123) 456-7890"
              },
              "description": "Test project for HP",
              "completedDate": null
            }
          ]
        }
      ]
    }
  }
}

```

## Filter support:

Currently, the filters supported on projects include - 
- id - ID for the project.
- customerId - ID of the customer, for whom you are creating the project. 
- status - Status of the project. Supported values include TODO, OPEN, IN_PROGRESS, COMPLETE, BLOCKED, CANCELLED, DELETED.

You can create a joint filter by including more than one filterable field.
For ex, to read all the projects which have status = 'IN_PROGRESS' for the customer with customerId = '', you can execute the following query - 

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
              "name": "New project - demo3",
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
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27391839",
              "name": "SC 1 Project 3",
              "status": "IN_PROGRESS",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "firstName": "Alisha",
                "lastName": "Kamat",
                "displayName": "Alisha Kamat",
                "phone": "(123) 456-7890"
              },
              "description": "Test project 3 for sub customer 1",
              "completedDate": null
            },
            {
              "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjY4ZDAxMTQ3ZGQ:27565069",
              "name": "test_project_123",
              "status": "IN_PROGRESS",
              "active": true,
              "customer": {
                "id": "djQuMTo5MTMwMzU1MjAyMDI4NDY2OjlkNjk5ZTk2MDg:1",
                "firstName": "Alisha",
                "lastName": "Kamat",
                "displayName": "Alisha Kamat",
                "phone": "(123) 456-7890"
              },
              "description": null,
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
		"description": "My project to track progress for xyz customer",
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
      "description": "My project to track progress for xyz customer",
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
      "description": "My project to track progress for xyz customer",
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
      "description": "My project to track progress for xyz customer",
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