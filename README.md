
***Household Loan Default Prediction Using NSSO & SECC Data***

**Project Overview**

Loan defaults are a growing concern in India, particularly in rural and semi-urban areas where access to formal credit is limited. Traditional credit scoring often ignores socio-economic realities that strongly influence repayment behavior.

This project integrates publicly available datasets:

NSSO Household Loan Data (loan-level household records)

SECC (Socio-Economic and Caste Census) District-Level Data (assets, deprivation, education, land, caste, etc.)

We build a machine learning framework to:

Predict household-level loan default risk

Provide transparent & interpretable insights using SHAP

Enable natural language explanations via LLMs + RAG

**Data Sources**

NSSO Household Loan Data (Unit-level records)

Contains detailed information on households with one or multiple loans

Loan attributes: amount, tenure, interest rate, purpose, source of credit, repayment status

SECC Datasets (District-Level)

Household asset ownership

Land ownership

Income profile & income sources

Socio-economic deprivation indicators

Caste & tribal composition

Educational profile

Household summary statistics

Optional Additional Data

District-level shapefiles / GeoJSON for loan default hotspot mapping

***Pipeline Steps***

**1. Data Extraction & Loading**

Downloaded SECC CSVs from government portals.

Loaded NSSO Household Loan CSV.

Ensured proper column naming & type consistency.

**2. Data Cleaning**

Removed duplicates & invalid records.

Standardized district names across NSSO & SECC datasets.

Converted categorical codes (loan purpose, source of credit) into human-readable categories.

Handled missing values: median imputation for numerics, "Unknown" for categoricals.

**3. Merging Datasets**

Household-level (NSSO) joined with District-level (SECC) on "District Name".

Strategy for multiple loans per household:

Aggregated to household level using:

Max outstanding amount

Average interest rate

Most frequent loan purpose

Preserved loan-level records for robustness checks.

**4. Exploratory Data Analysis (EDA**)

Loan Default Distribution (~24% default rate – balanced enough for ML).

Financial Indicators: higher interest rates, shorter tenure, and large loan size → more defaults.

Socio-Economic Indicators (SECC):

Higher % landless households → more defaults

Casual labor/agriculture income → higher defaults vs salaried

Secondary education in household → protective against default

Geographic Hotspots: mapped district-wise default % to identify clusters in Bihar, UP, Odisha.

**5. Geographic Hotspot Mapping**

District-wise loan default % visualized on India GeoJSON maps.

Identified policy intervention zones (clusters in Eastern India).

**6. Feature Engineering**

Derived household-level aggregates (loan-to-income ratio, weighted average interest rate).

Created socio-economic ratios (literacy %, land ownership %, deprivation index).

Encoded categorical features (loan purpose, caste, income source).

Scaled numeric features (StandardScaler).

**7. Model Building**

Train-test split (70-30).

Models tested:

Logistic Regression (baseline, interpretable)

Random Forest (non-linear patterns)

XGBoost (best accuracy & explainability)

Evaluation Metrics: AUC, Accuracy, Precision-Recall, F1-score.

**8. Explainability**

SHAP (SHapley Values):

Identified top drivers of loan default:

High interest rate

Landlessness

Casual labor as main income source

Low education attainment

Natural Language Explanations (LLM-powered):

Used GPT/Claude to turn SHAP insights into plain-language narratives.

Example:

"This household has a high risk of default mainly because their income comes from casual labor and they lack land ownership, making repayment less stable."

**9. RAG-based Interactive Query System (Future Work)**

Developed a Retrieval-Augmented Generation (RAG) prototype.

Allows credit officers to ask:

"Which districts have the highest defaults among landless households?"

"Why is repayment risk higher in agricultural households in Bihar?"

Returns natural language insights + supporting tables/graphs.
