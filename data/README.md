# Data Documentation

## General Insurance Capital & Risk Modelling

### 1. Data Source

This project uses the French Motor Third-Party Liability (MTPL) datasets
`freMTPL2freq` and `freMTPL2sev` distributed through the CASdatasets R package.

CASdatasets is a collection of insurance datasets developed for actuarial
science research, teaching and modelling.

The package is maintained by Christophe Dutang and Arthur Charpentier.

Dataset repository:
https://github.com/dutangc/CASdatasets

CASdatasets documentation:
https://dutangc.github.io/CASdatasets/

Dataset DOI:
10.57745/P0KHAG

---

## 2. Dataset Description

The data represent French Motor Third-Party Liability insurance experience
for approximately 677,991 policies, observed mostly over one year.

The underlying experience covers approximately 2011–2013.

Two related datasets are used.

### `freMTPL2freq`

Policy-level frequency dataset containing:

- Policy identifier (`IDpol`)
- Number of claims (`ClaimNb`)
- Exposure in years (`Exposure`)
- Vehicle power (`VehPower`)
- Vehicle age (`VehAge`)
- Driver age (`DrivAge`)
- Bonus-Malus level (`BonusMalus`)
- Vehicle brand (`VehBrand`)
- Fuel type (`VehGas`)
- Area (`Area`)
- Population density (`Density`)
- Region (`Region`)

The working dataset contains:

- 677,991 policy records
- 12 variables

### `freMTPL2sev`

Claim-level severity dataset containing:

- Policy identifier (`IDpol`)
- Individual claim amount (`ClaimAmount`)

The working dataset contains:

- 26,444 claim records
- 2 variables

Multiple rows for the same policy may represent multiple claims and therefore
must not automatically be treated as duplicate observations.

---

## 3. Raw Data

The original R data files are preserved unchanged in:

data/raw/

Files:

- `freMTPL2freq.rda`
- `freMTPL2sev.rda`

The raw files are retained to preserve the original source data and provide
an auditable link between the source and the analytical datasets.

Raw source files will not be modified during the project.

---

## 4. Processed Data

For analysis in Python, the original R datasets were loaded and converted
to CSV format.

The converted files are stored in:

data/processed/

Files:

- `freMTPL2freq.csv`
- `freMTPL2sev.csv`

The conversion changes the storage format only. No analytical filtering,
winsorisation, capping, imputation or removal of observations was performed
as part of the conversion.

Any subsequent modelling transformations will be documented explicitly in
the relevant analytical notebook.

---

## 5. Data Validation

A formal data-quality assessment is documented in:

notebooks/01_data_quality_audit.ipynb

The audit includes:

- dataset structure and completeness;
- missing-value assessment;
- duplicate investigation;
- frequency/severity reconciliation;
- numerical range validation;
- categorical-variable validation;
- exposure validation;
- claim-frequency validation; and
- investigation of extreme claim amounts.

A key reconciliation test confirmed that the claim counts represented in
the severity data agree with the policy-level `ClaimNb` values across all
677,991 policy records.

---

## 6. Important Data Considerations

The severity distribution is strongly right-skewed and contains a small
number of very large claims. These observations are retained because
extreme losses are directly relevant to insurance risk and capital modelling.

Some claim amounts in the underlying dataset may reflect fixed amounts
arising from French insurance claims settlement conventions.

These characteristics will be considered when selecting and validating
severity and tail-risk models.

---

## 7. Role of the Data in This Project

The historical data provide the empirical basis for:

- claim-frequency modelling;
- claim-severity modelling;
- tail-risk assessment; and
- estimation of parameters used in aggregate-loss simulation.

Historical observations will not be presented as simulated outcomes.

Where actuarial assumptions are required for capital modelling,
diversification or stress testing, those assumptions will be documented
separately from the observed data.

---

## 8. Citation and Licence

CASdatasets should be cited as:

Christophe Dutang and Arthur Charpentier (2026),
CASdatasets: Insurance datasets,
R package version 1.2-1.
DOI: 10.57745/P0KHAG.

The CASdatasets R package is distributed under GPL (>= 2).

The associated research data repository identifies the dataset under
the Etalab Open License 2.0.

Users of this repository should consult the original CASdatasets
documentation and data repository for the authoritative licence and
reuse conditions.

---

## 9. Reproducibility Principle

The project follows the Anthony Utulu Analytics standard of maintaining a
clear distinction between:

Observed Data → Estimated Parameters → Actuarial Assumptions →
Simulated Outcomes → Management Scenarios

This distinction will be maintained throughout the capital and risk
modelling workflow.
