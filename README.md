# Stat 156 Final Project

**Replication and Re-Analysis of Gelber (2011): How Do 401(k)s Affect Saving?**
Keval Amin & Stephanie Quiroz
University of California, Berkeley

---

## 📌 Project Overview

This repository contains our final project for **STAT 156 (Causal Inference)** at UC Berkeley.

We replicate and extend:

> Gelber, Alexander (2011). *How Do 401(k)s Affect Saving?*

The core research question:

> **Does eligibility for a 401(k) increase household saving, or does it simply shift assets across accounts?**

This question is difficult because individuals who prefer saving may self-select into jobs offering 401(k)s. Gelber solves this using **tenure-based eligibility rules** as a quasi-natural experiment. We replicate his approach and extend it using causal inference methods learned in class.

---

## 🎯 What We Contribute

Our project adds three main contributions:

### 1️⃣ Data Reconstruction

We reconstruct the dataset directly from raw SIPP survey files instead of using the author’s cleaned dataset.

We create three analytic samples:

* **Raw** – Fully reconstructed from raw SIPP
* **Raw Aligned** – Uses author eligibility flags for alignment
* **Replication** – Built from official replication files

This allows us to test sensitivity to data construction.

---

### 2️⃣ Replication of Main Results

We replicate Gelber’s regression:

[
Y_i = \alpha + \tau \cdot \text{Eligible}_i + f(\text{Age}_i) + X_i'\beta + \varepsilon_i
]

where the outcome is a **second difference in log assets**:

[
Y_i =
\log(A_{12}+10) - 2\log(A_{9}+10) + \log(A_{6}+10)
]

This measures whether asset growth accelerates after eligibility.

Our replication confirms:

* Large positive effects on **401(k) assets**
* Positive effect on **IRA assets**
* Little evidence of crowd-out of other financial assets
* Decline in car accumulation

The qualitative conclusions match the original paper.

---

### 3️⃣ New Causal Methods (Not in Original Paper)

We extend the analysis using:

#### 🔹 Nearest-Neighbor Matching (ATT)

Balances treated and control units on observed covariates.

#### 🔹 Doubly Robust AIPW Estimator (ATT)

Consistent if either:

* The propensity score model is correct, OR
* The outcome regression is correct.

#### 🔹 Rosenbaum Sensitivity Analysis

Quantifies how strong hidden bias would need to be to overturn results.

Main insight:

* Results are robust across estimators.
* However, Rosenbaum bounds show **moderate sensitivity to unobserved confounding**.

---

## 📁 Repository Structure

```
.
├── Analysis/              # Quarto analysis files (.qmd)
├── Tables/                # Generated regression tables
├── code/                  # Helper functions and renv.lock
├── data/raw/              # Raw SIPP data (not tracked if large)
├── renv/                  # R dependency management
├── Stat_156_Fina_(12).pdf # Final paper
└── README.md
```

---

## 📊 Main Results Summary

Across all samples and estimators:

* 401(k) eligibility increases retirement saving.
* IRA balances increase (crowd-in).
* Other assets and debt show little systematic response.
* Effects are stable across Raw, Aligned, and Replication samples.
* Hidden bias of Γ ≈ 1.05–1.10 could overturn significance.

---

## 🧠 Identification Strategy

Treatment:
Becoming eligible for a 401(k) due to tenure rules.

Key assumption:

> Conditional on observed covariates, timing of eligibility is independent of potential outcomes.

This is a **quasi-natural experiment**, not a randomized trial.

---

## 🛠 Methods Implemented

| Method                  | Estimand                        | Why Used                            |
| ----------------------- | ------------------------------- | ----------------------------------- |
| OLS (paper replication) | ATE-like regression coefficient | Direct replication                  |
| Matching                | ATT                             | Design-based causal comparison      |
| Doubly Robust AIPW      | ATT                             | Protection against misspecification |
| Rosenbaum Bounds        | Sensitivity                     | Hidden bias robustness              |

---

## ⚙️ Reproducing the Project

### 1️⃣ Clone Repository

```bash
git clone <repo-url>
cd <repo-name>
```

### 2️⃣ Restore R Environment

We use `renv` for reproducibility:

```r
install.packages("renv")
renv::restore()
```

### 3️⃣ Run Analyses

Main analysis files:

* `Analysis/table1.qmd`
* `Analysis/table2_raw.qmd`
* `Analysis/table3.qmd`
* `Analysis/matching_reanalyse.qmd`
* `Analysis/Doubly Robust.qmd`
* `Analysis/Rosenbaum.qmd`

Render with:

```r
quarto render Analysis/filename.qmd
```

---

## 📚 Data

Data source:

* **Survey of Income and Program Participation (SIPP)**

We merge:

* Waves 3, 6, 9, 12 (Topical Modules)
* Wave 7 (Core demographic file)

Sample restrictions:

* Age 22–64
* First year at firm
* Firm offers 401(k)
* For-profit firms
* Non-missing covariates

---

## 📄 Final Paper

The full paper is available here:

📄 **[Download Final Paper](Stat_156_Fina_%2812%29.pdf)**
Or view directly in this repository.

You can also reference the uploaded version here: 

---

## 📈 Key Takeaways

* 401(k) eligibility increases total saving.
* Little evidence of full crowd-out.
* Results robust to alternative estimators.
* Sensitivity analysis suggests moderate vulnerability to hidden bias.
* Matching and DR estimators confirm OLS patterns.

---

## 🎥 Project Video

Presentation video:
[https://drive.google.com/file/d/1Q1Z2s8VzEUjAv3gd6JEvfmk1xE4uzkoa/view](https://drive.google.com/file/d/1Q1Z2s8VzEUjAv3gd6JEvfmk1xE4uzkoa/view)

---

## 👥 Authors

**Keval Amin**
UC Berkeley / Sciences Po Paris
[keval.amin@berkeley.edu](mailto:keval.amin@berkeley.edu)

**Stephanie Quiroz**
UC Berkeley

---

## 📖 Course Context

STAT 156 – Causal Inference
University of California, Berkeley

This project demonstrates:

* Data reconstruction from raw survey files
* Replication credibility
* Application of modern causal inference methods
* Sensitivity analysis for unobserved confounding
