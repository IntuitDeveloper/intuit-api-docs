---
layout: default
title: Employee Verification
nav_order: 7
parent: Schema Entities
---


## Employee Verification

The following API samples show the different API calls that can be made to verify an employee.  The 3 flows documented below are:

1. [Verification of Employment](#verification-of-employment) (VOE)
2. [Verification of Income](#verification-of-income) (VOI)
3. [Social Service Verification](#social-service-verification) (SSV)
4. [Verification Data Feed URL](#verification-data-feed-url) (Cache File)

### Verification of Employment

```
mutation verificationOfEmployment {
  verifyEmployment(input: {type: VERIFICATION_OF_EMPLOYMENT, encryptedTaxIdentifier: "enc-SSN-123", encryptionKeyIdentifier: "hmacKeyId-123", employeeIdentifier: "123-emp-id", requestId: "456-req-id"}) {
    type
    lastPayDate
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
      employerIdentifier
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
      "type": "VERIFICATION_OF_EMPLOYMENT",
      "lastPayDate": "2021-02-23",
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
        "employerIdentifier": "3691470",
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
  verifyIncome(input: {type: VERIFICATION_OF_INCOME, encryptedTaxIdentifier: "enc-SSN-123", encryptionKeyIdentifier: "hmacKeyId-123", employeeIdentifier: "123-emp-id", requestId: "456-req-id"}) {
    type
    lastPayDate
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
      employerIdentifier
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
        totalGrossCompensation
        grossBaseCompensation
        grossOvertimeCompensation
        grossBonusCompensation
        grossCommissionCompensation
        grossOtherCompensation
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
      "type": "VERIFICATION_OF_INCOME",
      "lastPayDate": "2021-02-23",
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
        "employerIdentifier": "3691470",
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
            "totalGrossCompensation": 67000.00,
            "grossBaseCompensation": 55000.00,
            "grossOvertimeCompensation": 2000.00,
            "grossBonusCompensation": 9000.00,
            "grossCommissionCompensation": 1000.00,
            "grossOtherCompensation": 0
          },
          {
            "year": "2020",
            "totalGrossCompensation": 67000.00,
            "grossBaseCompensation": 55000.00,
            "grossOvertimeCompensation": 2000.00,
            "grossBonusCompensation": 9000.00,
            "grossCommissionCompensation": 1000.00,
            "grossOtherCompensation": 0
          },
          {
            "year": "2019",
            "totalGrossCompensation": 67000.00,
            "grossBaseCompensation": 55000.00,
            "grossOvertimeCompensation": 2000.00,
            "grossBonusCompensation": 9000.00,
            "grossCommissionCompensation": 1000.00,
            "grossOtherCompensation": 0
          }
        ]
      }
    }
  }
}
```

### Social Service Verification

```
mutation socialServiceVerification {
  verifyIncome(input: {type: SOCIAL_SERVICE_VERIFICATION, encryptedTaxIdentifier: "enc-SSN-123", encryptionKeyIdentifier: "hmacKeyId-123", employeeIdentifier: "123-emp-id", requestId: "456-req-id"}) {
    type
    lastPayDate
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
      employerIdentifier
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
        totalGrossCompensation
      }
      payPeriodInformation {
        payDate
        startDate
        endDate
        hoursWorked
        grossCompensation
        netCompensation
        yearToDateGrossCompensation
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
      "type": "SOCIAL_SERVICE_VERIFICATION",
      "lastPayDate": "2021-02-23",
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
        "employerIdentifier": "3691470",
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
            "totalGrossCompensation": 67000.00
          },
          {
            "year": "2020",
            "totalGrossCompensation": 67000.00
          },
          {
            "year": "2019",
            "totalGrossCompensation": 67000.00
          }
        ],
        "payPeriodInformation": [
          {
            "payDate": "2021-03-19",
            "startDate": "2021-03-01",
            "endDate": "2021-03-15",
            "hoursWorked": 40.0,
            "grossCompensation": 5000.00,
            "netCompensation": 2000.00,
            "yearToDateGrossCompensation": 10000.00
          },
          {
            "payDate": "2021-04-02",
            "startDate": "2021-03-15",
            "endDate": "2021-03-29",
            "hoursWorked": 40.0,
            "grossCompensation": 5000.00,
            "netCompensation": 2000.00,
            "yearToDateGrossCompensation": 10000.00
          },
          {
            "payDate": "2021-04-16",
            "startDate": "2021-03-29",
            "endDate": "2021-04-12",
            "hoursWorked": 40.0,
            "grossCompensation": 5000.00,
            "netCompensation": 2000.00,
            "yearToDateGrossCompensation": 10000.00
          },
          {
            "payDate": "2021-04-23",
            "startDate": "2021-04-12",
            "endDate": "2021-04-19",
            "hoursWorked": 40.0,
            "grossCompensation": 5000.00,
            "netCompensation": 2000.00,
            "yearToDateGrossCompensation": 10000.00
          }
        ]
      }
    }
  }
}
```

### Verification Data Feed URL

```
mutation verificationDataFeedURL {
  generateEmployeeVerificationDataFeedUrl {
    fileName
    url
    expiry
    fileGeneratedTimestamp
    recordCount
    keyIdentifier
    encryptedKeyValue
    publicKeyName
  }
}
```

Sample Response
```
{
  "data": {
    "generateEmployeeVerificationDataFeedUrl": {
      "fileName": "Intuit_Cache.txt",
      "url": "https://intuit-qbo-prod-4.s3.amazonaws.com/123146276328424/attachments/4e61e3c9-d0b9-4b69-b407-e49fb0202eb9Intuit_Cache.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20210303T212431Z&X-Amz-SignedHeaders=host&X-Amz-Expires=900&X-Amz-Credential=AKIA3V3MBG4KOIC66PTF%2F20210303%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=392da39ba07d4286a9ee055aed4833202dfdf4eca8597615cb82e0663eb10783",
      "expiry": "2021-04-22T11:23:11Z",
      "fileGeneratedTimestamp": "2021-04-22T09:23:11Z",
      "recordCount": 1000000,
      "keyIdentifier": "12w9523523",
      "encryptedKeyValue": "wr3wr32rwrf3f3r23rwr2rn23rij23oir2oi3rhsfwerwerwerfwerfwewewer",
      "publicKeyName": "4321w9523523"
    }
  }
}
```
