---
layout: default
title: Retirement
nav_order: 2
parent: Use Cases
---

## Retirement

Intuit Payroll is engaged in partnerships with Retirement plan providers to offer Retirement benefits to Small Business Owners. This will allow businesses to provide retirement benefits to their employees. This guide will help you understand the high level integration.

### Integration Steps

* Create and configure app on Inuit Developer portal: [pre-production](https://developer-stage.intuit.com/app/developer/homepage) (do this first) and [production](https://developer.intuit.com/app/developer/homepage)
  * read the [get started](https://developer.intuit.com/app/developer/qbo/docs/get-started) and [go live](https://developer.intuit.com/app/developer/qbo/docs/go-live) guide for a better understanding of the process for building apps with Intuit's ecosystem.  
* Implement SSO using OAuth2.0 authentication implementation which confirms with OpenID Connection specification
  * [OpenID Connect](https://developer.intuit.com/app/developer/qbo/docs/develop/authentication-and-authorization/openid-connect). Using OpenID you will have access to user information.
  * Establish connection between your app and QBO account for authorization to make calls

* Call Payroll APIs using the GraphQL end point. Rest of the document talks about the APIs you can call.

### Use Cases

There are four major connection points into payroll for the third party Retirement providers 

#### Company Setup

When first setting up a company with a new Retirement provider, information about the company needs to be sent back to map the authorization to the information in their system. Here are the fields as they have described it.

* Company ID
* taxidentifiers (EIN)
* Company Name
* Company Address (primary address -> formatted address)
* Admin Email

This information is particularly helpful because if the company owner decides to subscribe to a Retirement provider through the QB App Store, then this information will be pre-filled for them. And if the Retirement provider has been authorized they can pull an employee roster which will help their recommendation engine about what kind of plan to pick for everyone. 

After establishing a connection with the QBO company, run this query for company details

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

#### Employee roster

When setting up the plan, the Retirement provider has access to the company's employee roster and their current status (active/not). Other endpoints will enhance this employee info such as the Payslips for the year (being eligible for the plan requires 1000 hours worked in the US) and previous deduction elections if converting from another plan. 

* Employee ID
* First Name
* Last Name
* Employment Type
* Date of birth
* Hire Date
* Termination Date
* Compensations (Salary, bonus, etc)
* Email
* Physical Address (preferred to be in separate field, add 1, add 2, city, state, zip)
* Employee Status
* SSN 

SSN is the preferred way of mapping, but payroll ID can work as well up to a point. For legal reasons to be part of a plan, all employees participating in the plan must have SSN by the time of filing at the end of the year. Providers choose to do this differently:

* Some Retirement providers chose to not enroll those employees that didn’t log in to select an election (and provide SSN)
* others will just fail due to auto-enroll preferences. 
* Some companies will enroll everyone and then near the end of the fiscal year (for us is always with calendar year QBO) just notify the owner of the plan of missing compliance data (SSN or Tax ID)

*Access to employee SSN and date of birth is not included by default, work with your Intuit partner to get the necessary scopes associated with your app.*

After establishing connection with QBO company run this  query for employee roster

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

#### Contribution Level

Retirement Providers will have their own screens for sign up and enrollment of employees of the company, but will require that information be transferred back to QBO Payroll so that the correct deductions can be taken. 
 
They will then need to write (and read) these fields for contribution per employee level. The only person who can edit the names or fields of each contribution will be the creator. If you are taking over from a different company as Retirement provider you will need to work with QBO company's payroll Admins to sunset contributions from previous plan. 

* Traditional % or Traditional $
* Roth % or Roth $
* loan amount $ 
* Loan ID
* Employer contribution %
* Employer contributions limit
* Nonelective contribution 
* Deduction Code

Setup up a deduction for the employer 
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

For each employee on the plan, get their ID using the roster query and setup a deduction.

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

#### Paycheck Information

Retirement providers need to download Payslips after each payroll run so they know how much in deductions to take out for the employees, and this is where deductions details are most important.   At the beginning of the plan, providers will need to query for up to all of last fiscal year’s Payslips to determine plan eligibility for each employee:

* Pay date
* Payroll Process Date (approved date)
* Employee ID
* SSN (again above entitlements)
* Paycheck ID
* Gross Pay
* YTD Pay (optional, not launch blocker)
* Payroll Type (optional - bonus, overtime, regular, etc)
* Hours Worked
* Amount deducted for each category (employee)
  * Roth
  * Traditional
  * Loan
* Employer contribution  

After establishing connection with QBO company run this  query to download Payslips periodically.

```
query readAllEmployeePayslips {
  company {
	id
    employees{
      nodes {
        id
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
          }
      }
    }
  }
}
```
