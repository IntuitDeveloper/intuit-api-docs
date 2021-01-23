---
layout: default
title: Payroll
nav_order: 2
parent: FAQ
---

# Payroll

The following are some commonly asked questions related to Payroll. There are two sections, one related to the operating mechanism of the payroll service, and then detailed suggestions about how to use it working with retirement services. 

## Payroll General 

**1\.  What do I need to access payroll data?**

As of right now, the scopes necessary to access payroll data are not publicly exposed and cannot be onboarded without Intuit help. You can learn more on the scopes FAQ page about which you might need, but to get access you will need to work with an Intuit representative.

**2\. Should I be using development keys to test my app?**

**No**, Currently the Payroll service does *not* have a sandbox/playground/dev environment to work with. As such, as a payroll 3rd-party partner you will be given a fake account in the production environment you do not have to pay for, and as such you *must use production keys.* 

**3\. Where are the employer contributions stored?**

Within the payslip object per employee you will be able to see both the employee and employer contributions. This is set at the employee level, not generally at the company/employeer level to allow for different contribution levels of employees.

**4\. Do you expose payroll contribution types?**

Not currently. We expose type for other elements within payroll but do not show a need for this information based on what our 3rd party partners are trying to accomplish. 

**5\. Employee PensionID and Company PensionID do not match**

Yes this is an outstanding issue. We recommend that our partners match at an employee level for everything they are trying to accomplish.  

**6\. How can I explore more about what is available via the Payroll API?**

Once you have access to payroll (the proper scopes) you can explore the GraphQL entity with introspection (for example in Apollo Studio). We also have example Postman collections for retirement that your Intuit representative can get you set up with. 

  **7\. How do I get alerted of changes to employees or if a payroll is run?**

Webhooks, coming soon. We will alert you of any changes to employees (status, contact information etc), company, or payroll runs. Until that feature is released, we recommend running a nightly check to see if anything has changed. 


## Retirement and Payroll 

**1\. What do I have permission to change?**

Currently we allow our partners read/write access on any contibutions/deductions made through the API. If there are deductions from previous retirement providers, or other items that need to be deleted, you must work with the company owner on this through their UI. 

**2\. Is there no company-wide matching?**

**Correct** Intuit Online Payroll does not provide the capability for company-wide matching rules. We recommend that the retirement provider calculate the % match per employee and feed that number into our employer match withdrawal field. These fields can also have their own caps, for example 10k for the year which you can set. This allows the retirement provider to offer more options, like tiered matching, and be compatible with Intuit Online Payroll. 

**3\. Does Intuit handle catch-up contributions?**

**Yes, but you must tell us.** We do not auto-calculate based on date of birth who is eligible for the catch-up contributions, but we will handle it if you change the default contrubution caps. For example, for 2020 you can edit the cap for retirement contrubutions from null (the default for that year, 19.5k) to the 26k. Null in the API shows up as the default (19.5k) in the UI. 

**4\. What about combined contributions (Roth + traditional), how do I cap that?**

We do not handle that case right now and will leave it up the to the provider. Some providers have elected to calculate the caps for each and feed a cap respective of each, for example in 5% and 5% they would each have a cap of 9.75K. Other providers have elected to only support one contrubution at a time. Others have set to track the contributions on their own and feed back to IOP when the cap has been hit, zeroing out further contributions. 

**5\. How is leave of absence handled?**

The change of status will be a web hook alert that you can use when that is released. However, because the field for "effective date" is not required, we do not expose it so that our partners do not build to depend on it. One partner is recording the date of start to be the end of the pay period that the change happened, and same for when they are reinstated, end of the period where it changed back.  

**6\. Hours are not specified**

Correct, we do not currently expose the type of hours worked, however you must sum the total hours for each paycheck to check eligibility. We are working to improve this. 

**7\. Are pay scheduled supported?**

We are working to expose that, but it is not done yet. One partner is limiting the supported plans to be ones that only have one pay cycle until this feature is available. 
