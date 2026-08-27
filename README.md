# Hotel Booking Cancellation & Revenue Risk Analysis

## From Booking Behavior to Business Action

An end-to-end data analytics project that analyzes hotel booking behavior, cancellation risk, and revenue exposure to identify high-risk booking segments and translate analytical findings into actionable business recommendations.

The project combines **Python, Exploratory Data Analysis (EDA), Statistical Analysis, K-Means Clustering, Feature Engineering, and Power BI** to understand not only how many bookings are cancelled, but also **which bookings are most exposed to cancellation risk and where the business should prioritize intervention.**

---

## 1. Business Background

In the hotel industry, booking cancellations create uncertainty for both occupancy planning and expected revenue.

A high cancellation rate alone, however, does not fully explain where the actual business risk comes from. Different bookings may have different cancellation probabilities, booking behaviors, customer histories, and financial values.

For example, a booking made far in advance may have a different cancellation risk compared with a last-minute booking. Similarly, a cancelled booking from a high-volume market segment may create a larger total revenue exposure even when its individual risk is not the highest.

Therefore, this project focuses on connecting:

**Booking Behavior → Cancellation Risk → Revenue Exposure → Booking Segmentation → Business Action**

---

## 2. Business Problem

The main business problem is that overall cancellation performance does not clearly identify:

- Which booking characteristics are associated with higher cancellation risk.
- Whether customer booking history is related to cancellation behavior.
- Which booking characteristics create higher revenue exposure.
- Which market segments contribute the most to cancelled-booking revenue exposure.
- Whether bookings can be grouped into distinct risk profiles.

Without this analysis, applying the same treatment to all bookings may result in inefficient monitoring and unnecessary intervention.

---

## 3. Problem Statements

This analysis addresses five main questions:

1. **What booking characteristics are most associated with cancellation risk?**

2. **How does customer booking history relate to the likelihood of cancellation?**

3. **How do lead time, deposit type, and market segment differentiate cancellation risk?**

4. **How large is the estimated revenue exposure from cancelled bookings, and which market segments contribute the most to this exposure?**

5. **Can bookings be grouped based on similar behavioral and booking characteristics to identify segments with different cancellation risk profiles?**

---

## 4. Business Objectives

The objectives of this project are to:

- Identify booking characteristics associated with cancellation.
- Analyze customer historical behavior related to cancellation.
- Measure estimated revenue exposure from cancelled bookings.
- Identify market segments with high revenue exposure.
- Develop booking segments based on similar characteristics.
- Identify high-risk booking segments that require greater attention.
- Provide targeted business recommendations based on risk and revenue exposure.

---

# 5. Dataset Understanding

## Dataset Overview

The project uses a hotel booking dataset containing information about hotel reservations, customer behavior, booking characteristics, and financial attributes.

### Original Dataset

- **Rows:** 119,390
- **Columns:** 32

After data cleaning and preprocessing, approximately **83K valid bookings** were used for the main analysis and Power BI dashboard.

---

## Main Data Categories

### Booking Information

Variables related to how and when a booking was made, including:

- Lead Time
- Arrival Information
- Stay Duration
- Booking Changes
- Number of Guests

### Customer History

Variables that describe previous customer behavior:

- Previous Bookings
- Previous Cancellations
- Historical Cancellation Rate
- Repeated Guest

### Booking Characteristics

Variables describing the type and source of booking:

- Deposit Type
- Market Segment
- Distribution Channel
- Customer Type
- Special Requests

### Financial Information

Variables used to estimate booking value and revenue exposure:

- ADR (Average Daily Rate)
- Estimated Revenue

### Booking Outcome

- Cancellation Status

---

# 6. Understanding Market Segments

One important variable in the analysis is **Market Segment**, which represents how the booking was acquired or categorized.

The dataset contains several market segments, including:

| Market Segment | Meaning |
|---|---|
| Online TA | Online Travel Agent — bookings made through online travel agency platforms |
| Offline TA/TO | Offline Travel Agent / Tour Operator — bookings arranged through traditional agents or tour operators |
| Groups | Bookings made as part of a group |
| Direct | Bookings made directly with the hotel |
| Corporate | Bookings associated with corporate customers |
| Aviation | Bookings related to aviation/airline business |
| Complementary | Complimentary bookings |

### Why is Market Segment important?

Market segment helps the business understand **where bookings are coming from and where cancellation-related revenue exposure is concentrated**.

For example, the analysis found that **Online TA** contributed the largest estimated revenue exposure from cancelled bookings, followed by **Groups** and **Offline TA/TO**.

This makes market segment useful not only for describing booking distribution, but also for determining where risk mitigation efforts may have the greatest financial relevance.

---

# 7. Data Processing

The dataset was processed using Python in Google Colab.

The main preprocessing stages included:

1. Data type validation.
2. Missing value inspection.
3. Duplicate and data consistency checks.
4. Handling invalid or irrelevant records.
5. Feature engineering.
6. Creation of booking-related categories.
7. Creation of estimated revenue-related variables.
8. Preparation of variables for statistical analysis.
9. Preparation of variables for clustering.
10. Exporting the processed dataset for Power BI.

