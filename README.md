# SolanaForensics 🔍

**Enterprise-Grade Security, Monitoring, and Social Payment Platform for the Solana Ecosystem.**

## 📝 Project Overview

**SolanaForensics** is a comprehensive solution designed to bridge the gap between complex blockchain data and user-friendly security management. The project is divided into two primary pillars:

1. **Forense Security & Monitoring:** A robust backend engine that provides real-time visibility into Solana blockchain activity. It features automated anomaly detection, smart contract vulnerability analysis, and proactive wallet tracking to identify threats like phishing or malicious contract interactions.
2. **Social Pay System:** A decentralized payment architecture that simplifies Solana transactions. It replaces cryptic 44-character wallet addresses with human-readable aliases, protected by a security layer that validates the destination's reputation before executing any transfer.

This project is developed as part of the **ASIXc2 (Systems Administration)** curriculum, emphasizing system scalability, secure database architecture, and innovative entrepreneurial deployment.

---

## 🏗 System Architecture

The system follows a high-performance client-server architecture designed to ensure low latency and high availability.

### Core Stack

* **Frontend:** Semantic HTML5, CSS3 (Responsive Grid/Flexbox), and JavaScript.
* **Backend:** Node.js, utilizing `@solana/web3.js` for seamless interaction with the Solana RPC nodes.
* **Database:** Relational database design (SQL-compliant) for efficient management of user profiles, alias-to-wallet mapping, and historical audit logs.
* **Infrastructure:** Linux-based server environment with hardened security configurations, including `fail2ban` for intrusion prevention, `ufw` for firewall management, and strict user privilege control.

---

## 🛠 Key Features

* **Real-Time Blockchain Auditing:** Continuous monitoring of network transactions to flag suspicious patterns.
* **Alias-Based Directory:** A secure mapping service linking human-readable names to blockchain addresses.
* **Pre-Transaction Risk Validation:** An automated safety filter that evaluates the target wallet's history against known threat databases before finalizing payments.
* **Centralized Log Management:** Automated collection and indexing of system logs and blockchain events for forensic auditing.

---

## 📊 Database Design (M0372 Competency)

The logical model is normalized to ensure data integrity and query performance:

| Entity | Description |
| --- | --- |
| `Wallets` | Stores public addresses and associated security risk metadata. |
| `Contacts` | Mapping table connecting User IDs, Aliases, and Solana Addresses. |
| `Transactions` | Detailed historical log containing hash, timestamps, and risk status. |
| `SystemLogs` | Audit trails of system events, essential for M0369 compliance. |

---

## 📑 License

This project is licensed under the **MIT License**. We believe in the transparency and collaborative spirit of the open-source blockchain community, encouraging both academic use and professional contribution.

---

## 👨‍💻 Author

* **Alberto Trujillo**
* Student of Systems Administration (ASIXc2)
* Academic Year: 2026

