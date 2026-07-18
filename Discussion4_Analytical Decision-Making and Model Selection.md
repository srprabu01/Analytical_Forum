# Analytical Decision-Making & Model Selection

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](#license) [![Made with R](https://img.shields.io/badge/Made%20with-R-blue)](#methods--tools-referenced) [![Focus: Applied Analytics](https://img.shields.io/badge/Focus-Applied%20Analytics-orange)](#overview)


This folder consolidates a set of **course discussion posts** into a single, report-style README on
**how analysts turn ambiguous business problems into evidence-backed decisions** — and on **choosing the
right level of model complexity** for the job.

> Why this write-up?
> - Move the emphasis from *"run a model"* to *"enable a decision."*
> - Capture a repeatable analytical workflow: frame → explore → test → communicate.
> - Argue, with references, for **interpretability and parsimony** as first-class objectives.


## Table of Contents
- [Overview](#overview)
- [Part 1 — Structured Problem-Solving When There Is No Clear Answer](#part-1--structured-problem-solving-when-there-is-no-clear-answer)
  - [Step 1: Frame the Problem & Align Stakeholders](#step-1-frame-the-problem--align-stakeholders)
  - [Step 2: Data Collection & Exploratory Data Analysis](#step-2-data-collection--exploratory-data-analysis)
  - [Step 3: Hypothesis Testing & Scenario Modelling](#step-3-hypothesis-testing--scenario-modelling)
  - [Step 4: Communicate the Findings](#step-4-communicate-the-findings)
- [Part 2 — When Simpler Models Win (Occam's Razor)](#part-2--when-simpler-models-win-occams-razor)
  - [The Case for Simplicity](#the-case-for-simplicity)
  - [Choosing the Right Approach](#choosing-the-right-approach)
- [Part 3 — Reflection: From "Run a Model" to "Enable a Decision"](#part-3--reflection-from-run-a-model-to-enable-a-decision)
- [Key Takeaways](#key-takeaways)
- [Methods & Tools Referenced](#methods--tools-referenced)
- [References](#references)
- [License](#license)


## Overview
In data science and analytics, it is common to face business challenges that lack a clean or definitive
resolution. Rather than offering a single "correct" answer, the analyst's role is to **reduce uncertainty,
surface trade-offs, and strengthen decision-making with empirical evidence**. These posts document a
practical, repeatable approach to doing exactly that — and a companion argument that **model complexity
should be earned, not assumed**.


## Part 1 — Structured Problem-Solving When There Is No Clear Answer

Not every problem has a tidy solution. A structured analytical approach — **problem framing, EDA,
hypothesis testing, and scenario modelling** — is what lets an analyst add value even when no ideal
answer exists.

### Step 1: Frame the Problem & Align Stakeholders
Executives often present issues that are broad or vague — *"Why are sales declining?"* The analyst's job
is to reframe these into quantifiable, data-driven questions, e.g. *"Which customer segments show the
largest sales decline, and what factors are associated with that behaviour?"* This stage also fixes
**success criteria, constraints, and assumptions** up front.

### Step 2: Data Collection & Exploratory Data Analysis
Compile the available internal and external datasets, evaluate their quality, and investigate
correlations, patterns, and anomalies using visualization tools such as **Tableau** or **matplotlib**.
EDA frequently *reshapes* the problem and uncovers hidden drivers.

### Step 3: Hypothesis Testing & Scenario Modelling
Use statistical methods (regression, p-values, confidence intervals) or simulations to assess candidate
explanations and outcomes. **Scenario analysis** is especially valuable when no ideal solution exists —
it hands executives a set of "what-if" alternatives rather than one brittle recommendation.

### Step 4: Communicate the Findings
Translate technical complexity into **actionable insight**, supported by visuals and narrative, so
decision-makers can act on evidence instead of drowning in detail.

> **Bottom line:** framing → EDA → testing → communication is a workflow that produces defensible
> decisions even when a "correct" answer is unavailable.


## Part 2 — When Simpler Models Win (Occam's Razor)

Advanced models offer powerful predictive capability, but their complexity carries real costs. Simpler
models are often the better choice when **interpretability, speed, and cost-effectiveness** matter most.

### The Case for Simplicity
- **Interpretability & trust.** In regulated settings such as finance and healthcare, "black box" deep
  networks are often avoided. Linear regression or a decision tree makes it clear *how* each variable
  drives the outcome, which builds trust and stakeholder buy-in.
- **Speed & cost.** Lower computational demands mean faster training and prediction — ideal for
  real-time use or frequently retrained models — and cheaper development and maintenance.
- **Robustness (less overfitting).** With fewer parameters, simple models are less prone to learning
  noise, so they often generalize better to new, unseen data.

### Choosing the Right Approach
Deciding whether an advanced technique is warranted means weighing several factors:

| Factor | Lean Simple | Lean Advanced |
| --- | --- | --- |
| **Problem complexity / accuracy need** | Roughly linear relationships; accuracy sufficient | Highly non-linear; top accuracy is the primary goal |
| **Data availability & quality** | Small, noisy, or incomplete data | Large, high-quality datasets |
| **Interpretability vs. accuracy** | Transparency is non-negotiable | Accuracy outweighs explainability |
| **Deployment & maintenance** | Limited infra / team expertise | Specialized skills and infrastructure available |
| **Cost & time constraints** | Tight budget or timeline | Resources support longer builds |

> **Occam's Razor for analytics:** all else equal, the simplest solution is usually the best. Start with
> a simple, interpretable baseline and add complexity **only when the added performance justifies** the
> loss of transparency.


## Part 3 — Reflection: From "Run a Model" to "Enable a Decision"

The biggest shift over recent weeks was moving from *"run a model"* to *"enable a decision"* — a
repeatable workflow: **disciplined EDA → transparent baseline → escalate only when evidence justifies →
a decision-ready narrative.**

**In practice:**
- Begin every project by profiling **data quality**, mapping **missingness**, and visualizing
  distributions and segment cuts to surface early signals and caveats.
- Fit a simple, interpretable **baseline** (linear or logistic) before exploring generalized linear
  models and regularization.
- Use **cross-validation** — the `cv.glmnet` pattern comparing **Ridge and LASSO** at `λ.min` vs.
  `λ.1se` — as the default for balancing bias, variance, and parsimony. LASSO in particular tames
  multicollinearity while yielding a compact, explainable feature set.

**Diagnostics are non-negotiable:**
- *Regression:* residual patterns, heteroscedasticity, **VIF**, and **Cook's distance**.
- *Classification:* confusion matrix, precision/recall, **ROC/AUC**, and threshold choices tied to
  **business costs**.
- Add lightweight **scenario & sensitivity analysis** (shift a key driver ±10%, stress-test
  assumptions) so stakeholders see trade-offs, not just point estimates.

**Communication template (one page):** context → key insight → recommended action → risks/mitigations →
ownership, with **one clear visual per message** (driver waterfall, coefficient path, or ROC curve).

The most useful thread was the bridge from **inference to prediction**: using **Chi-Square / ANOVA** to
scout meaningful relationships, then formalizing those signals via **GLMs and regularization** — a
coherent pipeline from *"is there something here?"* to *"how much does it matter, and what should we do?"*


## Key Takeaways
- Not every business problem has a clean answer; a **structured workflow** still produces defensible
  decisions.
- **Reframing** vague asks into measurable questions is the highest-leverage early step.
- **Scenario/sensitivity analysis** communicates trade-offs better than a single point estimate.
- **Parsimony is a feature:** simpler models buy interpretability, speed, cost savings, and robustness.
- Escalate to complex models **only when the evidence justifies** the added opacity and cost.
- **Diagnostics + a decision-ready narrative** are what make an analysis trustworthy and actionable.


## Methods & Tools Referenced
- **Languages/Tools:** R (`glmnet`, `cv.glmnet`), Python (`matplotlib`), Tableau.
- **Inference:** Chi-Square, ANOVA, t-tests, confidence intervals, p-values.
- **Modelling:** Linear & logistic regression, GLMs, Ridge/LASSO regularization.
- **Diagnostics:** VIF, Cook's distance, residual/heteroscedasticity checks; confusion matrix,
  precision/recall, ROC/AUC.
- **Decision tooling:** scenario analysis, ±10% sensitivity/stress testing, one-page decision template.


## References
- Forbes. (2018, October 25). *Five reasons why simple models are a data scientist's best friend.* Forbes.
- KDnuggets. (2020, March 12). *Are we undervaluing simple models?* KDnuggets.
- Mantel Group. (2023). *Basic analytics vs advanced analytics.* https://mantelgroup.com.au/basic-analytics-vs-advanced-analytics/
- Pecan AI. (2022, July 21). *Gaining a new perspective: Analytics vs. advanced analytics.* https://www.pecan.ai/blog/analytics-vs-advanced-analytics
- DataNorth AI. (2021). *Simple vs. intelligent data analytics: A guide to modern data analysis.* DataNorth AI.


## License
This project is released under the **MIT License**. See `LICENSE` for details.