The cleaned dataset was then used consistently across the analysis and Power BI dashboards.

---

# 8. Exploratory Data Analysis

EDA was conducted to identify patterns before applying statistical analysis and segmentation.

The analysis focused on:

- Cancellation rate across booking lead-time categories.
- Estimated revenue exposure by market segment.
- Customer booking behavior.
- Booking characteristics related to cancellation.
- Relationship between booking behavior and business impact.

---

## Key EDA Finding 1 — Lead Time and Cancellation

Cancellation risk increases as booking lead time becomes longer.

| Lead Time Category | Cancellation Rate |
|---|---:|
| Last Minute | 9.7% |
| Short Lead Time | 27.6% |
| Medium Lead Time | 37.6% |
| Long Lead Time | 44.7% |
| Very Long Lead Time | 56.8% |

The cancellation rate increases from **9.7% for Last Minute bookings to 56.8% for Very Long Lead Time bookings**.

This indicates that bookings made significantly earlier are associated with substantially higher cancellation risk.

---

## Key EDA Finding 2 — Revenue Exposure by Market Segment

Estimated revenue exposure from cancelled bookings is not evenly distributed across market segments.

The largest exposure comes from:

- **Online TA → approximately $7.1M**
- **Groups → approximately $1.9M**
- **Offline TA/TO → approximately $1.7M**
- **Direct → approximately $0.7M**

This indicates that cancellation risk should also be evaluated from a financial perspective rather than only by cancellation rate.

---

# 9. Statistical Analysis

Statistical analysis was used to support the patterns identified during EDA.

The analysis did not rely on a large number of statistical tests. Instead, tests were selected based on the business questions and the patterns that required further validation.

The purpose was to determine whether observed differences or relationships in cancellation behavior were sufficiently supported by the data.

The statistical analysis complements the EDA by moving from:

**"There appears to be a pattern."**

to:

**"The observed pattern has statistical support."**

---

# 10. Booking Segmentation

## Why Segmentation?

EDA showed that cancellation risk is not evenly distributed across all bookings.

However, analyzing individual variables separately does not fully explain whether certain bookings share a combination of high-risk characteristics.

Therefore, K-Means Clustering was applied to identify groups of bookings with similar behavioral and booking characteristics.

> The segmentation in this project refers to **booking segmentation**, based on booking and behavioral characteristics.

---

## Why K-Means?

K-Means was selected because:

- The segmentation does not require predefined labels.
- It groups observations based on similarity.
- It allows different booking risk profiles to emerge from the data.
- It supports business prioritization after the risk patterns are identified.

---

# 11. Cluster Selection

The optimal number of clusters was evaluated using:

- **Elbow Method**
- **Silhouette Score**

The analysis resulted in:

### Optimal Number of Clusters

**K = 2**

### Silhouette Score

**0.6198**

The result indicates that two clusters provide a reasonable separation of booking characteristics for the purpose of this analysis.

---

# 12. Segmentation Results

The clustering process produced two booking segments.

## Segment 1 — High-Risk & Revenue-Exposed Bookings

### Booking Share

**5.28%**

### Total Bookings

**4,397**

### Key Characteristics

- Cancellation Rate: **91.27%**
- Average Lead Time: **193.98 days**
- Average ADR: **$76.46**
- Previous Cancellations: **1.65**
- Historical Cancellation Rate: **91.99%**
- Average Stay: **2.77 nights**
- Revenue Exposure Rate: **94.88%**

### Business Interpretation

This segment represents a relatively small portion of total bookings but has a very high cancellation rate.

The segment is characterized by:

- Longer booking lead time.
- Strong historical cancellation behavior.
- High revenue exposure relative to its booking volume.

This makes the segment a priority for targeted risk monitoring.

---

## Segment 2 — Core & Relatively Lower-Risk Bookings

### Booking Share

**94.72%**

### Total Bookings

**78,896**

### Key Characteristics

- Cancellation Rate: **33.92%**
- Average Lead Time: **98.89 days**
- Average ADR: **$103.13**
- Previous Cancellations: **0**
- Historical Cancellation Rate: **0%**
- Average Stay: **3.47 nights**
- Revenue Exposure Rate: **37.20%**

### Business Interpretation

This segment represents the majority of bookings and has a relatively lower cancellation risk compared with the high-risk segment.

The absence of historical cancellation behavior suggests that this segment does not require the same level of intervention as the high-risk group.

---

# 13. Risk vs Revenue Exposure

One important finding from the segmentation analysis is that **risk rate and absolute revenue exposure are not the same thing**.

### High-Risk & Revenue-Exposed Bookings

- Booking share: **5.28%**
- Cancellation rate: **91.27%**
- Revenue exposure: approximately **$0.9M**

### Core & Relatively Lower-Risk Bookings

- Booking share: **94.72%**
- Cancellation rate: **33.92%**
- Revenue exposure: approximately **$10.7M**

This creates an important business distinction:

> **High-risk segment = highest cancellation probability**

while:

> **Core segment = larger absolute revenue exposure because of its much larger booking volume**

