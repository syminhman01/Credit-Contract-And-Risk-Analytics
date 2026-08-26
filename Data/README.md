# Dataset Documentation

This folder documents the datasets used in the **Credit Contract Portfolio & Risk Analytics** project.

The raw banking data is not included in this repository.  
The dataset is used for academic and portfolio purposes.

---

## 1. Dataset Overview

The project uses a relational banking dataset containing information about:

- Credit contracts
- Loan repayment schedules
- Actual repayment transactions
- Customers
- Branches
- Regions
- Industries
- Disbursement plans
- Collateral
- Credit products and lending classifications

The analytical model is mainly centered around the credit contract lifecycle:

Credit Disbursement  
→ Outstanding Balance  
→ Scheduled Repayment  
→ Actual Repayment  
→ Overdue Exposure  
→ Portfolio Risk

---

## 2. Main Tables

| Table | Description | Main Analytical Role |
|---|---|---|
| `HOPDONG_TINDUNG` | Stores credit contract information including contract ID, customer, disbursement date, maturity date, loan amount, term, and interest rate | Main credit contract table |
| `KE_HOACH_TRA_NO` | Stores scheduled repayment obligations by contract and repayment period | Scheduled principal and interest obligations |
| `KHACHHANG_TRANO` | Stores actual repayment transactions including repayment date, principal paid, and interest paid | Actual repayment analysis |
| `KEHOACH_GIAINGAN` | Stores branch-level quarterly disbursement targets | KPI and target analysis |
| `KHACHHANG` | Stores customer information | Customer dimension |
| `CHINHANH` | Stores branch information | Branch analysis |
| `KHUVUC` | Stores regional classification | Regional analysis |
| `NGANHNGHE_KINHTE_CAP01` | Level 1 economic industry classification | Industry concentration analysis |
| `NGANHNGHE_KINHTE_CAP02` | Level 2 economic industry classification | Detailed industry analysis |
| `NGANHNGHE_KINHTE_CAP03` | Level 3 economic industry classification | Detailed industry analysis |
| `TAISAN_BAODAM` | Stores collateral information linked to credit exposure | Collateral and exposure analysis |
| `DateTable` | Calendar table used for time intelligence | Reporting date and trend analysis |
| `Dim_Thoigian_KPI` | Defines KPI reporting periods | Quarterly KPI analysis |
| `Dim_Aging` | Defines overdue aging buckets | Overdue aging analysis |

---

## 3. Main Data Grain

Understanding the grain of each table is important because the model contains multiple fact-like tables.

| Table | Data Grain |
|---|---|
| `HOPDONG_TINDUNG` | One row per credit contract |
| `KE_HOACH_TRA_NO` | One row per credit contract and repayment period |
| `KHACHHANG_TRANO` | One row per repayment transaction |
| `KEHOACH_GIAINGAN` | One row per branch and reporting period |
| `KHACHHANG` | One row per customer |
| `CHINHANH` | One row per branch |

The main relationship structure is conceptually:

```text
                    CHINHANH
                        |
                        |
KHACHHANG ------ HOPDONG_TINDUNG
                        |
                -------------------
                |                 |
                v                 v
       KE_HOACH_TRA_NO     KHACHHANG_TRANO
       Repayment Plan      Actual Repayment
