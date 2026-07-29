# Olist E-Commerce Analytics — Power BI Portfolio Project

**Customer Behavior, Sales Performance & Delivery Analysis for a Brazilian E-Commerce Marketplace**

---

##  Project Overview

A fast-growing e-commerce company needs to understand customer behavior, product performance, and operational efficiency to make data-driven decisions on retention, marketing spend, and logistics. This project analyzes real transactional data from **Olist**, a major Brazilian e-commerce marketplace, to answer that need end-to-end — from raw, messy relational data to a polished, decision-ready Power BI report.

**Role:** Data Analyst
**Deliverables:** Data cleaning, data modeling, DAX analysis, customer segmentation, and a 3-page Power BI dashboard with business recommendations.

---

##  Dataset

**[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)** — ~100K real orders (2016–2018) across 8 relational tables:

`orders` · `order_items` · `customers` · `order_payments` · `order_reviews` · `products` · `sellers` · `product_category_name_translation`

---

##  Tools & Skills Used

- **Power BI Desktop** — data modeling, report design
- **Power Query (M)** — data cleaning, merging, transformation
- **DAX** — 20+ measures, calculated columns, and a calculated RFM segmentation table
- **Data modeling** — star schema design across 8 relational tables

---

##  What This Project Involved

- Cleaned and merged 8 relational source tables into a proper star schema
- Diagnosed and fixed real data-quality issues, including:
  - A broken date relationship caused by timestamp/date type mismatches
  - The distinction between `customer_id` (per-order) and `customer_unique_id` (per-person) — critical for accurate repeat-customer analysis
  - A missing calendar dimension, built manually via Power Query
- Built **20+ DAX measures** covering sales, growth trends, customer value, and delivery/satisfaction metrics
- Designed a **calculated RFM (Recency, Frequency, Monetary) table** to segment ~96,000 customers into behavioral groups
- Deliberately scoped the report to **3 focused pages** instead of a chart-dump — every visual maps directly to a specific business question

---

##  Report Structure

### Page 1 — Sales & Category Performance
*Audience: Commercial / Marketing leadership*
Answers: which categories drive revenue, which underperform, are there seasonal trends, and where should regional marketing investment go.

**Key visuals:** Top 10 & bottom 10 categories by revenue, monthly revenue trend, revenue-by-state matrix with conditional formatting.

### Page 2 — Customer Segmentation & Value
** RMF Analysis **
Answers: who are the most valuable customers, and can they be segmented by behavior.

**Key visuals:** RFM-based segment breakdown, Frequency-vs-Monetary scatter plot, top-20 customer table.

### Page 3 — Delivery Performance & Satisfaction
*Audience: Operations leadership*
Answers: do delivery delays affect customer reviews, and how severely.

**Key visuals:** Late-vs-on-time review score comparison, review score by delay severity, delivery time trend.

---

##  Key Findings

**Sales & Regional Investment**
- **R$15.84M** total revenue across **99K orders**, averaging **R$159.33** per order
- `health_beauty`, `watches_gifts`, and `bed_bath_table` are the top revenue-generating categories — the strongest candidates for continued marketing investment
- Revenue is heavily concentrated in **São Paulo**, followed by **Rio de Janeiro** and **Minas Gerais**; São Paulo may already be near-saturated, making the second-tier states the stronger *incremental* investment targets

**Customer Retention**
- Only **3.12%** of customers ever place a second order — retention, not acquisition, is the company's biggest growth lever
- **69% of the customer base (66,182 customers)** has drifted into an "At Risk / Lost" segment
- Just **389 customers (0.4%)** qualify as high-value "Champions" — a small, targetable group for loyalty initiatives

**Delivery & Satisfaction**
- Average review score is **4.09**, but drops to **2.27** for late-delivered orders — nearly a 2-point swing on a 5-point scale
- Only **6.57%** of orders arrive late, yet this small group causes outsized damage to overall satisfaction
- Satisfaction degrades progressively with delay severity, not just at a single "late" cutoff — meaning reducing *any* delay (not only eliminating it) has measurable value

---

##  Report Preview

Report can be previewed from the .png files attached or download the PowerBI through the given link.

---

##  Known Limitations

Being transparent about scope and constraints:

- **RFM segmentation thresholds** (order count, spend, and recency windows) were set as reasonable business starting points and validated against the resulting distribution — not statistically derived.
- **Recency is measured against the dataset's own last order date (~Oct 2018)**, not the current date, since the dataset is historical. Using `TODAY()` would make every customer appear equally "old."
- **Regional and category investment recommendations use revenue concentration as a proxy** for where to invest. True ROI-based targeting would require marketing spend and conversion data not included in this dataset.
- **Delivery delay and review score show a strong correlation, not proven causation** — other factors (packaging, wrong items, seller issues) may independently contribute to both.

---

##  How to Explore

Download `Olist Reports.pbix` and open in Power BI Desktop, or view the published report here: *[insert Power BI Service link if published]*

---

**Author:** [Mohammed Muqtadir Ahmed]
**Connect:** [https://linkedin.com/in/mohammed-muqtadir-ahmed]   · [mohd.muqtadir.ahmed@outlook.com]
