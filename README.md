# TabTransformer
# Roundabout Risk Perception Analysis 🚦

## Overview
This project analyses **risk perception and behaviour at roundabouts** using survey data collected from respondents.  
It combines **categorical encoding, statistical insights, and machine learning (TabTransformer)** to understand factors influencing accident risk and safety perception.

---


---

##  Dataset Description

The dataset is based on a structured survey covering:

### 1. Demographics
- Gender
- Age group
- Driving experience
- Vehicle type
- Occupation
- Education level

Example encoding:
- Gender → Female (1), Male (2) :contentReference[oaicite:0]{index=0}  
- Age → >50 (1), 36–50 (2), 26–35 (3), 18–25 (4), <18 (5) :contentReference[oaicite:1]{index=1}  

---

### 2. Behavioural & Knowledge Questions
- Yielding rules
- Speed control at entry/exit
- Indicator usage
- Emergency handling

These are encoded as **nominal categorical variables**. :contentReference[oaicite:2]{index=2}  

---

### 3. Risk Perception (Ordinal Data)
- Risk during entry, circulation, exit
- Safety for different users (drivers, pedestrians, cyclists)
- Multi-lane vs single-lane risk

Example scale:
- Very High (5) → Very Low (1) :contentReference[oaicite:3]{index=3}  

---

### 4. Accident & Safety Insights
- Type of accident
- Location (entry, merging, circulating, exit)
- Causes (overspeeding, lane change, distraction, etc.)

---

##  Data Preprocessing

### Encoding Strategy
- **Nominal Variables → Label Encoding / One-Hot Encoding**
- **Ordinal Variables → Ordered Numerical Encoding**
- Missing values handled via:
  - Mode (categorical)
  - Median (numerical if applicable)

---

##  Model Used

### TabTransformer
- Designed for **tabular data with categorical features**
- Handles high-cardinality categorical variables effectively
- Trained for **1000 epochs**

##  Results & Model Performance

### Training Progress
The TabTransformer shows stable learning behaviour across epochs.

- Both **training loss** and **validation loss** decrease sharply in the initial epochs and then gradually stabilise.
- Final values converge near:
  - **Training Loss:** ~6.3
  - **Validation Loss:** ~6.6
- The small gap between the two curves suggests **good generalisation** and limited overfitting.

  ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)
  

**Interpretation:**  
The model is able to learn meaningful feature interactions from the survey-based tabular dataset without excessively memorising the training set.

---

### Confusion Matrix Insights

The confusion matrices below are shown as **row-wise percentages of the true class**, which makes it easier to interpret how well each actual risk level is being identified.

---

### 1. Risk While Entering the Roundabout
- **Very Low Risk (1):** classified correctly in **100%** of cases
- **Very High Risk (5):** classified correctly in **95.65%** of cases
- **Moderate Risk (3):** often confused with **High Risk (4)**

  ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)

**Insight:**  
The model performs strongly for extreme risk levels, while middle categories show overlap due to similar behavioural patterns.

---

### 2. Risk While Circulating Within the Roundabout
- **Very High Risk (5):** classified correctly in **100%** of cases
- **Low Risk (2):** classified correctly in **73.21%** of cases
- **Moderate Risk (3)** and **High Risk (4)** show substantial confusion

  ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)

**Insight:**  
The circulating phase appears to be one of the most complex stages, where distinctions between moderate and high perceived risk are harder to capture.

---

### 3. Risk While Exiting the Roundabout
- **Very Low Risk (1):** classified correctly in **100%** of cases
- **Very High Risk (5):** classified correctly in **81.82%** of cases
- **Low**, **Moderate**, and **High** classes show greater dispersion across neighbouring categories

  ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)

**Insight:**  
Exit manoeuvres may involve abrupt decisions, lane shifts, and mixed driver behaviour, making this stage harder to predict consistently.

---

### 4. Risk in Single-Lane Roundabouts
- **Very Low Risk (1):** **100%**
- **Very High Risk (5):** **100%**
- **High Risk (4):** **63.83%**
- Moderate confusion exists among **Low**, **Moderate**, and **High** classes

  ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)

**Insight:**  
The model performs relatively well in single-lane scenarios, likely because these environments are structurally simpler and behaviour is less variable.

---

### 5. Risk in Double-Lane Roundabouts
- **Very Low Risk (1):** **100%**
- **Moderate Risk (3):** **53.33%**
- **High Risk (4):** **67.94%**
- **Very High Risk (5):** **100%**

![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)

**Insight:**  
Performance remains strong in double-lane settings, though lower-risk classes still exhibit some confusion due to increased manoeuvring complexity.

---

