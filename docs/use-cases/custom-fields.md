---
layout: default
title: Custom Fields
nav_order: 5
parent: Use Cases
---


## Custom Fields 

Custom fields could be business-specific fields that can be optionally configured. 
For QuickBooks Online Simple Start, Plus, and Essentials, 3 custom fields can be defined and set.
For QuickBooks Advance, upto 12 custom fields can be configured.

Currently, QuickBooks Advance use case supports creating custom fields of type Alphanumeric/Numeric/Date/Dropdown.
The API supports reading/writing their string representation.
This page describes how to configure/read these fields, and their values for transactional entities like Invoice Draft, Sales Receipt Draft, and Estimate Draft.
Along with that, this page outlines the API for reading all the defined custom fields for a company.

### Query for reading all fields defined for a company

```
query {
  customFields {
    id
    name
    inactive
    associatedEntityTypes {
      type 
      subtype
    }
    __typename
    ... on TextField {
      allowedValues {
        value
        id
        inactive
      }
    }
  }
 }
```
For dropdown type of custom fields, the list of allowedValues is defined so that when the field takes a value, it has to be one of the allowed set.

### Query for reading a field by ID

Similar filters can be applied to read based on name, inactive status

```
query {
  customFields (filter: {id: {equals: "CUSTOM_FIELD_ID"}}){
    id
    name
    inactive
    associatedEntityTypes {
      type 
      subtype
    }
    __typename
    ... on TextField {
      allowedValues {
        value
        id
        inactive
        
      }
    }
  }
 }
```

### Mutation for defining value of field within an Invoice Draft

**Note**  
The following mutation shows just the fields required for creating the custom fields object within an Invoice Draft. For all the necessary field for creating an Invoice Draft, refer to the documentation for Invoice Draft.   

```
mutation createInvoiceDraft($invoiceDraftDetails: InvoiceDraftInput!) {
  createInvoiceDraft(invoiceDraftDetails: $invoiceDraftDetails) {
    id
    customFields { 
      value
      fieldId
      fieldName
    }
  }
}
```

### Variables
**Note**  
The following JSON has just the fields required for custom fields object, for all the necessary variables for an Invoice Draft, refer to the documentation for Invoice Draft.

```
{
  "invoiceDraftDetails": {
    "customFields": [
      {
        "fieldName": "field1",
        "fieldId": "id-string-1",
        "value": "text 123"
      },
      {
        "fieldName": "field2",
        "fieldId": "id-string-2",
        "value": "test"
      },
      {
        "fieldName": "dateField",
        "fieldId": "id-string-3",
        "value": "2021-01-01T15:15:15.796Z"
      },
      {
        "fieldName": "dropdown",
        "fieldId": "id-string-4",
        "value": "dropdown-allowed-value-id"
      }
    ]
}
```

### Query for reading custom fields within an Invoice Draft 

This query retrieves the **string representation** of the values taken by each defined custom field for the Draft Invoice.
Similar query can be executed for a Sales Receipt Draft or an Estimate Draft.
```
{
  transactionDraft(id: "invoice-id-string") {
    ... on InvoiceDraft {
      id
      customFields {
        fieldId
        fieldName
        value
        fieldDefinition {
          name
          id
          inactive
          __typename
          associatedEntityTypes{
            type
            subtype
          }
         
          ... on TextField {
            allowedValues {
              value
              id
            }
          }
        }
      }
    }
  }
}
```

