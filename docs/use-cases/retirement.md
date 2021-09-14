---
layout: default
title: Retirement
nav_order: 15
parent: Use Cases
---

# Build retirement benefits apps

As a retirement benefit provider, you can build retirement benefits apps that let small businesses connect their QuickBooks Online Payroll (not Intuit Payroll) data. This data tells you each employee's eligibility - use it to decide if they qualify for your retirement benefits plans. 

Employees can then sign up directly for retirement benefits. Your app gets accurate employee eligibility and deduction data from QuickBooks Online Payroll. Every time a change is made or payroll is run, you get a webhook with the new available data. 

Here's what to set up and our suggested build. We'll provide example queries and specific API entities you can use as a foundation for your app. 

## Step 1: Create your app in the Intuit Developer Portal

If you haven’t already, [create your app](../../getting-started/authentication/) on the developer portal.

## Step 2: Set your app's scopes

The Intuit Ecosystem API [uses scopes](../../getting-started/scopes/) to limit the type of data your app can access. You'll set scopes when you create your app. 

### If you want your app to be able to read and write data

To read QuickBooks Online Payroll data, and write in how much individual employees request for deductions, use these scopes:

* qb.company.read
* qb.company.taxidentifier.read
* qb.employee.read
* qb.employee.taxidentifier.read
* qb.payroll.benefits
* qb.payroll.compensation.read
* qb.employee.birthdate.read

### If you want your app to only read data

To read QuickBooks Online Payroll data, but not write, use these scopes:

* qb.company.read
* qb.company.taxidentifier.read
* qb.employee.read
* qb.employee.taxidentifier.read
* qb.payroll.compensation.read
* qb.employee.birthdate.read

  **Important**: The scopes you use depend on what you want your retirement benefits app to do. If you want your app to read and write data, use the `qb.payroll.benefits` scope. If you don't include the `qb.payroll.benefits` scope, your app can only read data from QuickBooks Online Payroll. It won't be able to write."

## Step 3: Get your app's credentials

