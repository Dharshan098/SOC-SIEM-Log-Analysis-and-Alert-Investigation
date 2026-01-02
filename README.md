# Linux Authentication Monitoring using Elastic SIEM

## 📌 Project Overview

This project demonstrates the implementation of a **Security Information and Event Management (SIEM)** solution using **Elastic Security** to monitor, detect, and investigate Linux authentication events. The goal is to simulate real **SOC (Security Operations Center)** workflows such as log ingestion, detection rule creation, alert investigation, and alert closure.

This project is designed as a **SOC Analyst (Tier 1) portfolio project** and uses **real Ubuntu logs**, not sample data.

---

## 🛠️ Tools & Technologies

* **Elastic Security (SIEM)**
* **Kibana**
* **Elastic Agent**
* **Ubuntu Linux**
* **System Integration (auth.log & syslog)**

---

## 🎯 Project Objectives

* Collect Linux authentication logs in real time
* Detect failed authentication attempts
* Generate and investigate security alerts
* Understand the SOC alert lifecycle
* Document findings for SOC workflows

---

## 🧱 Architecture

```
Ubuntu Linux Host
     ↓
Elastic Agent
     ↓
Elastic Cloud (Elasticsearch)
     ↓
Kibana (Elastic Security)
```

---

## 🔹 Step 1: Environment Setup

* Deployed **Ubuntu Linux** as the monitored endpoint
* Created an **Elastic Cloud deployment**
* Accessed **Elastic Security** via Kibana

---

## 🔹 Step 2: Elastic Agent Installation

* Installed Elastic Agent on Ubuntu
* Enrolled the agent into Fleet
* Verified agent status as **Healthy**

---

## 🔹 Step 3: Log Ingestion Configuration

* Added **System integration** to the agent policy
* Enabled:

  * `/var/log/auth.log`
  * `/var/log/syslog`
* Confirmed logs ingestion using **Discover → logs-***

---

## 🔹 Step 4: Log Validation

* Generated real authentication events:

  * Successful sudo access
  * Failed authentication (wrong password)
* Verified events using KQL queries:

```
event.dataset:system.auth
```

```
event.category:authentication AND event.outcome:failure
```

---

## 🔹 Step 5: Detection Rule Creation

Created a custom SIEM detection rule:

* **Rule Name:** Linux Authentication Failure
* **Rule Type:** Custom Query
* **Query:**

```
event.category:authentication AND event.outcome:failure
```

* **Severity:** Medium
* **Risk Score:** 47
* **Schedule:** Every 5 minutes

---

## 🔹 Step 6: Alert Generation & Investigation

* Triggered alert by entering incorrect password
* Investigated alert details:

  * Host name
  * User
  * Timestamp
  * Authentication failure message
* Viewed related events in **Discover**

---

## 🔹 Step 7: Alert Closure (SOC Workflow)

* Classified alert as **False Positive** (user testing)
* Closed alert via **Elastic Security Alerts interface**
* Understood limitations of comments/cases in lab setup

---

## 🧠 SOC Analyst Skills Demonstrated

* SIEM deployment and configuration
* Linux log analysis
* Authentication threat detection
* Alert triage and investigation
* SOC alert lifecycle management
  
Author: Dharshan
Role Target: SOC Analyst / Cybersecurity Analyst
