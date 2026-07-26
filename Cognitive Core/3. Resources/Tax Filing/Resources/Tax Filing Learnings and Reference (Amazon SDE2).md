# Tax Filing Learnings and Reference - Amazon SDE2

## Context

- Salaried employee in India working at Amazon
- Income sources:
  - Salary
  - Amazon RSUs from US-listed shares
  - Savings account interest
- Filing:
  - FY 2025-26
  - AY 2026-27

---

## AIS and Form 26AS

### AIS

AIS, or Annual Information Statement, is a statement from the Income Tax Department containing financial information reported by different institutions.

Use it to check:

- Interest income
- Securities transactions
- Mutual funds
- Foreign assets
- Other financial transactions

Download path: Income Tax Portal -> Services -> Annual Information Statement (AIS)

AIS PDF password format: PAN in uppercase + date of birth in `DDMMYYYY` format

Example: `ABCDE1234F01011990`

### Form 26AS

Form 26AS contains:

- TDS deducted by employer
- TDS deducted by banks
- Tax credits
- Refund details

Difference:

- AIS: shows financial activity reported to the Income Tax Department
- Form 26AS: shows tax credits and TDS

---

## Amazon RSU Understanding

Amazon RSU lifecycle:

Grant -> Vesting -> Shares become yours -> Some shares sold for tax withholding -> Remaining shares held in brokerage account

Important dates:

- Grant date: date RSUs are given by Amazon
- Vest date: date shares become yours; used as acquisition date for Foreign Asset reporting
- Sale date: date shares are sold

For Schedule FA:

- Acquisition date = RSU vest date
- Do not use grant date
- Do not use Amazon joining date

---

## Schedule FA Overview

Amazon RSUs require reporting because they are foreign assets.

Two sections are relevant:

1. A2 - Foreign Custodial Account
2. A3 - Foreign Equity Interest

---

## A2 - Foreign Custodial Account

This represents the foreign brokerage account where Amazon shares are held.

Example: Morgan Stanley StockPlan Connect

Status: Owner

Reason:

- Brokerage account is in your name
- Shares belong to you

Financial institution details:

- Name: Morgan Stanley Smith Barney LLC
- Address: 1 New York Plaza, 26th Floor, New York, NY 10004, USA
- ZIP: 10004

Account opening date: use the date your Morgan Stanley account was created.

Find it from:

- Morgan Stanley account details
- Account documents

Peak balance during period:

- Meaning: highest value of the foreign brokerage account from 01-Jan-2025 to 31-Dec-2025
- Calculation: peak USD value x USD-INR exchange rate on peak date

Closing balance:

- Meaning: value of brokerage account on 31-Dec-2025
- Calculation: shares held on 31-Dec-2025 x Amazon closing price x USD-INR rate on 31-Dec-2025

Gross amount paid/credited:

- Include dividends, cash credits, and sale proceeds if applicable
- Do not include salary, RSU grant value, or stock price increase
- For Amazon RSUs, this is usually `0`

---

## A3 - Foreign Equity Interest

This represents ownership of Amazon shares.

Entity details:

- Entity: Amazon.com Inc.
- Country: United States of America
- Address: Amazon.com Inc., 410 Terry Avenue North, Seattle, WA 98109, United States
- ZIP: 98109
- Nature of entity: Listed Company
- Nature of interest: Equity

Date of acquiring interest:

- For RSUs, use the RSU vesting date
- Example: 15-Feb-2025
- Do not use grant date or joining date

Initial value of investment:

- Meaning: value when shares were acquired
- Formula: number of shares vested x Amazon share price on vest date
- Convert USD to INR

Peak value of investment:

- Meaning: highest market value of Amazon shares during 2025
- Formula: highest number of shares held x Amazon stock price on that date
- Convert USD to INR

Closing balance:

- Meaning: value of Amazon shares held on 31-Dec-2025
- Formula: shares held on 31-Dec-2025 x Amazon closing price on 31-Dec-2025
- Convert USD to INR

---

## Exchange Rate Rules

For foreign assets:

- Peak value: use exchange rate on peak value date
- Closing value: use exchange rate on 31-Dec-2025

Examples:

- Peak: USD value x USD-INR rate on peak date
- Closing: USD value x USD-INR rate on 31-Dec-2025

---

## Salary Schedule

Profit in lieu of Salary under Section 17(3):

- For normal Amazon employment, enter `0`
- Applicable only for severance compensation, termination payments, or special employer compensation
- Not applicable for salary, bonus, RSU vesting, or regular benefits

---

## Future Years Reminder

Every year, check:

- Did Amazon RSUs vest?
- Did I sell any shares?
- Did I receive dividends?
- Did I hold foreign shares on 31-Dec?
- Did I have a foreign brokerage account?

If yes, review Schedule FA.
