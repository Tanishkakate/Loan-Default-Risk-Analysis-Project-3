# Loan-Default-Risk-Analysis-Project-3

# Loan Default Risk Analysis (Python + MySQL + Power BI)

**Business question:** Which customer segments have the highest default rates, and which applications should the credit team manually review?

**Data:** Credit Risk Dataset (Kaggle). 32,409 loan applications after cleaning; overall default rate 21.87% (7,088 defaults).

## Tools
Python (pandas, cleaning), MySQL (segmentation and rule testing), Power BI (DAX, 2-page dashboard)

## Data preparation
- Removed duplicates and impossible values.
- Filled missing interest rates and employment length with medians.
- Loaded the cleaned file into MySQL and checked the row count and default rate against Python.

## Key findings
- Risk jumps at grade D: 59.1% default vs 20.8% for grade C. Grades D to G are 15% of loans but 42% of defaults.
- Loans above 30% of income default at 65.6%, vs 11.6% to 21.0% below that.
- Applicants earning under 30K default at 47.2%, vs 9.0% for 100K+.
- Renters default at 31.6%, vs 12.6% (mortgage) and 7.5% (own).
- A prior default on file roughly doubles risk (37.9% vs 18.4%).
- Grade D renters are the largest high-risk segment: 2,109 loans at 73.8%.

## Proposed manual-review rule
Flag a loan if grade is D to G **or** the loan is 30%+ of income.
- Flags 25.5% of applications (8,259 loans)
- 61.3% of flagged loans default (vs 21.9% overall)
- Catches 71.4% of all defaults

## Recommendations
1. Send loans meeting the rule to manual review, and test a stricter cap near 30% of income.
2. Apply tighter terms or lower limits for renters in grades D to F.
3. Treat a prior default on file as a risk flag.
4. Validate the rule on new data first.

## Limitations
- These are patterns, not causes. Loan grade is the lender's own risk rating.
- Single snapshot with no time dimension.
- The rule is untested on new data. About 39% of flagged loans don't default, and about 29% of defaults are missed.
- "Other" home ownership has only 106 loans, so don't over-read it.

## Dashboard
![Risk overview](<img width="1366" height="768" alt="Screenshot (307)" src="https://github.com/user-attachments/assets/abc5795c-c8c0-498e-94a9-50e6e66b4c52" />
)
![Risk segments](<img width="1366" height="768" alt="Screenshot (308)" src="https://github.com/user-attachments/assets/e4016a6d-d215-4af4-8a2e-d9f7e18140c7" />
)

## Repo contents
`python/` (cleaning) · `sql/` · `powerbi/loan_dashboard.pbix` · `screenshots/`
