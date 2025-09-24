Kaletch Underwriting Suite v2.6
The Kaletch Underwriting Suite v2.6 is an institutional-grade real estate private equity (REPE) underwriting tool designed for modeling value-add, core-plus, and core investment strategies. Built as a single-page web application using HTML, JavaScript, and Tailwind CSS, it provides a robust, user-friendly interface for calculating capital stacks, cash flows, partnership waterfalls, internal rates of return (IRR), equity multiples (MOIC), and CSV exports. The suite is optimized for performance, accuracy, and flexibility, making it suitable for institutional investors, asset managers, and developers.
Features

Modular Calculation Engine: Computes capital stack, monthly cash flows, scenario analysis, waterfall distributions, IRR, and MOIC with high precision.
Dynamic Presets: Supports Value-Add, Core-Plus, and Core deal types with preconfigured assumptions and a confirmation dialog to prevent accidental overwrites.
Waterfall Modeling: Configurable partnership waterfall via JSON, supporting preferred returns, return of capital, GP catch-up, and final splits.
Sensitivity Analysis: Visualizes Project IRR across exit cap rates and hold periods.
Formatted Outputs: Generates readable CSV exports with sanitized filenames and a polished UI with Chart.js visualizations.
Robust Validation: Handles edge cases (e.g., zero equity, underwater exits, 100% vacancy) with clear alerts and no crashes.
Market Benchmarks: Displays property-type-specific IRR ranges (sourced from 2025 market reports, e.g., CBRE).
Accessibility: Includes sr-only labels and print-optimized layouts for inclusivity and reporting.

Installation

Clone the Repository:git clone https://github.com/KALETECH999/kaletch-underwriting-suite.git


Open the Application:
Navigate to the project directory and open index.html in a modern web browser (e.g., Chrome, Firefox).
No server setup is required, as the application runs entirely client-side.



Usage

Input Assumptions:
Enter deal parameters in the left panel (e.g., purchase price, units, rent, financing terms).
Select a preset (Value-Add, Core-Plus, Core) or customize inputs. Changing inputs reverts the preset to "Custom."
Optionally define a partnership waterfall in JSON format (e.g., [{"name": "Preferred Return", "type": "pref", "rate": 8.0}, ...]).


Run Calculations:
Click "Run Underwriting" to compute results, including Project IRR, MOIC, capital stack, and cash flows.
View outputs in the Dashboard (summary, charts), Pro Forma (annual cash flows), or Sensitivity Analysis (IRR table).


Export or Print:
Click "Export CSV" to download a formatted pro forma (<PropertyName>_pro_forma.csv).
Click "Print" for a clean, stakeholder-ready report (excludes input panel).


Reset or Restore:
Click "Reset" to restore default Value-Add assumptions.
Click "Restore Default" to reset the waterfall JSON.



Example Inputs (Value-Add Default)

Property & Acquisition:
Property Name: The Landmark
Property Type: Multifamily
Purchase Price: $50,000,000
Units: 250
Closing Costs: 2.5%


Value-Add Renovations:
Renovation Budget: $15,000/unit
Reno Completion: 12 months
Post-Reno Rent Premium: 15%


Financing:
Loan-to-Cost: 65%
Interest Rate: 4.5%
Amortization: 30 years
Interest-Only Period: 24 months
Financing Fees: 1.0%


Operations & Revenue:
Starting Rent: $1,500/month
Vacancy Rate: 5.0%
Rent Growth: 3.0%/year
OpEx Ratio: 40% of Year 1 PGI
OpEx Growth: 2.5%/year
Stabilized CapEx: $250/unit/year


Exit & Partnership:
Hold Period: 5 years
Exit Cap Rate: 4.75%
Terminal Growth Rate: 3.0%
Cost of Sale: 1.5%
LP Equity Share: 90%


Waterfall JSON (Default):[
  { "name": "1. Preferred Return", "type": "pref", "rate": 8.0 },
  { "name": "2. Return of Capital", "type": "returnOfCapital" },
  { "name": "3. GP Catch-up", "type": "catchup", "gpShare": 100 },
  { "name": "4. Final Split", "type": "split", "lp": 80, "gp": 20 }
]



