# 📈 Measuring ROI on Sponsored Search Ads – A Causal Inference Study

This project uses a **natural experiment and Difference-in-Differences (DiD) regression** to estimate the **causal ROI** of branded keyword advertising at Bazaar.com. A temporary suspension of Google ads allowed for a quasi-experimental analysis, distinguishing actual incremental traffic from cannibalized organic visits.

> 📁 Part of **MSBA 6441 – Causal Inference** (Spring 2025) at the University of Minnesota

---

## 🧠 Case Background

- **Company**: Bazaar.com (e-commerce retailer)
- **Scenario**: Technical glitch paused *branded search ads* on Google for weeks 10–12
- **Platforms Involved**:
  - **Treated**: Google (ad suspension)
  - **Control**: Bing, Yahoo, Ask (ads ran uninterrupted)
- **Goal**: Estimate the true Return on Investment (ROI) of branded search ads

Case based on Columbia Business School's case:  
📄 *“Measuring ROI on Sponsored Search Ads”* by Kinshuk Jerath

---

## 📊 Key Questions Addressed

### 1️⃣ What's Wrong with the Naive ROI Calculation?

Bob calculated ROI as if **all paid clicks were incremental**, ignoring that users might have clicked the **organic result anyway**. This overstates the ROI. A proper causal estimate requires accounting for substitution behavior.

### 2️⃣ Defining Treatment & Control

- **Unit of Analysis**: Platform-week
- **Treated Unit**: Google
- **Control Units**: Yahoo, Bing, Ask
- **Treatment Period**: Weeks 10–12
- **Variables**:
  - `treated`: 1 if Google, 0 otherwise
  - `post`: 1 if week ≥ 10, 0 otherwise
  - `did`: Interaction term for DiD

### 3️⃣ First Difference (Pre-Post on Google)

Estimated a simple regression on Google traffic before and after the outage.

- ❌ Result: ~0.13% change (not significant)
- ⚠️ Issue: Ignores time trends and external shocks; unreliable as a causal estimate

### 4️⃣ Difference-in-Differences (DiD) Model

Used a **fixed effects panel regression** on log-transformed total traffic across all platforms.

- **Treatment Effect**: -1.116 (log units)
- **Converted to %**: **~67% drop in traffic** due to removing branded ads
- ✅ Statistically significant (p < 0.001)
- ✔️ Parallel trends assumption validated

### 5️⃣ Corrected ROI Estimate

Using actual data and DiD results:

- **Week 9 Sponsored Clicks**: 12,681
- **Estimated Incremental Traffic**: 8,522 clicks (from -67.2% drop)
- **Conversion Rate**: 12%
- **Margin per Conversion**: $21
- **Cost per Click**: $0.60

**📈 Final ROI**: **182.24%**

> For every $1 spent on ads, Bazaar.com earned $2.82 in revenue, netting $1.82 in profit.

---

## 📂 Files
```
bazaar-search-roi-analysis/
├── Casual_HW3.Rmd # Full RMarkdown analysis script
├── Casual_HW3.pdf # Rendered report
├── Assignment 3 Instructions.docx # Instructions and prompt
├── Measing ROI on Sponsored Search Ads.pdf # Columbia case
└── README.md # This file
```
---

## 📦 Tools & Libraries

- **R**, with:
  - `dplyr`, `ggplot2` – Data wrangling & visualization
  - `plm` – Panel data regression
  - `lm`, `exp()` – Causal interpretation
- **Methodology**:
  - Difference-in-Differences
  - Fixed Effects Panel Model
  - Log transformation for skewed distributions

---

## 👥 Authors

- **Ujjwal Khanna**
- **Aurosikha Mohanty**

---

## 📚 Reference

- Columbia CaseWorks (CU181): *Measuring ROI on Sponsored Search Ads*
- Blake, Nosko, & Tadelis (2015), *Econometrica*

---
