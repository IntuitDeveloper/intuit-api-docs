---
layout: default
title: Scopes
nav_order: 2
parent: Getting Started
---

**Last updated**: May 11, 2021

**Read time**: 1 min

# Learn about Intuit Ecosystem scopes

In GraphQL, scopes limit what data your app can read and update. Instead of getting broad permissions for everything, set granular permissions so your app only focuses on what's necessary.

Here are the current scopes for Intuit Ecosystem API. 

| **Scope**                                     | **Description**                      | **Sensitive data**       |
|:----------------------------------------------|:-------------------------------------|:-------------------------|
| qb.company.read                               | Grants access to company information | |
| qb.company.taxidentifier.read                 | Grants access to the tax identifier (EIN, CBN) for the company | Yes |
| qb.employee.read                              | Grants access to employee information | |
| qb.employee.taxidentifier.read                | Grants access to the tax identifier (SSN, SIN) for the employee | Yes |
| qb.employee.birthdate.read                    | Grants access to employee birth date | |
| qb.payroll.compensation.read                  | Grants access to payroll compensation | |
| qb.payroll.benefits                           | Grants access to payroll benefits | |
| qb.project.write                              | Grants access to create/update/delete/recover projects for the company | |


**Note**: Sensitive data requires additional legal agreement and manual onboarding with our support team. 