Therefore, business decisions should consider both **risk level and financial exposure**, rather than relying on cancellation rate alone.

---

# 14. Power BI Dashboard

The analytical findings were translated into an interactive Power BI dashboard consisting of three main perspectives.

## Dashboard 1 — Hotel Booking Performance & Cancellation Risk

This dashboard provides an overview of:

- Total Booking
- Cancellation Rate
- Estimated Revenue
- Revenue Exposure
- Median Lead Time
- Booking Outcome
- Revenue Exposure by Market Segment
- Cancellation Risk by Lead Time

### Main KPI

- **83K Total Booking**
- **37.0% Cancellation Rate**
- **$29.84M Estimated Revenue**
- **$11.66M Revenue Exposure**
- **69 Median Lead Time**

---

## Dashboard 2 — What Drives Cancellation Risk?

This dashboard focuses on behavioral signals associated with cancellation.

The analysis includes:

- Customer History vs Cancellation
- Deposit Type vs Cancellation
- Customer Type vs Cancellation
- Special Request vs Cancellation
- Lead Time vs Booking Value

The purpose is to help identify behavioral and booking characteristics associated with higher cancellation risk.

---

## Dashboard 3 — Customer Segmentation & Business Opportunity

This dashboard focuses on the resulting booking segments.

It includes:

- Booking Distribution by Segment
- Cancellation Risk by Segment
- Revenue Exposure by Segment
- Behavioral Profile by Segment
- Cancellation Risk Across Market Segments

The dashboard helps translate segmentation results into business priorities.

---

# 15. Key Business Insights

### 1. Cancellation risk increases significantly with lead time.

Very Long Lead Time bookings show a **56.8% cancellation rate**, compared with only **9.7% for Last Minute bookings**.

### 2. Revenue exposure is concentrated in several market segments.

Online TA contributes the largest estimated revenue exposure from cancelled bookings at approximately **$7.1M**.

### 3. Cancellation risk is strongly concentrated in the high-risk segment.

The High-Risk & Revenue-Exposed segment has a **91.27% cancellation rate**.

### 4. High risk does not always mean the largest absolute financial exposure.

Although the high-risk segment has a much higher cancellation rate, the Core segment has larger absolute revenue exposure because it represents the majority of bookings.

### 5. A single treatment for all bookings may not be efficient.

Different booking segments have different risk profiles, suggesting the need for a more targeted approach.

---

# 16. Business Recommendations

## 1. Prioritize High-Risk Bookings

Bookings with high historical cancellation behavior and long lead times should receive greater attention from the beginning of the booking lifecycle.

## 2. Apply Stronger Confirmation

High-risk bookings can receive more proactive confirmation, especially as the arrival date approaches.

## 3. Use Selective Deposit or Payment Policies

Deposit or payment commitment can be considered selectively for high-risk bookings rather than being applied to all customers.

## 4. Monitor High-Risk Market Segments

Within the High-Risk & Revenue-Exposed segment, market segments such as:

- Groups
- Offline TA/TO
- Online TA

show particularly high cancellation risk and can become priority areas for monitoring.

## 5. Protect Revenue Exposure

Risk prioritization should consider both cancellation probability and the financial value exposed by potential cancellation.

---

# 17. Business Impact

The analysis can support the business in several ways:

### Better Risk Prioritization

Instead of treating every booking equally, the business can focus resources on bookings with stronger risk signals.

### Revenue Protection

Revenue exposure provides an additional financial perspective when deciding which cancellation risks should be addressed first.

### Targeted Strategy

Confirmation, payment, and monitoring strategies can be adjusted according to booking risk characteristics.

### More Efficient Resource Allocation

The business can avoid applying intensive intervention to the entire booking population and instead focus on segments where intervention is more relevant.

---

# 18. Next Steps

The analysis can be translated into the following business actions:

### 1. Implement Risk-Based Monitoring

Use characteristics such as historical cancellation and long lead time as early risk indicators.

### 2. Test Targeted Interventions

Test stronger confirmation or selective deposit policies on high-risk bookings and compare the results with standard booking processes.

### 3. Prioritize High-Risk Market Segments

Start monitoring high-risk market segments such as Groups, Offline TA/TO, and Online TA.

### 4. Track Business Outcomes

Monitor changes in:

- Cancellation Rate
- Cancelled Bookings
- Revenue Exposure

after interventions are implemented.

### 5. Refine the Strategy

Use the results of the intervention to determine whether the strategy should be expanded, reduced, or adjusted for specific booking characteristics.

---

# 19. Tools & Technologies

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Scikit-learn**
- **Google Colab**
- **Power BI**
- **DAX**

---

# 20. Project Workflow

```text
Raw Hotel Booking Data
        ↓
Data Understanding
        ↓
Data Cleaning & Manipulation
        ↓
Feature Engineering
        ↓
Exploratory Data Analysis
        ↓
Statistical Analysis
        ↓
K-Means Clustering
        ↓
Booking Segmentation
        ↓
Revenue Exposure Analysis
        ↓
Power BI Dashboard
        ↓
Business Recommendation
