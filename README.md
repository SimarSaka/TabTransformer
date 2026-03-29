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

#### Key Advantages:
- Learns contextual relationships between features
- Outperforms traditional ML on structured categorical data

---

##  Objectives

- Identify **high-risk scenarios in roundabouts**
- Analyse **user perception vs actual risk factors**
- Predict:
  - Accident likelihood
  - Safety perception score

---


git clone https://github.com/your-username/roundabout-risk-analysis.git
cd roundabout-risk-analysis
