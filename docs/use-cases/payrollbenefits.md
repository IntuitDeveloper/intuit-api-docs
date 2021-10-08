---
layout: default
title: Payroll Benefits
nav_order: 18
parent: Use Cases
---

# Build payroll benefits apps

As a payroll benefit provider, you can build apps that let small businesses connect their QuickBooks Online Payroll (not Intuit Payroll) data. This data tells you each employee's eligibility - use it to decide if they qualify for your payroll benefits plans. 

Employees can then sign up directly for payroll benefits. Your app gets accurate employee contribution and deduction data from QuickBooks Online Payroll. Each time a change is made or payroll is run, your app receives a webhook event depicting which entities changed.

Please visit this section for AppSetup: [Prerequisites](../#build-apps-around-use-cases) 


To read QuickBooks Online Payroll Benefits data, use these scopes:

* qb.payroll.benefits



## Create queries for your app 

Use the sample queries in the following sections as guides. The field and value data comes directly from QuickBooks Online Payroll. You don't need to use every field, but we've included most to show what types of data your app can utilize. 


### Create an Employer Benefit

Use this method to create an Employer Benefit such as HSA, FSA, etc. The field `statutoryBenefitPolicy` depicts the actual benefit type, and can have the following values - 


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


### Create an Employee Benefit (i.e. Assign Employer Benefit against an Employee)

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


### List all Employer Benefits against Company

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


### Fetch Employee Roster (Benefits)

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


### Fetch Employee Payslips 

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

