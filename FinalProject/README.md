# GreenStream Energy - Smart Meter ETL Design
## Selected Topics Course - Final Project

This project involves the conceptual design of a **Serverless ETL (Extract, Transform, Load) Pipeline** for **GreenStream Energy**, a smart-utility provider.

## 📄 Project Resources
*   **[Lec-Task.pdf](./Lec-Task.pdf)**: Case study description and requirements.
*   **[Selected_Topics_Course_Lecture_Task.pdf](./Selected_Topics_Course_Lecture_Task.pdf)**: Final submission containing the architecture design, transformation logic, and lifecycle analysis.

---

## 🏢 Case Study: GreenStream Energy

GreenStream Energy collects electricity usage data from **50,000 households** via smart meters. Despite collecting valid data, it remains "dark data" stored but not transformed into actionable insights.

### 🚩 The Problem
The raw smart-meter data suffers from several data quality issues:
*   **Inconsistent Units**: Some meters report in Watts (W), others in Kilowatts (kW).
*   **Missing Data**: Gaps in time series due to connectivity outages.
*   **Format**: Data arrives in non-optimized CSV format.
*   **Goal**: The company needs to identify peak consumption, detect faulty meters, and prepare data for predictive analytics.

---

## 🏗️ Proposed Solution

The project focuses on designing an automated, serverless pipeline to Clean, Validate, Store, and Archive this data.

### 1. Business Rules & Transformation Logic
The design implements specific rules to standardize the data:
*   **Unit Standardization**: Automatically converts all "W" readings to "kW" (divide by 1000).
*   **Missing Values**: Records with NULL readings are flagged and excluded from peak-usage calculations but kept for completeness.
*   **Data Validation**: Rejects records with negative values or invalid timestamps.
*   **Fault Detection**: Identifies "potentially faulty" meters if zero consumption is reported for an unusually long period (e.g., 24+ hours).

### 2. Single Record Lifecycle
The data flow for a single smart-meter record is defined as:
1.  **Upload**: Raw CSV upload preserves auditability.
2.  **Trigger**: Orchestration workflow initiates transformation.
3.  **Clean & Validate**: Sequential checks for units, nulls, and anomalies.
4.  **Structured Storage**: Validated data is stored in a query-ready database (RDS) for fast analytics.
5.  **Archival**: Data is converted to **Parquet** format for long-term historical analysis and forecasting.

### 3. Failure Strategy
*   **Transient Failures**: Automatic retry mechanisms.
*   **Data Violations**: Invalid records are routed to a "Quarantine" storage for deeper inspection without breaking the pipeline.
*   **System Failure**: Pipeline stops to prevent data corruption.

---

## 👨‍💻 Author

**Abdelrahman Ahmed Eldaba**
*   Data Scientist • Web Developer • Python Enthusiast
*   [GitHub Profile](https://github.com/Abdelrahman47-code)
*   [LinkedIn](https://www.linkedin.com/in/abdelrahmaneldaba/)
*   [Portfolio Website](https://sites.google.com/view/abdelrahman-eldaba110)