Example Outputs (Value-Add Default)

Executive Summary:
Project IRR: ~20.9%
Equity Multiple: ~2.44x
Total Equity Required: ~$20.38M
Exit Value: ~$76.90M


Partnership Returns:
LP IRR: ~19.4%
GP IRR: ~31.1%
LP Multiple: ~2.28x
GP Multiple: ~3.62x


Waterfall Distribution:
LP Preferred Return: ~$7.31M
LP Capital: ~$17.65M
GP Capital: ~$1.96M
GP Catch-up: ~$1.83M
Final Split (80/20): ~$4.49M


Capital Stack:
Senior Debt: $35.63M (65% LTC)
LP Equity: $18.34M (90% of equity)
GP Equity: $2.04M (10% of equity)



Key Calculations

Capital Stack:
Total Project Cost = Purchase Price + Renovation Budget + Closing Costs + Financing Fees
Senior Loan = Total Project Cost × Loan-to-Cost
Equity Required = Total Project Cost - Senior Loan
LP Equity = Equity Required × LP Share
GP Equity = Equity Required × (1 - LP Share)


Cash Flows:
Monthly PGI = Units × Current Rent (with post-reno premium after completion)
EGI = PGI × (1 - Vacancy Rate)
OpEx = Year 1 PGI × OpEx Ratio, grown annually
NOI = EGI - OpEx
Debt Service = Interest + Principal (post I/O period)
Levered CF = NOI - CapEx - Debt Service


Exit Value:
Forward NOI = Final Year NOI × (1 + Terminal Growth Rate)
Gross Exit Value = Forward NOI / Exit Cap Rate
Net Sale Proceeds = Gross Exit Value - Cost of Sale - Final Loan Balance


IRR:
Computed using Newton-Raphson method for project, LP, and GP cash flows.
Project CFs: [-Equity Required, Annual Levered CFs, Net Sale Proceeds]
LP/GP CFs: [-LP/GP Equity, Annual LP/GP Distributions]


Waterfall:
Processes tiers sequentially (pref, return of capital, catch-up, split).
Preferred return compounds annually at specified rate (e.g., 8%).
Catch-up targets GP profit to match final split ratio.



Edge Cases Handled

Zero Equity (LP Share = 100%): GP IRR/MOIC = N/A; LP IRR calculated normally.
Underwater Exit (Negative Proceeds): Distributions stop at partial pref; alerts triggered.
High Vacancy (100%): NOI = 0; negative IRR handled gracefully.
Short/Long Holds: Validates hold ≥ 1 year; supports up to 10 years with compounding pref.
Invalid Waterfall JSON: Disables partnership sections; project-level metrics unaffected.

Performance

Calculation Time: <100ms for default scenarios.
CSV Export: Instantaneous with sanitized filenames.
UI Updates: Seamless with no lag.

Known Limitations

Monthly Granularity: Rent premium is monthly, but debt service and capex are annually aggregated. This has minimal impact (~0.1% IRR variance) for typical holds.
Hardcoded Benchmarks: IRR ranges (e.g., Multifamily: 15-20%) are sourced from 2025 market reports but not dynamically updated. API integration could enhance accuracy.
Documentation: Assumes users refer to this README for formulas and usage. Additional in-app tooltips could improve onboarding.

Contributing
Contributions are welcome! Please:

Fork the repository.
Create a feature branch (git checkout -b feature/YourFeature).
Commit changes (git commit -m 'Add YourFeature').
Push to the branch (git push origin feature/YourFeature).
Open a pull request.

Report bugs or suggest features via GitHub Issues or email kaletech.ai@gmail.com.
Contact

Email: kaletech.ai@gmail.com or gautam.kale1999@gmail.com
GitHub: KALETECH999
LinkedIn: Gautam Kale

License
© 2025 Gautam Kale. All rights reserved. This project is licensed under the MIT License. See the LICENSE file for details.
