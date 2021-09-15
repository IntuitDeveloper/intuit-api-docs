---
layout: default
title: PayrollBenefits
nav_order: 18
parent: Use Cases
---

# Build payroll benefits apps

As a payroll benefit provider, you can build apps that let small businesses connect their QuickBooks Online Payroll (not Intuit Payroll) data. This data tells you each employee's eligibility - use it to decide if they qualify for your payroll benefits plans. 

Employees can then sign up directly for payroll benefits. Your app gets accurate employee contribution and deduction data from QuickBooks Online Payroll. Each time a change is made or payroll is run, your app receives a webhook event depicting which entities changed.

## Step 1: Create your app in the Intuit Developer Portal

If you haven’t already, [create your app](../../getting-started/authentication/) on the developer portal.

## Step 2: Set your app's scopes

The Intuit Ecosystem API [uses scopes](../../getting-started/scopes/) to limit the type of data your app can access. You'll set scopes when you create your app. 

### If you want your app to be able to read and write data

To read QuickBooks Online Payroll data, and write in how much individual employees request for deductions, use these scopes:

* qb.payroll.benefits


  **Important**: The scopes you use depend on what you want your payroll benefits app to do. If you want your app to read and write data, use the `qb.payroll.benefits` scope.

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


## Create an Employer Benefit

Use this method to create an Employer Benefit such as HSA, FSA, etc. The field `statutoryBenefitPolicy` depicts the actual benefit type, and can have the following values - 

List of possible values for `statutoryBenefitPolicy` - 

```
TBPO_CUS_MEDICAL - Health Insurance (Medical)
TBPO_CUS_VISION - Health Insurance (Vision)
TBPO_CUS_DENTAL - Health Insurance (Dental)
TBPO_CUS_DEPCARE_FSA - FSA (Dependent Care)
TBPO_CUS_MED_FSA - FSA (Medical Expense)
TBPO_CUS_PRETAX_HSA - HSA (PreTax)
TBPO_CUS_TAXABLE_HSA - HSA (Taxable)
TBPO_CCA_PRIVATE_MEDICAL
```

Mutation Query - 

```
mutation createEmployerBenefit($input: CreateEmployerBenefitInput!) {
  createEmployerBenefit(benefit: $input) {
    id
    name
    statutoryBenefitPolicy
  }
}
```

Variables - 

```
{
	"input": {
		"name": "A Sample HSA (Taxable)",
		"statutoryBenefitPolicy": "TBPO_CUS_TAXABLE_HSA"
	}
}
```


## Create an Employee Benefit (i.e. Assign Employer Benefit against an Employee)

An Employer Benefit once created can be assigned against an existing Employee. The Employer as well as Employee can contribute against an Employee Benefit (e.g HSA plan).

Mutation Query - 

```
mutation createEmployeeBenefit($input: CreateEmployeeBenefitInput!) {
  createEmployeeBenefit(benefit: $input) {
    id
    active
    employerSetup {
      amount {
        percentage
        value
      }
      cappings {
        amount
        timeInterval
      }
    }
    employeeSetup {
      amount {
        percentage
        value
      }
      cappings {
        amount
        timeInterval
      }
    }
    employerBenefit {
      id
      name
      statutoryBenefitPolicy
    }
  }
}
```

Variables - 

```
{
	"input": {
		"employerBenefitId": "djQuMTo5MTMwMzUzODUxMTUyODc2OjJlN2Y1MmQyMGM:2644960",
		"employeeId": "djQuMTo5MTMwMzUzODUxMTUyODc2OjlkNjk5ZTk2MDg:0020712e2edc488cea4778b6cf1ee37da93d96",
		"active": true,
		"employeeSetup": {
			"amount": {
				"value": "10",
				"percentage": false
			},
			"cappings": [
				{
					"amount": "100",
					"timeInterval": "FISCALYEAR"
				}
			]
		},
		"employerSetup": {
			"amount": {
				"value": "20",
				"percentage": false
			},
			"cappings": [
				{
					"amount": "100",
					"timeInterval": "FISCALYEAR"
				}
			]
		}
	}
}
```


## List all Employer Benefits against Company

Use the following query the list of Employer Benefits (HSA plan, FSA plan, etc) defined against the current company. 

Query - 

```
query readAllEmployerBenefits {
  company {
    payrollProfile {
      benefits {
        id
        name
        statutoryBenefitPolicy
      }
    }
  }
}
```


## Fetch Employee Roster (Benefits)

The following query will list all Benefits assigned against a given Employee. The Employee benefiit will also inlude information about the Employee and Employer contributions.

Query - 

```
query fetchEmployeeRoster {
  company {
    employees {
      nodes {
        firstName
        lastName
        payrollProfile {
          benefits {
            id
            active
            employerBenefit {
              id
              name
              statutoryBenefitPolicy
            }
            employerSetup {
              amount {
                percentage
                value
              }
              cappings {
                amount
                timeInterval
              }
            }
            employeeSetup {
              amount {
                percentage
                value
              }
              cappings {
                amount
                timeInterval
              }
            }
          }
        }
      }
    }
  }
}
```


## Fetch Employee Payslips 

Once Payroll has been executed for the current monthh, the Payroll Benefits should also show up against an Employee Payslip (Contributions and deductions). 

Query (with EmployeeId as filter) - 

```
query readAllEmployeePayslips {
  company {
    employees(
     filter: {
        id: {
          equals: "djQuMTo5MTMwMzUzODUxMTUyODc2OjlkNjk5ZTk2MDg:0020718d03ea5feb4b49f28ff20b9e7e201aa7"
        }
      }
    ) {
      pageInfo {
        hasNextPage
        startCursor
        endCursor
        hasPreviousPage
      }
      nodes {
        id
        firstName
        lastName

        employeePayslips {
          nodes {
            id
            deductions {
              type
              description
              deductionAmount {
                amount
                yearToDateAmount
              }
            }
            contributions {
              type
              description

              contributionAmount {
                amount
                yearToDateAmount
              }
            }
          }
        }
      }
    }
  }
}
```



## Step 6: Go live with your app

Follow these steps when you're ready to [publish your app](https://developer.intuit.com/app/developer/qbo/docs/go-live). 