### 6. Risk in Multi-Lane Roundabouts
- **Very Low Risk (1):** **100%**
- **Low Risk (2):** **92.45%**
- **Moderate Risk (3):** **51.92%**
- **Very High Risk (5):** **68.57%**
- **High Risk (4):** only **26.67%** correctly classified

  ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)

**Insight:**  
Multi-lane roundabouts are the most behaviourally complex, leading to greater class overlap and lower model confidence, especially in higher-risk categories.

---

### 7. Risk with Increased Traffic
- **Low Risk (2):** **84.21%**
- **Moderate Risk (3):** **50.91%**
- **High Risk (4):** **42.21%**
- **Very High Risk (5):** **81.82%**
- **Very Low Risk (1)** is fully shifted toward **Low Risk (2)**

  ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)

**Insight:**  
As traffic increases, perceived risk becomes less cleanly separable, especially in the middle classes. This suggests that traffic density introduces non-linear and context-dependent effects.

---

### 8. Overall Opinion on Roundabout Safety
- **Very Low Risk (1):** **96.88%**
- **High Risk (4):** **100%**
- **Very High Risk (5):** entirely predicted as **High Risk (4)**
- **Low** and **Moderate** opinions show notable mixing

  ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)
  

##  Feature Interaction & Attention Analysis

###  Global Feature Interaction (Attention Matrix)

The feature interaction attention matrix visualises how the TabTransformer assigns importance across all feature pairs.

**Key Observations:**

- Attention values are **densely distributed (~0.06–0.08 range)**, indicating:
  - No single feature dominates the model
  - The model relies on **distributed learning across multiple inputs**

- Subtle hotspots suggest higher interactions between:
  - **Traffic-related variables** (speed breakers, signage, road markings)
  - **Behavioural features** (indicator usage, yielding behaviour)
  - **Accident-related variables** (type, cause, consequence)

**Interpretation:**
- The model captures **complex, multi-dimensional relationships** rather than relying on isolated predictors  
- Risk perception is influenced by a **combination of infrastructure, behaviour, and context**

---

###  Target-Focused Attention (Top Feature Contributions)

The second matrix highlights **top contributing features for each prediction target**.

---

### Risk Prediction Insights

#### 1. Risk Entering
- Strong influence from:
  - **Chance of accident (~0.31)**
  - **Faced accident/near accident (~0.22)**
  - **Speed breakers (~0.19)**

**Insight:**  
Entry risk is driven by both **past experience** and **physical traffic calming measures**.

---

#### 2. Risk Circulating
- Key contributors:
  - **Chance of accident (~0.31)**
  - **Speed breakers (~0.19)**
  - **Road lighting (~0.15)**

**Insight:**  
Circulation risk depends on **environmental visibility + infrastructure design**.

---

#### 3. Risk Exiting
- Influenced by:
  - **Chance of accident (~0.31)**
  - **Object hazard signs (~0.27)**
  - **Speed breakers (~0.19)**

**Insight:**  
Exit risk is sensitive to **hazard awareness and control elements**.

---

###  Lane-Based Risk

#### Single-Lane
- Moderate distributed attention across:
  - Behavioural + signage features

#### Double-Lane
- Stronger influence of:
  - **Lane markings (~0.21)**
  - **Traffic signage**

#### Multi-Lane
- More complex pattern:
  - Attention spread across multiple features
  - No dominant predictor

**Insight:**  
As lane complexity increases, **feature importance becomes more distributed**, reflecting real-world uncertainty.

---

###  Traffic & Safety Perception

#### Increased Traffic Risk
- Strong signals from:
  - **Chance of accident (~0.31)**
  - **Vehicle category (~0.22)**
  - **Occupation (~0.21)**
 
    ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)
    ![image alt](https://github.com/SimarSaka/Industrial_Training/blob/main/WhatsApp%20Image%202025-12-04%20at%201.43.04%20AM.jpeg?raw=true)

**Insight:**  
Traffic risk perception is influenced by **user profile + experience level**, not just infrastructure.

---

#### Overall Safety Opinion
- Influenced by:
  - **Chance of accident (~0.31)**
  - **Car safety perception (~0.31)**
  - **Past accident experience (~0.22)**

**Insight:**  
Overall opinion is largely **experience-driven rather than purely objective**.

---

###  Model Behaviour Summary

- The model uses **contextual feature interactions**, not isolated variables  
- **Accident history and perceived risk variables** consistently show high importance  
- **Infrastructure elements (signs, markings, lighting)** act as secondary modifiers  
- Socio-demographic features (vehicle type, occupation) contribute in **traffic-related scenarios**

---


##  Conclusion

The attention analysis validates that the model is not treating the problem as a simple classification task, but rather as a **context-aware decision system**, where multiple weak signals combine to influence predictions.

This aligns well with real-world traffic behaviour, where risk perception is inherently **subjective, situational, and interaction-driven**.