1. [Sign in](https://developer.intuit.com/) to your developer account.
2. Select the **Dashboard** link on the toolbar. 
3. Select and open your app. 
4. In the **Production** section, select **Keys & OAuth**. 
5. Copy the **Client ID** and **Client Secret**. 

## Step 4: Authorize your app

If you haven't already, use your Client ID, Client Secret, and scopes to [set up OAuth 2.0](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0). 

## Step 5: Create queries for your app 

Use the sample queries in the following sections as guides. The field and value data comes directly from QuickBooks Online Payroll. You don't need to use every field, but we've included most to show what types of data your app can utilize. 

There are four main tasks to set up for retirement benefits apps:

* Get info from small businesses that connect to your app
* Get employee lists
* Capture employee contribution amounts (write only)
* Take deductions based on payslip data

### Endpoints

The endpoint for all queries is the same: **https://public.api.intuit.com/2020-04/graphql**

## Get info from small businesses that connect to your app

When small businesses connect to your retirement benefits app, you need to get info about the small business and their employees. Use this info to connect and map benefits data to the right people. 

### Create query

After small businesses connect to your app, use this sample query to call the getCompanyDetails entity and get info about their QuickBooks Online company: 

**Required entities**

* **getCompanyDetails**

**Query header** 

* Content-Type: **application/json**
* Authorization: [Use the scopes](../../getting-started/scopes/) you picked for your app to get access tokens. After [generating an OAuth token](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0), put it in the request header.

**Query body**

```
query getCompanyDetails {
  company {
    id
    industryType
    taxIdentifiers {
      taxIdentifierType
      value
    }
    companyName
    companyType
    contactMethods {
      primary
      active
      address {
        streetAddress1
      }
      email
    }
  }
}
```
**Tip**: If the small business decides to [subscribe to your app through the QuickBooks App store](https://quickbooks.intuit.com/app/apps/home/), their info will be prefilled.

## Get employee lists

After small businesses authorize your retirement benefits app, you get access to the `realmId` for their QuickBooks Online company. Use the `realmId` to get info about the businesses' employee roster. 

When small businesses first sign up for a plan, your app needs to query to get their last fiscal year's payslip data. You also may want to query for multiple years at once. Employee roster info comes directly from QuickBooks Online Payroll. You get full info for each employee and their status. This info all helps determine their eligibility.

Once you know an employee is eligible, you can invite them to your platform.
In order to map deductions correctly, use a field that uniquely identifies individual employees. For example, you can use their SSN. This offers the most flexibility. But, you can also map to other fields like their payroll IDs.

**Learn more about mapping to SSNs** 

Access to sensitive employee data, like SSN and date of birth, isn't enabled by default. Reach out to your Intuit partner to get the correct scopes for your app. 

All employees participating in a retirement plan through a small business are legally required to have a SSN by end of the year tax filing. However, as the benefits provider, you can choose how you validate the collected SSNs.

### Create a query

Use this sample query to call the `readEmployeeRoster` entity. This gets info for the employees on the small business' employee roster: 

**Required entities**
* **readEmployeeRoster** 

**Query header** 

* Content-Type: **application/json**
* Authorization: [Use the scopes](../../getting-started/scopes/) you picked for your app to get access tokens. After [generating an OAuth token](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0), put it in the request header.

**Query body**

```
query readEmployeeRoster {
  company {
    id
    industryType
    companyType
    employees{
      nodes {
        id
        firstName
        lastName
        displayName
        
        payrollProfile {
          preferredPhone
          preferredAddress {
            streetAddress1
            state
          }
          compensations {
            id
            active
            amount
          }
          deductions {
            id
            amount {
              percentage
              value
            }
          }
        }
      }
    }
  }
}
```
**Tip**: Remember, your app only sees the employees small business owners add to QuickBooks Online Payroll, not everyone who potentially works for them.

## Capture employee contribution amounts (write only)

Your retirement benefits app needs a way to let the individual employees sign up and enroll for benefits and make contributions. They should sign up for plans and select contribution levels in your app. 

If your app has write permissions (via scopes), you can transfer deduction info back to QuickBooks Online Payroll so it has matching data. Use the mutations below if your app can write info back to QuickBooks Online. 

### Create a mutation

You'll need to create separate mutations for the `createEmployeeDeduction` entity: 
* One mutation to set up deductions with the small business
* As many mutations as needed to record contributions for each employee

**Required entities** 
* **createEmployeeDeduction** 

**Mutation header**

* Content-Type: **application/json**
* Authorization: [Use the scopes](../../getting-started/scopes/) you picked for your app to get access tokens. After [generating an OAuth token](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0), put it in the request header.

**Mutation body**

Use this mutation to call the `createEmployeeDeduction` entity and write deductions and contributions to QuickBooks Online Payroll. This covers business and employee benefits: 

````
mutation {
 
  createEmployerDeduction (
    
    deduction : {
      name : "My plan deduction"
      statutoryDeductionPolicy: "Annual max is 10k"
    }
  ) {
    id
    name
  }
}
````

Use this mutation for each employee to create (or modify) deductions in QuickBooks Online Payroll. This ensures payroll data matches the contributions employees set in your retirement benefits app. 

You'll need to get the `employeeId` value using the employee roster query: 

```
mutation {
  
  createEmployeeDeduction (
    deduction : {
      employeeId: "<employee id>"
      active: true
      amount: {
        value : 500
        percentage : false
      }
      employerDeductionId: "<id from employer deduction>"
    } 
  ) {
    id
    active
    amount {
      percentage
      value
    }
  }
}
```
**Note**: If you as the retirement plan provider are taking over for an existing provider, please work directly with the small business' payroll admins to stop contributions from the previous plan. 

## Take deductions based on payslips

Each time a small business runs payroll, your retirement benefits app gets a webhook with each employees' payslip data. This tells you how much to take out for deductions for each employee. 

### Create a query

Use this sample query daily (preferably syncing during low traffic hours) to call the `readAllEmployeePayslips` entity and get employee payslip info:

**Required entities**
* **readAllEmployeePlayslips**

**Query header** 

* Content-Type: **application/json**
* Authorization: [Use the scopes](../../getting-started/scopes/) you picked for your app to get access tokens. After [generating an OAuth token](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/oauth-2.0), put it in the request header.

**Query body**

```
query readAllEmployeePayslips {
  company {
    id
    employees{
      nodes {
        id
        payrollProfile {
          paySchedule {
            id
            name
            initialPayDate
            frequency
          }
        }
        payslips {
          id
          payDate
          grossPay {
            amount
            yearToDateAmount
          }
          contributions {
            description
            contributionAmount {
              amount
              yearToDateAmount
            }
          }
          deductions {
            type
            description
            deductionAmount {
              amount
              yearToDateAmount
            }
          }
          paySchedule {
  	        id
  	        name
  	        initialPayDate
  	        frequency
          }
        }
      }
    }
  }
}
```
**Note**: It's possible to reassign a PaySchedule against an Employee. This means historical `paySchedules` can be accessed against each payslip. This may change which group they are paid with.

## Step 6: Go live with your app

Follow these steps when you're ready to [publish your app](https://developer.intuit.com/app/developer/qbo/docs/go-live). 
