---
layout: default
title: Employee Verification
nav_order: 8
parent: Use Cases
---


## Employee Verification

The following API samples show the different API calls that can be made to verify an employee.  The 3 flows documented below are:

1. [Verification of Employment](#verification-of-employment) (VOE)
2. [Verification of Income](#verification-of-income) (VOI)
3. [Social Service Verification](#social-service-verification) (SSV)

### Verification of Employment

```
mutation verificationOfEmployment {
  verifyEmployment(input: {type: VOE, encryptedTaxIdentifier: "enc-SSN-123", employeeIdentifier: "123-emp-id", requestId: "456-req-id"}) {
    type
    payrollProcessDateTime
    employeeIdentifier
    employeeInformation {
      taxIdentifier {
        taxIdentifierType
        value
      }
      firstName
      middleName
      lastName
      suffix
      birthDate
      homeAddress {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
    employerInformation {
      legalName
      legalAddress {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
    employmentInformation {
      employmentStatus
      originalHireDate
      hireDate
      terminationDate
      jobTitle
      workLocationAddress {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
  }
}
```

Sample Response

```
{
  "data": {
    "verifyEmployment": {
      "type": "VOE",
      "payrollProcessDateTime": "2021-02-23T09:23:11Z",
      "employeeIdentifier": "123-emp-id",
      "employeeInformation": {
        "taxIdentifier": {
          "taxIdentifierType": "ENCRYPTED_SSN",
          "value": "enc-SSN-123"
        },
        "firstName": "Alice",
        "middleName": "Jeane",
        "lastName": "Cooper",
        "suffix": null,
        "birthDate": "1963-11-03",
        "homeAddress": {
          "streetAddress1": "321 Center Street",
          "streetAddress2": "Apt B",
          "city": "Springfield",
          "state": "WY",
          "zipCode": "87356",
          "country": "US"
        }
      },
      "employerInformation": {
        "legalName": "Alice Art Shop",
        "legalAddress": {
          "streetAddress1": "321 Center Street",
          "streetAddress2": "Apt B",
          "city": "Springfield",
          "state": "WY",
          "zipCode": "87356",
          "country": "US"
        }
      },
      "employmentInformation": {
        "employmentStatus": "ACTIVE",
        "originalHireDate": "2018-11-03",
        "hireDate": "2020-11-03",
        "terminationDate": "2019-11-03",
        "jobTitle": "Accountant",
        "workLocationAddress": {
          "streetAddress1": "321 Center Street",
          "streetAddress2": "Apt B",
          "city": "Springfield",
          "state": "WY",
          "zipCode": "87356",
          "country": "US"
        }
      }
    }
  }
}
```

### Verification of Income

```
mutation verificationOfIncome {
  verifyIncome(input: {type: VOI, encryptedTaxIdentifier: "enc-SSN-123", employeeIdentifier: "123-emp-id", requestId: "456-req-id"}) {
    type
    payrollProcessDateTime
    employeeIdentifier
    employeeInformation {
      taxIdentifier {
        taxIdentifierType
        value
      }
      firstName
      middleName
      lastName
      suffix
      birthDate
      homeAddress {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
    employerInformation {
      legalName
      legalAddress {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
    employmentInformation {
      employmentStatus
      originalHireDate
      hireDate
      terminationDate
      jobTitle
      workLocationAddress {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
    payrollInformation {
      payFrequency
      payRate
      payType
      lastPaycheckTotalHours
      yearToDatePayInformation {
        year
        totalGrossWages
        grossBaseWages
        grossOtherWages {
          amount
          type
        }
      }
    }
  }
}
```

Sample Response

```
{
  "data": {
    "verifyIncome": {
      "type": "VOI",
      "payrollProcessDateTime": "2021-02-23T09:23:11Z",
      "employeeIdentifier": "123-emp-id",
      "employeeInformation": {
        "taxIdentifier": {
          "taxIdentifierType": "ENCRYPTED_SSN",
          "value": "enc-SSN-123"
        },
        "firstName": "Alice",
        "middleName": "Jeane",
        "lastName": "Cooper",
        "suffix": null,
        "birthDate": "1963-11-03",
        "homeAddress": {
          "streetAddress1": "321 Center Street",
          "streetAddress2": "Apt B",
          "city": "Springfield",
          "state": "WY",
          "zipCode": "87356",
          "country": "US"
        }
      },
      "employerInformation": {
        "legalName": "Alice Art Shop",
        "legalAddress": {
          "streetAddress1": "321 Center Street",
          "streetAddress2": "Apt B",
          "city": "Springfield",
          "state": "WY",
          "zipCode": "87356",
          "country": "US"
        }
      },
      "employmentInformation": {
        "employmentStatus": "ACTIVE",
        "originalHireDate": "2018-11-03",
        "hireDate": "2020-11-03",
        "terminationDate": "2019-11-03",
        "jobTitle": "Accountant",
        "workLocationAddress": {
          "streetAddress1": "321 Center Street",
          "streetAddress2": "Apt B",
          "city": "Springfield",
          "state": "WY",
          "zipCode": "87356",
          "country": "US"
        }
      },
      "payrollInformation": {
        "payFrequency": "BIWEEKLY",
        "payRate": 55000.00,
        "payType": "HOURLY",
        "lastPaycheckTotalHours": 160.0,
        "yearToDatePayInformation": [
          {
            "year": "2021",
            "totalGrossWages": 67000.00,
            "grossBaseWages": 55000.00,
            "grossOtherWages": [
              {
                "amount": 9000.00,
                "type": "Bonus Wage"
              },
              {
                "amount": 2000.00,
                "type": "Overtime Wage"
              },
              {
                "amount": 1000.00,
                "type": "Holiday Wage"
              }
            ]
          },
          {
            "year": "2020",
            "totalGrossWages": 67000.00,
            "grossBaseWages": 55000.00,
            "grossOtherWages": [
              {
                "amount": 9000.00,
                "type": "Bonus Wage"
              },
              {
                "amount": 2000.00,
                "type": "Overtime Wage"
              },
              {
                "amount": 1000.00,
                "type": "Holiday Wage"
              }
            ]
          },
          {
            "year": "2019",
            "totalGrossWages": 67000.00,
            "grossBaseWages": 55000.00,
            "grossOtherWages": [
              {
                "amount": 9000.00,
                "type": "Bonus Wage"
              },
              {
                "amount": 2000.00,
                "type": "Overtime Wage"
              },
              {
                "amount": 1000.00,
                "type": "Holiday Wage"
              }
            ]
          }
        ]
      }
    }
  }
}
```

### Social Services Verification

```
mutation socialServiceVerification {
  verifyIncome(input: {type: SSV, encryptedTaxIdentifier: "enc-SSN-123", employeeIdentifier: "123-emp-id", requestId: "456-req-id"}) {
    type
    payrollProcessDateTime
    employeeIdentifier
    employeeInformation {
      taxIdentifier {
        taxIdentifierType
        value
      }
      firstName
      middleName
      lastName
      suffix
      birthDate
      homeAddress {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
    employerInformation {
      legalName
      taxIdentifier {
        taxIdentifierType
        value
      }
      legalAddress {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
    employmentInformation {
      employmentStatus
      originalHireDate
      hireDate
      terminationDate
      jobTitle
      workLocationAddress {
        streetAddress1
        streetAddress2
        city
        state
        zipCode
        country
      }
    }
    payrollInformation {
      payFrequency
      payRate
      payType
      lastPaycheckTotalHours
      yearToDatePayInformation {
        year
        totalGrossWages
      }
      payPeriodInformation {
        payDate
        startDate
        endDate
        hoursWorked
        grossWages
        netWages
        yearToDateGrossWages
      }
    }
  }
}
```

Sample Response

```
{
  "data": {
    "verifyIncome": {
      "type": "SSV",
      "payrollProcessDateTime": "2021-02-23T09:23:11Z",
      "employeeIdentifier": "123-emp-id",
      "employeeInformation": {
        "taxIdentifier": {
          "taxIdentifierType": "ENCRYPTED_SSN",
          "value": "enc-SSN-123"
        },
        "firstName": "Alice",
        "middleName": "Jeane",
        "lastName": "Cooper",
        "suffix": null,
        "birthDate": "1963-11-03",
        "homeAddress": {
          "streetAddress1": "321 Center Street",
          "streetAddress2": "Apt B",
          "city": "Springfield",
          "state": "WY",
          "zipCode": "87356",
          "country": "US"
        }
      },
      "employerInformation": {
        "legalName": "Alice Art Shop",
        "taxIdentifier": {
          "taxIdentifierType": "FEIN",
          "value": "123-23-4567"
        },
        "legalAddress": {
          "streetAddress1": "321 Center Street",
          "streetAddress2": "Apt B",
          "city": "Springfield",
          "state": "WY",
          "zipCode": "87356",
          "country": "US"
        }
      },
      "employmentInformation": {
        "employmentStatus": "ACTIVE",
        "originalHireDate": "2018-11-03",
        "hireDate": "2020-11-03",
        "terminationDate": "2019-11-03",
        "jobTitle": "Accountant",
        "workLocationAddress": {
          "streetAddress1": "321 Center Street",
          "streetAddress2": "Apt B",
          "city": "Springfield",
          "state": "WY",
          "zipCode": "87356",
          "country": "US"
        }
      },
      "payrollInformation": {
        "payFrequency": "BIWEEKLY",
        "payRate": 55000.00,
        "payType": "HOURLY",
        "lastPaycheckTotalHours": 160.0,
        "yearToDatePayInformation": [
          {
            "year": "2021",
            "totalGrossWages": 67000.00
          },
          {
            "year": "2020",
            "totalGrossWages": 67000.00
          },
          {
            "year": "2019",
            "totalGrossWages": 67000.00
          }
        ],
        "payPeriodInformation": [
          {
            "payDate": "2021-03-19",
            "startDate": "2021-03-01",
            "endDate": "2021-03-15",
            "hoursWorked": 40.0,
            "grossWages": 5000.00,
            "netWages": 2000.00,
            "yearToDateGrossWages": 10000.00
          },
          {
            "payDate": "2021-04-02",
            "startDate": "2021-03-15",
            "endDate": "2021-03-29",
            "hoursWorked": 40.0,
            "grossWages": 5000.00,
            "netWages": 2000.00,
            "yearToDateGrossWages": 10000.00
          },
          {
            "payDate": "2021-04-16",
            "startDate": "2021-03-29",
            "endDate": "2021-04-12",
            "hoursWorked": 40.0,
            "grossWages": 5000.00,
            "netWages": 2000.00,
            "yearToDateGrossWages": 10000.00
          },
          {
            "payDate": "2021-04-23",
            "startDate": "2021-04-12",
            "endDate": "2021-04-19",
            "hoursWorked": 40.0,
            "grossWages": 5000.00,
            "netWages": 2000.00,
            "yearToDateGrossWages": 10000.00
          }
        ]
      }
    }
  }
}
```
