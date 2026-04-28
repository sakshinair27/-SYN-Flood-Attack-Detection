# 🛡️ SYN Flood Attack Detection System

> A lightweight, host-based intrusion detection system that identifies SYN flood attacks in real-time using rule-based TCP handshake analysis.

---

## 🎯 Project Overview

SYN flood attacks remain one of the most persistent **Denial-of-Service (DoS)** techniques used to overwhelm systems by exploiting the TCP three-way handshake. Attackers flood victims with SYN packets without completing connections, causing the connection table to fill and crash the system.

This project develops a **lightweight, rule-based detection mechanism** that runs directly on the victim machine. By analyzing packet rates, SYN/SYN-ACK ratios, and connection patterns, it detects both **single-source and distributed SYN flood attacks** in real-time — without requiring complex machine learning or expensive enterprise IDS systems.

---

## 📊 Key Results

- ✅ **Detection time:** Alerts triggered within **1–3 seconds** of attack onset
- ✅ **CPU efficiency:** Maintained **<10% CPU usage** on victim machine
- ✅ **Attack detection range:** Successfully handled SYN rates up to **3,000 SYN/sec**
- ✅ **Coverage:** Detected both **single-source** and **distributed** SYN flood attacks
- ✅ **Zero false positives** under normal traffic conditions

---

## 🛠️ Tech Stack

| Category | Tools |
|---|---|
| **Languages** | Python, Bash |
| **Network Tools** | tcpdump, hping3, Wireshark, Scapy |
| **Environment** | Ubuntu 20.04 (SEED Labs VM) |
| **Concepts** | TCP/IP, Network Security, Intrusion Detection, Packet Analysis |

---

## 🏗️ Experimental Environment

A three-machine setup using the official **SEED Labs** environment:

| Machine | Role |
|---|---|
| **Attacker** | Generates SYN flood traffic using `hping3` |
| **Victim** | Runs detection script and observes TCP queue impact |
| **Monitor/Server** | Captures packets using `tcpdump` for analysis |

---

## 🔍 Detection Logic

The system implements **4 lightweight rules** to identify SYN flood patterns:

**Rule 1: SYN Rate Threshold** — Flags traffic when SYN rate exceeds 200 per second.

`if syn_rate > 200 per second: flag = "Possible SYN Flood"`

**Rule 2: SYN vs SYN-ACK Imbalance** — Detects when SYN packets vastly outnumber completed handshakes.

`if syn_rate > 5 * synack_rate: flag = "SYN Flood Likely"`

**Rule 3: Half-Open Connection Count** — Confirms attack when too many incomplete handshakes accumulate.

`if incomplete_connections > 100: flag = "Attack Confirmed"`

**Rule 4: Multi-Source SYN Indicators** — Identifies distributed attacks from many source IPs.

`if unique_source_ips > 50 and syn_rate is abnormal: flag = "Distributed SYN Flood"`

---

## 📦 Features Extracted from Packet Captures

1. **SYN rate per second** — Detects abnormal arrival spikes
2. **SYN-ACK rate per second** — Measures handshake completion attempts
3. **SYN to SYN-ACK ratio** — Identifies handshake imbalance
4. **Incomplete TCP handshakes** — Indicates half-open connection abuse
5. **Unique source IP count** — Distinguishes spoofing-based floods
6. **Backlog queue usage** — Tracks connection table exhaustion

---

## 🧪 Attack Simulation

Attacks were simulated using `hping3`:

`sudo hping3 -S -p 80 --flood <victim-ip>`

Packet capture during attacks was performed using:

`sudo tcpdump -nn -i eth0 'tcp[tcpflags] & tcp-syn != 0'`

⚠️ **Note:** Run only in controlled lab environments. Do not deploy on networks you don't own.

---

## 🚀 How to Run

Clone and run the project with these commands:

`git clone https://github.com/sakshinair27/SYN-Flood-Attack-Detection.git`

`cd SYN-Flood-Attack-Detection`

`pip install -r requirements.txt`

`sudo python3 syn_detector.py`

---

## 📁 Project Structure

```
SYN-Flood-Attack-Detection/
├── syn_detector.py                   # Main real-time detection script (Scapy-based)
├── offline_syn_analyzer.py           # Offline analysis of captured traffic
├── capture_syn.sh                    # Bash script for tcpdump packet capture
├── requirements.txt                  # Python dependencies
├── saknair_Final Project Report.pdf  # Detailed methodology + findings
└── README.md
```

---

## 📈 Comparison: Normal vs. Attack Traffic

| Metric | Normal Traffic | SYN Flood Attack |
|---|---|---|
| **SYN Rate** | < 20 SYN/sec | 500–5,000 SYN/sec |
| **SYN ↔ SYN-ACK Ratio** | Balanced | Highly imbalanced |
| **Handshake Completion** | High | Near-zero |
| **Backlog Queue** | Stable | Quickly fills |

---

## ⚠️ Limitations

- **Manual threshold tuning** — Detection rules require calibration per system
- **Slow-rate attacks** — Low-and-slow SYN floods may evade immediate detection
- **Reactive design** — Detects attacks but does not prevent them
- **Not a full IDS replacement** — Designed as a lightweight host-level supplement

---

## 🚀 Future Improvements

- 🤖 Integrate **machine learning** for adaptive threshold tuning
- 🛡️ Add **automatic mitigation** via `iptables` blocking
- 📊 Build a **real-time monitoring dashboard**
- 📡 Centralized logging server for distributed deployments
- 🌐 Extend support for **IPv6** and multi-interface systems

---

## 🌟 What I Learned

- Deep understanding of TCP/IP handshake vulnerabilities and exploitation
- Building lightweight detection systems with minimal performance overhead
- Industry-standard packet analysis using `tcpdump`, `Scapy`, and Wireshark
- The value of rule-based detection for fast, interpretable security tools
- Trade-offs between detection speed, accuracy, and resource consumption

---

## 📫 Connect With Me

**Sakshi Nair** — MS Data Science @ Indiana University

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/sakshinair27)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:sakshinair086@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=flat&logo=github&logoColor=white)](https://github.com/sakshinair27)

