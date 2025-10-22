# 🧠 IDS 702 Midterm Comprehensive Study Guide

---

## 📍 Unit 1: Statistics Fundamentals

### 1️⃣ Population vs. Sample
- **Population**: entire group of interest.  
- **Sample**: subset used to estimate population parameters.  
- **Goal**: draw *inferences* about the population using the sample.  
- Sampling introduces **sampling variability** — results change with different samples.

---

### 2️⃣ Inference vs. Prediction
| Type | Goal | Example |
|------|------|----------|
| **Inference** | Explain relationships / test hypotheses | Does smoking affect heart disease risk? |
| **Prediction** | Forecast outcomes | Predict next year’s CO₂ emissions |

---

### 3️⃣ Probability Concepts
- **Random variable (RV)**: numerical outcome of a random event.  
- **PMF/PDF**: functions giving probability (discrete) or density (continuous).  
- **Expected value (E[X])**: long-run average outcome.  
- **Variance (Var[X])**: spread around the mean.  
- **Joint probability**: Pr(A ∧ B)  
- **Conditional probability**: Pr(A | B) = Pr(A ∧ B)/Pr(B)  
- **Mutual exclusivity** ⇒ Pr(A ∧ B)=0.

---

### 4️⃣ Common Distributions
- **Binomial** → # of successes in n independent Bernoulli trials.  
- **Normal** → continuous symmetric “bell” curve; defined by μ, σ².  
- **Approximation**: for large n, Binomial ≈ Normal(μ = np, σ² = np(1 − p)).

---

### 5️⃣ Sampling Distributions & CLT
- **Sampling distribution**: distribution of a statistic (e.g., sample mean) over many samples.  
- **Central Limit Theorem (CLT)**: regardless of the population’s shape,  
  \[
  \bar{X} \sim N(\mu, \sigma^2/n)
  \]
  for large n.  
- **Standard deviation** vs. **standard error (SE)**:
  - SD = spread of individual data.
  - SE = spread of sample statistic (decreases ∝ 1/√n).

---

### 6️⃣ Maximum Likelihood Estimation (MLE)
1. Write the **likelihood** L(θ)=P(data | θ).  
2. Take log → log-likelihood.  
3. Differentiate w.r.t θ, set = 0 → solve θ̂.  
4. MLE has good properties (consistency, asymptotic normality).

Intuition: choose parameter θ that makes observed data most “likely.”

---

### 7️⃣ Confidence Intervals (CI)
- **Interpretation**: If we repeatedly sampled, ≈ 95 % of CIs would contain the true parameter.  
- **Affects width**: variability ↑ → CI wider; n ↑ → CI narrower; confidence ↑ → CI wider.  
- **Analytical** vs. **Bootstrap**:  
  - Analytical: use formulas & distribution assumptions.  
  - Bootstrap: resample data; compute empirical CI (no parametric assumption).

---

### 8️⃣ Hypothesis Testing
1. **Form hypotheses** H₀ vs Hₐ.  
2. **Compute test statistic** (t, z, χ², F).  
3. **Find p-value** = Pr(statistic ≥ observed | H₀ true).  
4. **Decision rule**: p < α → reject H₀.

**Types of tests**  
- *Parametric*: assume known distribution (t-test, z-test).  
- *Simulation-based*: permutation or bootstrap tests.  

**Two-sample logic**  
- Within-sample dependence → paired test.  
- Across-sample independence → independent-samples test.

---

## 📍 Unit 2: Linear Regression

---

### 1️⃣ Simple & Multiple Linear Regression

#### Model form
\[
y_i = \beta_0 + \beta_1 x_{i1} + \dots + \beta_p x_{ip} + \varepsilon_i
\]

#### Theoretical vs. Fitted
- *Theoretical model*: describes population relationship.  
- *Fitted model*: estimated from data via **OLS**.

#### Least Squares Idea
Minimize \( RSS = \sum (y_i - \hat{y_i})^2 \).  
OLS line minimizes squared residuals.

#### Interpretation
- **β̂j** = expected change in y for one-unit change in xj, holding others constant.  
- **p-value(β̂j)** → evidence predictor ≠ 0.  
- **CI(β̂j)** → range of plausible slope values.

---

### 2️⃣ Matrix Notation
\[
\mathbf{Y}=X\boldsymbol{\beta}+\varepsilon
\]
- X = n × p matrix (incl. intercept column of 1’s).  
- β = p × 1 vector of parameters.  
- ε = n × 1 vector of residuals.  
- OLS solution: β̂ = (XᵀX)⁻¹ XᵀY.

---

### 3️⃣ Categorical Predictors

- Convert factor with K levels → K − 1 dummy variables.  
- Choose a **reference (baseline)** category; coefficients compare each level to baseline.  
- **Interpretation:** β̂j = difference in mean Y between that level and baseline, holding others constant.  
- Avoid including all K dummies → *perfect multicollinearity*.

---

### 4️⃣ Interaction Terms

Model:
\[
Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + \beta_3(X_1X_2) + \varepsilon
\]
- The **interaction coefficient (β₃)** shows how the effect of X₁ changes across X₂.  
- If β₃ ≠ 0, the slope of X₁ depends on X₂.  
- *Use when*: theory or EDA suggests varying slopes by groups.

**Example**  
“Effect of dosage on anxiety differs by age group.”

---

### 5️⃣ Model Assessment

#### Coefficient of Determination (R²)
\[
R^2 = 1 - \frac{RSS}{TSS}
\]
Proportion of variance explained by the model.

#### Adjusted R²
Penalizes extra predictors:
\[
R^2_{adj} = 1 - (1 - R^2)\frac{n - 1}{n - p - 1}
\]

#### Interpreting R²
- High R² ≠ good model if assumptions fail.  
- Use adjusted R² for comparing models with different p.

---

### 6️⃣ Regression Assumptions

| Assumption | Diagnostic | Fix if Violated |
|-------------|-------------|----------------|
| **Linearity** | residuals vs fitted (no pattern) | add polynomial / log transform |
| **Independence** | residuals vs index (no trends) | change study design / use mixed model |
| **Normality** | Q–Q plot (points ≈ 45° line) | transform y or use robust inference |
| **Equal variance** | residuals vs fitted (no fan shape) | transform y or weighted least squares |

---

### 7️⃣ F-Test (Overall Model)

Tests whether **all slopes = 0**:
\[
H_0: \beta_1=\beta_2=\dots=\beta_p=0
\]
\[
F = \frac{MSR}{MSE} = \frac{(SSR/(p))}{(SSE/(n-p-1))}
\]
If F large → at least one predictor explains significant variance.

---

### 8️⃣ Nested F-Test (Partial F-Test)

Compares **full vs. reduced model**.

\[
F = \frac{(RSS_R - RSS_F)/(p_F - p_R)}{RSS_F/(n - p_F)}
\]

**Interpretation:**
- \(H_0:\) extra predictors = 0  
- Reject H₀ → added variables improve model fit.  
Used for sets of categorical dummy variables or interaction terms.

**In R:**  
```r
anova(reduced_model, full_model)
