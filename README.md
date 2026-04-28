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
| **Network Tools** | tcpdump, hping3, Wireshark |
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

### **Rule 1: SYN Rate Threshold**
```python
