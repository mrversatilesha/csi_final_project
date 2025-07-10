# Generic Continuous Data Ingestion & Conditional Processing using Azure Data Factory
[📽️ Watch Demo Video](https://drive.google.com/file/d/143u6-td5RY-SwvUT-vOuwsZd3ZzXIdh6/view?usp=sharing)

---

## 📌 Project Overview

This project demonstrates a robust Azure Data Factory (ADF) setup for:

- 🔄 **Continuous ingestion of REST API data from multiple sources** (India, US, UK, China, Russia)
- 🧠 **Conditional execution of pipelines** based on dynamic thresholds (record counts)
- ☁️ **Storing results in Azure Data Lake Storage Gen2 (ADLS)**
- 🔁 **Running pipelines automatically twice a day**

The solution includes both **static ingestion pipelines** and **dynamic condition-triggered pipelines**, ideal for enterprise-level ETL workflows.

---

## 🧱 Architecture Summary

### ✅ 1. Country Data Export Pipeline

Fetches and stores country-level metadata from the [RESTCountries API](https://restcountries.com).

- REST Linked Services: 5 (India, US, UK, China, Russia)
- Datasets: 5 (one per country)
- `ForEach` loop + `Switch` logic to route per country
- Copy Activity writes each country’s data to: /data-export/{country}.json
- - Runs at: **12:00 AM and 12:00 PM IST**

---

### ✅ 2. Conditional Customer & Product Data Pipeline

Simulates a dynamic system that:
- Calls an external API for customer data
- Checks if record count > 500:
- If yes: dumps data to ADLS and calls the child product pipeline
- In the child pipeline, if record count > 600:
- Simulates further downstream actions (e.g., product data processing)

Uses:
- **Parent-child pipelines**
- **If Conditions**
- **Dynamic expressions**
- **Parameter passing**

---

## 🗃️ Technologies Used

- Azure Data Factory (ADF)
- Azure Data Lake Storage Gen2
- REST APIs (`restcountries.com`, `randomuser.me`)
- JSON Expressions
- Scheduled Triggers
- Web & Copy Activities
- ForEach + Switch + If Condition logic

---

## 🧪 How It Works

### 🌍 Country Data Pipeline:
1. Loops through: `["india", "us", "uk", "china", "russia"]`
2. For each country:
 - Calls REST API
 - Stores JSON in ADLS under `data-export/`

### 👥 Conditional Pipeline:
1. Pulls 1000 random users
2. If count > 500:
 - Stores to ADLS
 - Calls product pipeline
3. In Product pipeline, if count > 600:
 - Proceeds with simulated product processing

---

## 🕓 Scheduling

- **Country pipeline runs twice daily** via scheduled trigger (12 AM & 12 PM IST)
- **Conditional pipeline can be triggered manually or scheduled as needed**

---

## 📽️ Demo Video

Click below to watch the full working demo of the pipeline:

▶️ [Watch the Demo](https://drive.google.com/file/d/143u6-td5RY-SwvUT-vOuwsZd3ZzXIdh6/view?usp=sharing)

---

## 📈 Potential Use Cases

- Real-time API data ingestion for dashboards
- Scalable ETL framework for customer/product pipelines
- Workflow automation with thresholds
- Educational demo of ADF advanced features

---

## ✅ Outcome

This project showcases how Azure Data Factory can be used to build:
- Modular, scalable, and reusable pipelines
- Time-based and condition-based automation
- Intelligent control flow using ADF's expressions and triggers

---

  
