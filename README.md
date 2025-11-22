# Credit Strategy Optimization & Risk Analytics Dashboard

This project showcases an end-to-end workflow for analyzing credit risk, modeling probability of default (PD), evaluating underwriting strategies, and visualizing portfolio performance. It replicates the type of work performed by a Financial Data Science / Credit Strategy Analyst in a fintech or consumer lending environment.

## 📊 Project Overview

The goal of this project is to simulate a real-world lending workflow:
1. Generate a synthetic credit application dataset.
2. Train a probability-of-default (PD) model using Python.
3. Use SHAP explainability to interpret model behavior.
4. Simulate Champion vs. Challenger underwriting strategies.
5. Calculate approvals, defaults, expected losses, and profitability.
6. Load the results into Microsoft Access for reporting queries.
7. Build an interactive Power BI dashboard to visualize performance.

This project demonstrates the ability to:
- Work end-to-end across Python, SQL/Access, and Power BI.
- Design, test, and evaluate risk-based underwriting strategies.
- Translate ML output into business impacts (approval lift, loss mitigation, profitability).
- Build dashboards and KPI reporting used by credit strategy teams.

---

## 🧠 Key Features

### **1. Synthetic Credit Dataset Creation (Python)**
- 20,000 applicants with realistic features: credit score, DTI, income, utilization, delinquency history, bankruptcies, loan terms, and channels.
- Logistic-based probability model to generate true default outcomes.
- Exported to CSV for Access/BI ingestion.

### **2. Probability of Default (PD) Modeling**
- Gradient Boosting Classifier trained on risk features.
- Model performance evaluated via AUC and classification metrics.
- SHAP values generated to identify top risk drivers.
- Exported applicant-level PDs for strategy simulation.

### **3. Underwriting Strategy Simulation**
Two strategies were compared:
- **Strategy A:** Traditional rule-based underwriting (e.g., credit score ≥ 640, DTI ≤ 40%).
- **Strategy B:** Data-driven underwriting using PD thresholds.

Each strategy was evaluated on:
- Approval rate  
- Default rate (approved population)  
- Expected loss  
- Profitability  
- Risk distribution (PD segmentation)  

A Champion/Challenger A/B test was simulated to compare performance.

### **4. Microsoft Access Reporting Layer**
- Applicant-level data imported into Access.
- Queries created for core KPIs:
  - Approval rate
  - Default rate (approved only)
  - Expected loss
  - Total profit
  - PD segmentation (0–5%, 5–10%, 10–20%, etc.)
- Forms built to allow CSV import with a “Browse + Import” button.

### **5. Power BI Dashboard**
An interactive dashboard was created with:
- KPI cards (Approval %, Default %, Profit, Expected Loss, Avg Loan Amount)
- Approval & default rate comparison (Strategy A vs Strategy B)
- Profitability by strategy
- PD-band segmentation (volume, default rate, and profit)
- Slicers for product type, channel, and term

---

## 🧩 Technology Stack

- **Python:** pandas, numpy, scikit-learn, SHAP, scipy  
- **SQL / Access:** queries, import forms, Access UI  
- **Power BI:** interactive visuals, DAX measures, segmentation  
- **Tools:** Jupyter/Colab, Microsoft Access, Power BI Desktop  

---

## 📂 Folder Structure

