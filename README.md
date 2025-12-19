# 📊 Global AI & Data Science Job Market Analysis (2024-2030)

## 📝 Project Overview

This project provides a comprehensive analysis of the global AI and Data Science job market. By integrating **four distinct datasets**, I analyzed key metrics regarding compensation, skill demand, and the transformative impact of Generative AI (GenAI) on the workforce.

The dashboard offers a strategic view of current trends (2024) and future projections (up to 2030), helping stakeholders navigate the shift towards AI-driven roles.

---

## 📸 Dashboard Visuals

### 1. Market Overview & Compensation
<img width="1380" height="780" alt="Screenshot 2025-12-15 151707" src="https://github.com/user-attachments/assets/eacbee1f-b7f8-4eb2-83fe-e70cb796e48d" />
<img width="1378" height="783" alt="Screenshot 2025-12-15 151740" src="https://github.com/user-attachments/assets/8f16eb7d-958e-4bf7-943d-e1e76fc459f1" />


### 2. The Tech Ecosystem
<img width="1379" height="781" alt="Screenshot 2025-12-15 151855" src="https://github.com/user-attachments/assets/559622c2-1c1c-4c1f-aef2-7b96bb8a0cc3" />
<img width="1378" height="774" alt="Screenshot 2025-12-15 151916" src="https://github.com/user-attachments/assets/eb0874da-037a-4521-b3b7-b486e19d4ce6" />



### 3. Future Impact & Workforce
<img width="1370" height="769" alt="Screenshot 2025-12-15 151936" src="https://github.com/user-attachments/assets/8781a966-471b-43f4-ab35-f0efcbbbace2" />
<img width="1378" height="773" alt="Screenshot 2025-12-15 151954" src="https://github.com/user-attachments/assets/5199ffd9-6130-4654-b169-35c3bd0b2472" />



### 4. 🔍 Strategic Deep Dive
<img width="1262" height="704" alt="Screenshot 2025-12-19 133427" src="https://github.com/user-attachments/assets/7719d15d-7ecf-4388-b47f-eeb78316f5e7" />

| *Decomposition Tree identifying high-risk career paths* |

---

## 🔍 Key Insights & Data Story

### 1. The "Degree Trap" in Tech (Critical Insight)
Using Root Cause Analysis (Decomposition Tree), I uncovered a critical vulnerability in the **Finance & Legal sector**:
* While the sector has a moderate average automation risk (**57.06**), **AI** roles within it jump to a **66.76** risk score.
* From the tree analysis suggests that entry-level, theoretical tasks are highly susceptible to automation compared to specialized, experience-based roles.

### 2. Market & Compensation Trends
* **Hybrid Work Dominance:** The industry has shifted significantly, with **58%** of roles offering hybrid work and **23%** offering remote models.
* **Top Earners:** **Machine Learning** roles command the highest average salary ($134K). The **Analytics Engineering Manager** stands out as the highest-paying individual contributor role (~$203K).
* **Skill Value:** Proficiency in **Reinforcement Learning** and **TensorFlow** correlates with higher median salaries compared to standard SQL/R skills.

### 3. The GenAI Disruption
* **Productivity vs. Risk:** GenAI adoption is driving an **18% productivity increase** and is projected to create **2 Million new roles**. However, it brings a moderate automation risk (48.6%) to existing workflows.
* **Industry Leaders:** The **Consumer & Services** and **Technology** sectors are leading the charge, creating over **800K new GenAI-driven roles** combined.

### 4. Future Outlook (2030)
* **Growth Roles:** **Data Processing Manager** is identified as a top growing role for 2030.
* **Future-Proofing:** The dashboard maps roles against "Automation Risk" vs. "Projected Openings." Roles with high projected openings but lower automation scores represent the safest career bets for the next decade.

---

## ⚙️ Data Preparation & Modeling Strategy

The core challenge of this project was integrating **4 distinct, disjointed datasets** with varying schemas, inconsistent naming conventions (e.g., "US" vs. "United States"), and messy multi-value columns.

To solve this, I designed a **Star Schema** architecture to enable seamless cross-filtering.

### 1. Dimensional Modeling (The "900 to 6" Solution)
To unify the data, I created centralized Dimension tables to filter across all four fact tables:

| Dimension | The Challenge | The Solution (ETL) |
| :--- | :--- | :--- |
| **Dim_Location** | Source files used mixed formats (ISO Codes vs. Full Names). | Created a master reference list by appending all sources and standardizing abbreviations via **Power Query (M)** to create a single `Country` key. |
| **Dim_JobCategory** | **900+ unique job titles** (e.g., "Staff Data Scientist", "Lead AI Engineer") made analysis impossible. | Engineered conditional logic to categorize these into **6 strategic buckets** (Data Science, AI, ML, Data Engineering, Analyst, Finance). |
| **Dim_Industry** | 15+ niche industry names that fragmented the visuals. | Grouped industries into **5 "Super-Sectors"** (Tech, Finance, Healthcare, Industrial, Consumer) for broader trend analysis. |

### 2. Advanced Transformations (Power Query)
**The Multi-Value Problem:**
The `skills_required` column contained comma-separated string values in a single cell (e.g., *"Python, SQL, AWS"*). This prevented granular analysis.

* **Strategy:** Created a bridge table (`Fact_Job_Skills`).
* **Transformation:** Used **Split Column by Delimiter (Rows)** to normalize the data, turning one row into multiple rows while preserving the `job_id`.
* **Enrichment:** Added conditional columns to categorize skills (e.g., tagging "LangChain" as a "GenAI Tool").

### 3. The Data Model
The final model utilizes a **Star Schema** with **One-to-Many (1:*)** relationships:
* **Central Dimensions:** `Dim_Location`, `Dim_JobCategory`, `Dim_Industry` filter all 4 datasets simultaneously.
* **Bridge Connections:** The `ai_job_market` table connects to `Fact_Job_Skills` via the normalized `job_id`, allowing for many-to-many analysis between jobs and specific tools.

---

## 🛠️ Tools & Technologies
* **Data Visualization:** Microsoft Power BI (Decomposition Trees, Scatter Plots, Dynamic Slicers)
* **Data Engineering:** Power Query (M Language) for ETL and Data Cleaning.
* **Analysis:** DAX (Data Analysis Expressions) for measures like `YoY Growth` and `Weighted Average Risk`.
* **Data Sources:** Aggregated datasets from Kaggle and Industry Reports.

## 🚀 How to Use
1.  Download the `job_analysis_dashboard.pbix` file from this repository.
2.  Open using **Microsoft Power BI Desktop**.
