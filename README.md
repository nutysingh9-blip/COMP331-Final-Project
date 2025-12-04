Project Overview

The project examines data quality issues in a retail data warehouse used for forecasting and strategic business planning. The warehouse contains:

Table	Description	Purpose
Sales (Fact)	Weekly sales by store & department	Forecasting, profitability tracking
Stores (Dimension-like)	Store characteristics (e.g., size, type)	Controls for physical attributes
Features (Dimension-like)	Economic conditions + promotions	Driver variables for sales

Maintaining strong data quality is critical because inaccurate or incomplete data can lead to poor forecasting, incorrect inventory decisions, and lost revenue. The analysis focuses on essential quality dimensions:
✔ Completeness
✔ Consistency
✔ Accuracy & Validity


COMP 331

2️⃣ Dataset Description

The dataset originates from the Walmart Sales Forecasting benchmark and includes 3 CSV tables covering 2010–2012.

Table	Rows	Notes
Sales	~421,000	Fact table
Features	~8,000	External indicators
Stores	45	Store metadata

These tables enable multi-year sales analysis using both internal and external retail drivers.


COMP 331

3️⃣ Methods & Tools

The analysis was performed using a data profiling approach, detecting quality issues across completeness, consistency, and validity dimensions.


COMP 331

4️⃣ Completeness Analysis

Results indicate highly variable missing values:

Variable Group	Missing %	Impact
Stores + Sales tables	0%	High reliability for core sales data
MarkDown1–5 (promotions)	50–64%	Weakens promotion effects analysis
CPI & Unemployment	7.14%	Reduces economic modeling accuracy

Conclusion: The Features table introduces major incompleteness risk — especially promotional pricing — which can mislead demand forecasting and pricing strategy.


COMP 331

5️⃣ Consistency Analysis

Key findings show that the relational structure is largely intact:

✔ 45 unique Store IDs exactly match across all tables
✔ Fact table grain: Store–Dept–Date keys are unique
✔ Dates mismatch: Features has more dates (182) than Sales (143) → missing indicator alignment
✘ After table joins, 270K–310K nulls remain for MarkDown fields

Business Impact: Forecasting models will consistently lack promotional inputs on many dates/stores, skewing revenue insights.


COMP 331

6️⃣ Accuracy & Validity

Checks revealed:

⚠ 1,285 negative sales values → violates business logic
⚠ 4,188 unrealistic temperature values → external data contamination
✔ CPI and unemployment fall within valid ranges
✔ Data types validated after transformation


COMP 331

These issues imply upstream ETL or data-entry errors, requiring cleansing rules (e.g., bounding logic, imputation strategies).

7️⃣ Overall Conclusion & Recommendations

The Sales and Stores tables are reliable, but Features carries major data quality risks:

Dimension	Risk Level	Key Concern
Completeness	🔴 High	MarkDown values missing >50%
Consistency	🟠 Medium	Time misalignment across tables
Accuracy/Validity	🟠 Medium	Negative sales + faulty temperatures
Recommended Improvements

Impute promotional variables using domain-based statistical methods

Filter or correct negative sales + extreme temperatures

Synchronize date coverage to ensure analytical consistency

Apply business rules validation during ETL processing

By improving these areas, forecasting and business decisions would become significantly more reliable.
