# 🛡️ Honeypot Deployment & Analysis

## 📋 Overview
As part of the KANO Cyber Institute curriculum, I developed and deployed a custom honeypot to monitor and analyze unauthorized access attempts over a five-day period.

## 🔧 Key Activities

### 🛠️ Custom Honeypot Development
- Developed a Python-based honeypot designed to simulate vulnerable services.
- Configured to listen on:
  - Port **5900** (VNC)
  - Port **25565** (Minecraft)
  - Port **8888** (Jupyter Notebook)
- Objective: Attract potential attackers by mimicking exposed systems.

### ☁️ Deployment Environment
- Deployed on a **Linux server** hosted on the **KANO Cloud** platform.
- The honeypot ran **continuously for five days** to ensure uninterrupted data collection.

### 📊 Data Collection & Analysis
- Captured network traffic and logged all connection attempts.
- Ingested logs into **Splunk** for advanced analysis.
- Built a custom **Splunk dashboard** to visualize trends and identify anomalies.

## 📈 Findings
- **Days 1–4:** Low-level probing and minimal activity observed.
- **Day 5:** 
  - Sharp spike in traffic: ~82,000 connection attempts in 24 hours.
  - Majority of traffic originated from **DigitalOcean IP ranges**.
  - Insight into **automated scanning behaviors** and **common attacker tactics**.

---

> 🧠 This project demonstrates practical skills in honeypot engineering, log analysis, and security monitoring—highlighting a real-world example of proactive cyber threat intelligence collection.

