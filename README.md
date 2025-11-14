# 🧪 Splunk Basics – DNS Log Analysis Lab

This project walks through ingesting and analyzing DNS logs in Splunk using Zeek JSON logs.  
It includes all three core investigation tasks:  
✔️ Task 1 – Top Queried Domains  
✔️ Task 2 – Top Source Hosts  
✔️ Task 3 – DNS Query Type Breakdown  

---

## 🎯 Objective

- Ingest DNS logs into Splunk  
- Identify suspicious DNS activity  
- Perform top domain analysis  
- Detect noisy internal hosts  
- Analyze DNS query types (A, AAAA, PTR, TXT…)  
- Build SOC investigation skills  

---

## 📁 Project Structure

splunk-dns-log-analysis/
│
├── README.md
│
├── screenshots/
│ ├── task1.png → Top Domains
│ ├── task2.png → Top Source Hosts
│ ├── task3.png → DNS Query Types
│ ├── combined.png (optional)
│
└── dns-sample/
└── dns.log


---

## 🖥️ Splunk Setup

### Requirements
- Splunk Enterprise / Free  
- Zeek DNS logs (JSON format)  
- Index: `dns_lab`

---

## ⚙️ Uploading DNS Logs to Splunk

1. Open **Splunk Web**
2. Go to **Settings → Add Data**
3. Choose **Upload**
4. Select `dns.log`
5. Configure:
   - Source type: `json`
   - Index: `dns_lab`
6. Click **Submit**
7. Verify:


---

# 🔍 **TASK 1 – Most Frequently Queried Domains**

### ✔️ SPL Query
```spl
index=dns_lab sourcetype="json"
| stats count by query
| sort -count

index=dns_lab sourcetype="json"
| stats count by "id.orig_h"
| sort -count

✔️ Purpose

Shows which internal IPs generate the most DNS traffic

Noisy hosts may indicate:

Malware beaconing

DNS tunneling

Misconfiguration


index=dns_lab sourcetype="json"
| stats count by qtype
| sort -count


✔️ Purpose

Shows DNS record distribution

Normal: A, AAAA, PTR

Suspicious: TXT, NULL (often used in exfiltration/tunneling)

