# 🚨 Real-Time Fraud Detection System — Azure

## Overview
A real-time phone call fraud detection pipeline built using Microsoft Azure services.  
The system detects fraudulent calls by identifying when the same user makes calls from two different countries within 5 seconds — which is physically impossible.

## Live Dashboard
![Fraud Detection Dashboard](screenshots/dashboard.png)

---

## Architecture
```
TelcoGenerator → Azure Event Hub → Azure Stream Analytics → Power BI Dashboard
(Fake Calls)      (Data Ingestion)   (Fraud Detection Query)  (Live Visualization)
```

---

## Technologies Used
- **Azure Event Hubs** — Real-time data ingestion
- **Azure Stream Analytics** — Real-time fraud detection using SQL queries
- **Microsoft Power BI** — Live dashboard visualization
- **SQL** — Stream Analytics fraud detection query
- **TelcoGenerator** — Sample phone call data generator

---

## How Fraud is Detected
```sql
Same User (CallingIMSI)
+
Within 5 seconds
+
Different Country (SwitchNum different)
= FRAUD DETECTED 🚨
```
If a person calls from USA and Australia within 5 seconds — that's impossible. The system flags it as fraud instantly.

---

## Project Structure
```
fraud-detection-azure/
│
├── README.md                        ← Project description
├── .gitignore                       ← Secrets excluded
├── queries/
│   └── fraud_detection.sql         ← Fraud detection query
├── config/
│   └── telcodatagen.exe.config     ← App config (no secrets)
└── screenshots/
    └── dashboard.png               ← Live Power BI dashboard
```

---

## Setup Steps

### Step 1 — Azure Event Hub
1. Go to Azure Portal → Search "Event Hubs"
2. Create Namespace → Resource Group → Standard Tier
3. Inside Namespace → Create Event Hub named `telcocalls`
4. Copy Connection String from Shared Access Policies

### Step 2 — Configure TelcoGenerator
1. Download TelcoGenerator.zip
2. Open `telcodatagen.exe.config`
3. Add your Event Hub Name and Connection String
4. Run: `.\telcodatagen.exe 1000 0.2 2`

### Step 3 — Azure Stream Analytics
1. Create Stream Analytics Job
2. Add Input → Event Hub (alias: `CallStream`)
3. Add Output → Power BI (alias: `MyPBIoutput`)
4. Paste fraud detection query
5. Start the job

### Step 4 — Power BI Dashboard
1. Go to app.powerbi.com
2. Find `ASAdataset` in My Workspace
3. Create Dashboard with:
   - Card tile → Total Fraudulent Calls
   - Line Chart tile → Fraud Over Time

---

## Results
- ✅ Detects fraudulent calls in real-time
- ✅ Live Power BI dashboard updates every second
- ✅ Identifies impossible simultaneous calls from different countries
- ✅ End-to-end automated pipeline with zero manual intervention

---

## Key Learnings
- Real-time stream processing using Azure Stream Analytics
- Temporal windowing (Tumbling Window)
- Self-join technique to detect anomalies in streaming data
- End-to-end data pipeline from ingestion to visualization

---

## Author
Built as part of Microsoft Azure Data Engineering learning path.
