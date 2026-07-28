📈 Mutual Fund Investment Analytics Dashboard
> \*\*An end-to-end Business Intelligence solution built using Python, SQL
> Server and Power BI to automate mutual fund NAV collection, investment
> tracking and portfolio analytics.\*\*
---
📌 Project Overview
This project automates the complete lifecycle of mutual fund analytics.
Instead of manually checking daily NAVs and maintaining spreadsheets,
the solution:
Downloads daily NAV data from AMFI.
Stores historical NAV data in SQL Server.
Prevents duplicate NAV records.
Registers mutual fund transactions.
Calculates portfolio holdings automatically.
Provides interactive Power BI dashboards for investment decisions
and portfolio performance.
---
🎯 Business Problem
Investors often struggle to answer:
Should I invest today?
Is today's NAV lower than my SIP reference NAV?
Which funds are currently attractive to buy?
What is my portfolio worth today?
How much have I invested?
Which AMC or category has the highest allocation?
This project solves these questions through automation and analytics.
---
🏗 Solution Architecture
``` text
                 AMFI NAV Data
                      │
                      ▼
             download\_nav.py
                      │
                      ▼
               daily\_etl.py
                      │
                      ▼
              SQL Server Database
      ┌────────────┬──────────────┬──────────────┐
      │            │              │              │
 FundMaster    NAVHistory    Transactions     DimDate
      │            │              │              │
      └────────────┴──────────────┴──────────────┘
                      │
                      ▼
                Power BI Dashboard
            ┌────────────────────────┐
            │ Page 1 - Buy Signals   │
            │ Page 2 - Portfolio     │
            └────────────────────────┘
```
---
🛠 Technology Stack
Technology      Purpose
---
Power BI        Dashboard & Reporting
SQL Server      Data Storage
Python          ETL & Automation
Pandas          Data Processing
PyODBC          SQL Connectivity
AMFI NAV Data   Daily NAV Source
---
🗄 Database Design
Tables
FundMaster
Stores tracked mutual funds and configuration.
Fields include:
FundID
SchemeCode
FundName
AMC
FundCategory
ConfiguredSIPDay
AlertThreshold
---
NAVHistory
Stores daily historical NAV values.
Business Rules:
One NAV per Fund per Date.
Duplicate NAVs are prevented.
---
Transactions
Stores investment transactions.
Fields:
TransactionID
FundID
TransactionDate
TransactionType
Amount
NAV
Units
Business Rules:
Transaction allowed only if NAV exists.
Weekend and market holiday transactions are automatically rejected
because no NAV exists.
Units are calculated automatically using:
Units = Amount / NAV
---
DimDate
Calendar table used for reporting and time intelligence.
---
🐍 Python Utilities
download_nav.py
Responsibilities
Download NAV file from AMFI
Clean data
Return dataframe
---
daily_etl.py
Responsibilities
Download latest NAV
Read tracked funds
Filter required schemes
Insert new NAVs
Skip duplicates
Log ETL execution
---
register_fund.py
Registers new mutual funds.
Features
Fund Registration
SIP Day Configuration
Alert Threshold Configuration
---
register_transaction.py
Registers BUY / SELL transactions.
Workflow
``` text
Select Fund
      ↓
Enter Date
      ↓
Validate NAV
      ↓
Select BUY/SELL
      ↓
Enter Amount
      ↓
Calculate Units
      ↓
Preview Summary
      ↓
Insert Transaction
```
---
📊 Power BI Dashboard
Page 1 -- Buy Opportunity Dashboard
Purpose
Identify whether a fund should be bought based on configurable NAV
thresholds.
KPIs
Latest NAV Date
Total Funds
Buy Opportunities
Measures
Latest NAV
Month Start NAV
NAV Change %
Recommendation
Visuals
Recommendation Table
NAV Trend
Fund & AMC slicers
---
Page 2 -- Portfolio Performance
Purpose
Track current portfolio performance.
KPIs
Total Amount Invested
Total Units Held
Current Portfolio Value
Unrealized Gain / Loss
Portfolio Return %
Visuals
Investment by AMC
Investment by Category (Treemap)
Portfolio Holdings Table
Holdings Table includes
Fund Name
Invested Amount
Units
Average Buy NAV
Latest NAV
Current Value
Gain/Loss
Return %
---
📐 Important DAX Measures
Measure                   Purpose
---
Latest NAV                Latest available NAV for selected fund
Month Start NAV           First available NAV in current month
NAV Change %              Compare latest NAV with reference NAV
Recommendation            BUY / WAIT based on threshold
Average Buy NAV           Weighted average purchase NAV
Current Portfolio Value   SUMX(Units × Latest NAV)
Unrealized Gain/Loss      Current Value − Invested Amount
Portfolio Return %        Gain/Loss ÷ Invested Amount
---
📂 Project Structure
``` text
MutualFundInvestmentDashboard
│
├── Python
│   ├── download\_nav.py
│   ├── daily\_etl.py
│   ├── register\_fund.py
│   └── register\_transaction.py
│
├── SQL
│   ├── Database.sql
│   └── SampleData.sql
│
├── Power BI
│   └── MutualFundDashboard.pbix
│
├── Screenshots
│
└── README.md
```
---
🚀 How to Run
Clone repository.
Restore SQL Server database.
Configure SQL connection in Python scripts.
Run `download\_nav.py`.
Run `daily\_etl.py`.
Register funds.
Register transactions.
Refresh Power BI.
---
⭐ Key Features
Automated ETL Pipeline
Historical NAV Tracking
Duplicate NAV Prevention
Configurable Buy Recommendation
Transaction Registration Utility
Automatic Unit Calculation
Portfolio Analytics
Dynamic DAX Measures
Interactive Dashboards
---
📸 Dashboard Screenshots
Add screenshots here.
Page 1
![Page1](Screenshots/Page1.png)
Page 2
![Page2](Screenshots/Page2.png)
---
🚧 Future Enhancements
Live NAV API Integration
Power BI Service Scheduled Refresh
Email Notifications
SIP Automation
Portfolio Rebalancing
Sell Validation
Mobile Layout
---
📚 Skills Demonstrated
SQL Server Database Design
Python ETL Development
Data Cleaning
Data Modeling
DAX
Power BI Visualization
Business Analytics
Financial Reporting
---
💼 Resume Summary
Mutual Fund Investment Analytics Dashboard
Developed an end-to-end BI solution using Python, SQL Server and Power
BI. Automated NAV ingestion from AMFI, designed a normalized database,
implemented ETL with duplicate validation, built transaction management
utilities, and created interactive dashboards for buy recommendations
and portfolio performance using advanced DAX measures.
---
👨‍💻 Author
Vishal Surwase
If you found this repository useful, consider giving it a ⭐.
