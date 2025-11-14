# 🧪 Splunk Basics – DNS Log Analysis Lab

This project demonstrates how to ingest and analyze DNS logs using Splunk.  
You will explore DNS query patterns, top talkers, and query types using SPL.

---

## 🎯 Objective

- Ingest Zeek DNS logs into Splunk  
- Perform DNS-based threat hunting  
- Identify top queried domains  
- Detect noisy DNS clients  
- Analyze DNS query types (A, AAAA, PTR, CNAME, etc.)  
- Build SOC-style investigation skills  

---

## 📂 Project Structure

splunk-dns-log-analysis/
│
├── README.md
│
├── screenshots/
│ ├── task1.png
│ ├── task2.png
│ ├── task3.png
│
└── dns-sample/
└── dns.log


---

## 🖥️ Lab Setup

### Requirements
- Splunk Enterprise / Free edition  
- Zeek DNS log file (`dns.log` in JSON format)  
- Internet browser to access Splunk Web  
- Custom Index: `dns_lab` (recommended)

---

## ⚙️ Uploading DNS Logs into Splunk

1. Open **Splunk Web**
2. Navigate to **Settings → Add Data**
3. Choose **Upload from file**
4. Select your `dns.log`
5. Set:
   - **Source Type:** `json`
   - **Index:** `dns_lab`
6. Click **Submit**
7. Validate ingestion:



---

# 🔍 DNS Analysis (SPL Queries)

Below are the three core DNS investigation queries required for this lab.

---

## ✅ Task 1 – Most Frequently Queried Domains

### SQL Query:
```sql
index=dns_lab sourcetype="json"
| stats count by query
| sort -count

## ✅ Task 2 – Most Frequently Queried Domains

###SQL Query:
```sql
index=dns_lab sourcetype="json"
| stats count by "id.orig_h"
| sort -count


