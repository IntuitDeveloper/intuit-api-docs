---
layout: default
title: API Charges
nav_order: 4
parent: FAQ
---

# API charges & reporting (retirement partners)

*Note: this information applies to retirement plan providers accessing the Intuit Payroll services and is subject to change. Beta participants should refer to specific terms in their 3rd party Payroll API Beta agreement*

## Overview
Access to Intuit's Payroll API service incurs a fee for each connected QuickBooks company. You receive an invoice on a quarterly basis. 

To track API fees and automate invoicing, retirement providers are required to upload a monthly usage report via Intuit's Partner File Transfer System (PFTS). 

## 1) Setup access to PFTS
Refer to [PFTS setup instructions](../../../assets/files/HowToConnectToPFTS.pdf) for specific commands on Linux, Mac or Windows. 

1. **Create a public SSH key**
2. **Submit your public key to Intuit to enable PFTS access**.  Copy paste the contents of your public key and submit as an attachment to your Intuit point of contact. 
3. **Test  your PFTS connection** once you receive notification from Intuit that your PFTS account is active

##  2) Reporting and invoicing process

1. **On the first business day of each month**: generate usage report for the previous month. Upload the file to the `/incoming` folder with the following naming convention: `<partnername>_YYYYMM.csv` 

	*Note: File retention on Intuit's PFTS  server is set to 30 days, after which, files are purged and not retrievable.* 

2. **On the first business day of each quarter** Intuit issues an invoice based on your total API usage for the 3 previous months. The invoice needs to be paid within 30 days of reception. 

## 3) File format

Upload the report as comma separated values (.csv). See sample monthly report [here](../../../assets/files/partnername_202104.csv).

*Important notes:*
 - *Keep columns in the exact same order in your generated csv file*
 - *The last line of the report must be a total summary*
	
| # |  Column name | Description |
|--|--|--|
| 1 | Customer name | Name of the connected company |
| 2 | Reporting month | Calendar month for the current usage report. Format YYYY-MM. |
| 3 | Connection date | Date the API connection was established with this company (e.g. the date a successful OAuth access token was created). Format YYYY-MM-DD. |
| 4 | QuickBooks company ID | Unique identifier for the Intuit QuickBooks company. |
| 5 | Total employees | total number of employees who are active (i.e. not terminated) with the company, regardless of whether or not they are participating in or eligible for the retirement plan. |
| 6 | Number of participating employees | Total number of employees who contributed to their retirement plan in the reporting month, i.e. there has been a financial contribution to the plan whether from employee or employer.
| 7 | Fee | Fee for this active connection. Will be the identical for each row as specified in the 3rd party Payroll Beta Agreement
