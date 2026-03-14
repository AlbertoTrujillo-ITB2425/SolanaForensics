# SolanaForensics 🔍

<div align="center">

**Enterprise-Grade Security, Monitoring, and Social Payment Platform for the Solana Ecosystem.**

[![License: MIT](https://img.shields.io/badge/License-MIT-9945FF.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Solana](https://img.shields.io/badge/Solana-Mainnet-14F195.svg?style=flat-square&logo=solana)](https://solana.com)
[![Node.js](https://img.shields.io/badge/Node.js-Backend-339933.svg?style=flat-square&logo=node.js)](https://nodejs.org)
[![RPC](https://img.shields.io/badge/RPC-Helius-FF6B35.svg?style=flat-square)](https://helius.dev)
[![Status](https://img.shields.io/badge/Status-Active%20Development-brightgreen.svg?style=flat-square)]()
[![Academic](https://img.shields.io/badge/Academic-ASIXc2%20·%202025--2026-blue.svg?style=flat-square)]()

<br/>

```
███████╗ ██████╗ ██╗      █████╗ ███╗   ██╗ █████╗
██╔════╝██╔═══██╗██║     ██╔══██╗████╗  ██║██╔══██╗
███████╗██║   ██║██║     ███████║██╔██╗ ██║███████║
╚════██║██║   ██║██║     ██╔══██║██║╚██╗██║██╔══██║
███████║╚██████╔╝███████╗██║  ██║██║ ╚████║██║  ██║
╚══════╝ ╚═════╝ ╚══════╝╚═╝  ╚═╝╚═╝  ╚═══╝╚═╝  ╚═╝
███████╗ ██████╗ ██████╗ ███████╗███╗   ██╗███████╗██╗ ██████╗███████╗
██╔════╝██╔═══██╗██╔══██╗██╔════╝████╗  ██║██╔════╝██║██╔════╝██╔════╝
█████╗  ██║   ██║██████╔╝█████╗  ██╔██╗ ██║███████╗██║██║     ███████╗
██╔══╝  ██║   ██║██╔══██╗██╔══╝  ██║╚██╗██║╚════██║██║██║     ╚════██║
██║     ╚██████╔╝██║  ██║███████╗██║ ╚████║███████║██║╚██████╗███████║
╚═╝      ╚═════╝ ╚═╝  ╚═╝╚══════╝╚═╝  ╚═══╝╚══════╝╚═╝ ╚═════╝╚══════╝
```

*Blockchain transparency. Security by design. Payments made human.*

[🔍 Live Demo](https://solanaguard.app) · [📖 Docs](#-documentation) · [🐛 Issues](https://github.com/AlbertoTrujillo/solana-forensics/issues) · [📬 Contact](#-author)

</div>

---

## 📋 Table of Contents

- [Overview](#-project-overview)
- [System Architecture](#️-system-architecture)
- [Frontend — SolanaGuard UI](#-frontend--solanaguard-ui)
- [Key Features](#️-key-features)
- [Database Design](#-database-design-m0372)
- [Security Infrastructure](#-security-infrastructure)
- [API & RPC Integration](#-api--rpc-integration)
- [Tool Inventory](#-tool-inventory)
- [Installation](#-installation--setup)
- [Project Structure](#-project-structure)
- [Roadmap](#️-roadmap)
- [Academic Context](#-academic-context)
- [License](#-license)
- [Author](#-author)

---

## 📝 Project Overview

**SolanaForensics** is a comprehensive forensic intelligence and payment platform built on top of the Solana blockchain. It bridges the gap between raw on-chain data and actionable security intelligence — making blockchain auditing accessible to investigators, developers, and everyday users alike.

The project is structured around **two primary pillars**:

### 🛡️ Pillar 1 — Forensic Security & Monitoring Engine

A real-time blockchain intelligence backend providing:

- Automated anomaly detection on wallet behavior (transaction error rates, age vs. activity ratios, token accumulation patterns)
- Smart contract interaction fingerprinting (Jupiter, Raydium, Pump.fun, and unknown program identification)
- Proactive wallet tracking with live polling via Helius RPC subscription model
- NFT portfolio analysis using the Helius DAS (Digital Asset Standard) API
- Stake account mapping and validator relationship tracking
- Risk scoring engine (0–100 heuristic model with multi-factor signal weighting)
- Bulk wallet analysis (up to 20 simultaneous addresses with error-rate profiling)
- CSV export of transaction histories for forensic and fiscal use

### 💸 Pillar 2 — Social Pay System

A decentralized payment architecture that humanizes Solana transactions:

- Human-readable alias system replacing 44-character Base58 addresses
- SNS (Solana Name Service) `.sol` domain resolution with a 3-layer cascade fallback: **Bonfida API → NameRecord PDA → Helius RPC**
- Pre-transfer reputation validation against known threat databases
- Wallet comparison engine for side-by-side balance and behavior analysis

---

## 🏗️ System Architecture

The system follows a high-performance client-server architecture designed for low latency and high availability at scale.

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                            │
│   index.html (Buscador/Home)   ·   tools.html (9 Herramientas) │
│   Dark/Light Theme · i18n (10 idiomas) · Google Translate       │
└──────────────────────────┬──────────────────────────────────────┘
                           │ HTTPS / JSON-RPC 2.0
┌──────────────────────────▼──────────────────────────────────────┐
│                       API GATEWAY LAYER                         │
│              Helius RPC (mainnet.helius-rpc.com)                │
│         CoinGecko REST API · Bonfida SNS Proxy API              │
└──────────┬──────────────────────────────────────┬───────────────┘
           │                                       │
┌──────────▼──────────┐               ┌────────────▼──────────────┐
│   SOLANA MAINNET    │               │      BACKEND SERVER        │
│                     │               │   Node.js + @solana/web3   │
│  • RPC Nodes        │               │   Express REST API         │
│  • Stake Program    │               │   Authentication layer     │
│  • Token Program    │               │   Rate limiting            │
│  • SNS Program      │               │   Proxy (API key shield)   │
│  • DAS API          │               └────────────┬──────────────┘
└─────────────────────┘                            │
                                       ┌────────────▼──────────────┐
                                       │      DATABASE LAYER        │
                                       │   SQL — Normalized Schema  │
                                       │   Wallets · Contacts       │
                                       │   Transactions · Logs      │
                                       └───────────────────────────┘
```

### Core Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Frontend** | HTML5 · CSS3 · Vanilla JS | SPA-style UI, no framework dependency |
| **Blockchain Client** | `@solana/web3.js` v1.95.3 | RPC calls, PDA derivation, SNS resolution |
| **RPC Provider** | Helius (mainnet) | High-throughput, DAS-enabled, low-latency |
| **Price Feed** | CoinGecko REST v3 | Real-time SOL/USD market data |
| **SNS Resolution** | Bonfida SNS Proxy | `.sol` domain → wallet address |
| **Backend** | Node.js | API proxy, DB bridge, business logic |
| **Database** | SQL (relational) | Normalized schema for audit logs and user data |
| **Infrastructure** | Linux (Ubuntu) | Hardened server with `fail2ban`, `ufw`, privilege separation |
| **Styling** | Tailwind CSS (CDN) · CSS custom properties | Responsive layout with dark/light theme system |

---

## 🖥 Frontend — SolanaGuard UI

The frontend is a two-page application with a shared design system:

### `index.html` — Buscador (Home)

The primary audit interface. Features:

- **Universal wallet search** — accepts both Base58 addresses and `.sol` SNS domains
- **3-layer SNS resolution cascade** for maximum compatibility:
  1. Bonfida public API proxy
  2. On-chain NameRecord PDA derivation via SHA-256 hashing
  3. Helius `getAccountInfo` fallback
- **Live balance display** with SOL → USD conversion
- **SPL token table** sorted by balance descending
- **Transaction history** with DEX identification (Jupiter, Raydium, Pump.fun)
- **Recent search history** persisted in `localStorage`
- **URL parameter support** (`?wallet=ADDRESS`) for cross-page deep-linking from `tools.html`
- **Quick-load wallets** (Solana Foundation, Binance Hot Wallet, toly.sol)

### `tools.html` — Centro de Herramientas (9 tools)

| # | Tool | Backend Method | Description |
|---|---|---|---|
| 1 | 🖼️ **NFT Scanner** | Helius DAS `getAssetsByOwner` | Full NFT portfolio with real images, collection grouping, and Solscan links |
| 2 | 📡 **Live Monitor** | `getSignaturesForAddress` polling (5s) | Real-time transaction feed with DEX tagging and error highlighting |
| 3 | ⚖️ **Wallet Comparator** | Parallel `Promise.all` fetches | Side-by-side comparison of balance, activity, SPL tokens, error rate, and success rate — **supports mixed `.sol` + Base58** |
| 4 | 🚨 **Rug Detector** | Multi-signal heuristic engine | Risk score 0–100 with 8 detection signals: error rate, age/activity ratio, token accumulation, bot patterns |
| 5 | 🥩 **Staking Tracker** | `getParsedProgramAccounts` with `memcmp` filter | Full stake account mapping: validator, delegation status, lamport breakdown |
| 6 | 📤 **CSV Exporter** | `getSignaturesForAddress` (50–500 txs) | Download transaction history as CSV compatible with Excel, Google Sheets, and tax tools |
| 7 | 🔢 **Bulk Check** | `Promise.allSettled` × 20 | Parallel multi-wallet analysis with balance, transaction count, and error rate table |
| 8 | 📈 **SOL Price** | CoinGecko `/coins/solana` | Live price, 24h/7d/30d % changes, market cap, volume, ATH, and SOL→USD inline converter |
| 9 | ⭐ **Top Wallets** | Curated dataset | 18 reference wallets (protocols, DeFi, exchanges, whales, founders) with category filters and search |

### Shared UI System

- **Dark / Light theme toggle** — zero-flash implementation using `data-theme` attribute applied before first paint via inline script; state synced between pages via `localStorage` (`sgTheme`)
- **Multilingual support** — 10 languages (ES, EN, PT, FR, DE, IT, RU, AR, JA, ZH) powered by Google Translate with a custom premium selector UI; preference stored in `localStorage` (`sgLang`)
- **API key obfuscation** — key split into Base64-encoded fragments, assembled at runtime; designed to be replaced by a backend proxy endpoint in production

---

## 🛠️ Key Features

### 🔴 Real-Time Blockchain Auditing
Continuous monitoring of network transactions using Helius RPC with 5-second polling intervals. The live feed classifies each transaction by program interaction (DEX swaps, transfers, contract calls) and highlights failures in real time.

### 🟢 Alias-Based Directory (Social Pay)
The SNS resolution engine converts human-readable `.sol` domain names to wallet addresses using a three-layer fallback system, making the payment UX accessible to non-technical users while maintaining on-chain verifiability.

### 🟡 Pre-Transaction Risk Validation
Before displaying or routing a payment to any address, the Rug Detector scores the wallet against 8 heuristic signals derived entirely from on-chain data. No external threat databases required — all signals are derived from publicly available chain state.

### 🔵 Forensic Export & Audit Trail
Transaction history can be exported to CSV (up to 500 entries) with UTC timestamps, slot numbers, and status flags. This supports compliance with fiscal reporting requirements and forensic investigation workflows.

### 🟣 Staking Intelligence
The staking tracker queries the Stake program directly using `getParsedProgramAccounts` with a `memcmp` filter on the authorized withdrawer field — producing a complete map of delegation positions, validator relationships, and total staked SOL.

---

## 📊 Database Design (M0372)

The logical data model is normalized to 3NF to ensure data integrity, eliminate redundancy, and support efficient forensic queries at scale.

```sql
-- Core entity schema (simplified)

CREATE TABLE Wallets (
    wallet_id       UUID PRIMARY KEY,
    address         VARCHAR(44)  UNIQUE NOT NULL,   -- Solana Base58 public key
    alias           VARCHAR(64),                     -- SNS domain if resolved
    risk_score      SMALLINT     DEFAULT 0,          -- 0-100 heuristic score
    is_flagged      BOOLEAN      DEFAULT FALSE,
    first_seen_at   TIMESTAMP,
    last_activity   TIMESTAMP,
    created_at      TIMESTAMP    DEFAULT NOW()
);

CREATE TABLE Contacts (
    contact_id      UUID PRIMARY KEY,
    user_id         UUID         NOT NULL REFERENCES Users(user_id),
    alias           VARCHAR(64)  NOT NULL,           -- Human-readable name
    wallet_address  VARCHAR(44)  NOT NULL REFERENCES Wallets(address),
    verified        BOOLEAN      DEFAULT FALSE,
    created_at      TIMESTAMP    DEFAULT NOW(),
    UNIQUE (user_id, alias)
);

CREATE TABLE Transactions (
    tx_id           UUID PRIMARY KEY,
    signature       VARCHAR(88)  UNIQUE NOT NULL,    -- Solana tx signature
    from_wallet     VARCHAR(44)  REFERENCES Wallets(address),
    to_wallet       VARCHAR(44)  REFERENCES Wallets(address),
    amount_lamports BIGINT,
    slot            BIGINT,
    block_time      TIMESTAMP,
    program_tag     VARCHAR(32),                     -- Jupiter, Raydium, etc.
    status          VARCHAR(8)   DEFAULT 'SUCCESS',  -- SUCCESS | FAIL
    risk_flag       BOOLEAN      DEFAULT FALSE,
    raw_data        JSONB
);

CREATE TABLE SystemLogs (
    log_id          UUID PRIMARY KEY,
    event_type      VARCHAR(32)  NOT NULL,           -- AUDIT | ALERT | INFO | ERROR
    source          VARCHAR(64),                     -- Component that generated the log
    wallet_ref      VARCHAR(44),                     -- Optional wallet reference
    message         TEXT         NOT NULL,
    severity        SMALLINT     DEFAULT 1,          -- 1=INFO 2=WARN 3=ERROR 4=CRITICAL
    created_at      TIMESTAMP    DEFAULT NOW()
);
```

### Entity Relationship Summary

| Entity | Key Relations | Purpose |
|---|---|---|
| `Users` | 1:N → `Contacts` | Platform user accounts with authentication |
| `Wallets` | N:M via `Contacts` · 1:N → `Transactions` | Indexed address registry with risk metadata |
| `Contacts` | Belongs to `User`, references `Wallet` | Alias directory for Social Pay |
| `Transactions` | References two `Wallets` (from/to) | Immutable audit log of blockchain events |
| `SystemLogs` | Standalone audit trail | Infrastructure events for M0369 compliance |

---

## 🔐 Security Infrastructure

The server environment follows a defense-in-depth model with hardened Linux configurations:

```
┌─────────────────────────────────────────────┐
│           NETWORK PERIMETER                  │
│  UFW Firewall — allow 22/tcp, 80/tcp, 443   │
│  Fail2Ban — SSH brute force protection       │
│  Rate limiting on all API endpoints          │
└────────────────────┬────────────────────────┘
                     │
┌────────────────────▼────────────────────────┐
│           APPLICATION LAYER                  │
│  Node.js backend as non-root user           │
│  Environment variables for secrets          │
│  API key proxy — never exposed to client    │
│  CORS policy — origin whitelist             │
│  Input sanitization (Base58 regex filter)   │
└────────────────────┬────────────────────────┘
                     │
┌────────────────────▼────────────────────────┐
│              DATA LAYER                      │
│  Parameterized SQL queries (no raw concat)  │
│  Principle of least privilege on DB users   │
│  Encrypted connections (SSL/TLS)            │
│  Automated backup rotation                  │
└─────────────────────────────────────────────┘
```

### API Key Security Model

The Helius RPC API key is protected through layered obfuscation and server-side proxying:

1. **Frontend (current):** Key is Base64-fragmented and assembled at runtime — mitigates automated scraping and public repo leaks
2. **Production target:** All RPC calls are routed through a backend proxy endpoint (`/api/rpc`), keeping the key entirely server-side
3. **Helius dashboard:** Domain allowlist configured to restrict key usage to `solanaguard.app` only

---

## 🔌 API & RPC Integration

### Helius RPC (Primary)

| Method | Used By | Purpose |
|---|---|---|
| `getBalance` | Audit, Compare, Bulk | SOL balance in lamports |
| `getSignaturesForAddress` | Audit, Monitor, Export | Transaction history + status |
| `getParsedTransactions` | Audit, Rug Detector | Full transaction decode with log messages |
| `getParsedTokenAccountsByOwner` | Audit, Rug, Compare | SPL token holdings |
| `getParsedProgramAccounts` | Staking Tracker | Stake delegation accounts |
| `getAccountInfo` | SNS Resolution | NameRecord PDA data |
| `getAssetsByOwner` (DAS) | NFT Scanner | Full NFT portfolio with metadata |

### External APIs

| API | Endpoint | Used By |
|---|---|---|
| CoinGecko v3 | `/coins/solana?market_data=true` | Price panel (live price, market cap, ATH) |
| Bonfida SNS Proxy | `/resolve/{name}` | SNS Layer 1 resolution |
| CoinGecko Simple | `/simple/price?ids=solana` | Balance panel USD conversion |

### SNS Resolution — 3-Layer Cascade

```
Input: "toly.sol"
       │
       ▼
Layer 1: GET https://sns-sdk-proxy.bonfida.workers.dev/resolve/toly
         → returns { result: "PublicKey..." }  ✓ → resolved
         → network error / not found            ↓
Layer 2: Derive NameRecord PDA on-chain
         SHA-256( \x00 + "toly" ) → seeds → findProgramAddress
         Read data[32:64] → owner PublicKey     ✓ → resolved
         → empty / zero pubkey                  ↓
Layer 3: Helius getAccountInfo("toly.sol")
         → value.owner !== SystemProgram        ✓ → resolved
         → all layers failed                    ✗ → Error thrown
```

---

## 🧰 Tool Inventory

### Frontend Files

```
solanaguard/
├── index.html          # Home — Wallet buscador & auditor
├── tools.html          # Centro de herramientas (9 tools)
└── assets/
    └── logo_solana.png # Brand logo
```

### Features Matrix

| Feature | index.html | tools.html |
|---|:---:|:---:|
| Wallet Search (Base58) | ✅ | ✅ (all tools) |
| SNS `.sol` Resolution | ✅ | ✅ (all tools) |
| SOL Balance | ✅ | ✅ |
| SPL Token List | ✅ | — |
| Transaction History | ✅ | ✅ (Export CSV) |
| DEX Identification | ✅ | ✅ (Monitor) |
| NFT Scanner | — | ✅ |
| Live Transaction Monitor | — | ✅ |
| Wallet Comparator | — | ✅ |
| Rug/Risk Detector | — | ✅ |
| Staking Tracker | — | ✅ |
| CSV Export | — | ✅ |
| Bulk Wallet Check | — | ✅ |
| SOL Price + Converter | — | ✅ |
| Curated Wallet Directory | — | ✅ (18 wallets) |
| Dark / Light Theme | ✅ | ✅ |
| 10-Language i18n | ✅ | ✅ |
| URL Deep-link (`?wallet=`) | ✅ | — |
| Recent Search History | ✅ | — |

---

## 🚀 Installation & Setup

### Prerequisites

```bash
node >= 18.0.0
npm  >= 9.0.0
```

### 1. Clone the repository

```bash
git clone https://github.com/AlbertoTrujillo/solana-forensics.git
cd solana-forensics
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

```bash
cp .env.example .env
```

Edit `.env`:

```env
# Helius RPC API Key — get yours at https://helius.dev
HELIUS_API_KEY=your_api_key_here

# Server
PORT=3000
NODE_ENV=production

# Database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=solana_forensics
DB_USER=sfuser
DB_PASS=your_secure_password

# Security
ALLOWED_ORIGINS=https://solanaguard.app,http://localhost:3000
RATE_LIMIT_WINDOW_MS=60000
RATE_LIMIT_MAX=100
```

### 4. Initialize the database

```bash
npm run db:migrate
npm run db:seed    # Optional: populate reference wallet data
```

### 5. Start the server

```bash
# Development (with hot reload)
npm run dev

# Production
npm start
```

### 6. Open the frontend

Navigate to `http://localhost:3000` or open `index.html` directly in any modern browser. No build step required for the frontend.

---

### Linux Server Hardening (Production)

```bash
# UFW Firewall
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable

# Fail2Ban — protect SSH
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban

# Run Node.js as non-root
sudo useradd -r -s /bin/false sfnode
sudo chown -R sfnode:sfnode /opt/solana-forensics

# Process manager
npm install -g pm2
pm2 start npm --name "solana-forensics" -- start
pm2 save
pm2 startup
```

---

## 📁 Project Structure

```
solana-forensics/
│
├── 📄 index.html                 # Home — wallet buscador
├── 📄 tools.html                 # Herramientas avanzadas
│
├── assets/
│   └── logo_solana.png
│
├── backend/
│   ├── server.js                 # Express entry point
│   ├── routes/
│   │   ├── rpc.js                # Helius proxy routes
│   │   ├── wallets.js            # Wallet CRUD endpoints
│   │   ├── contacts.js           # Alias directory API
│   │   └── transactions.js       # Tx log endpoints
│   ├── middleware/
│   │   ├── auth.js               # JWT authentication
│   │   ├── rateLimiter.js        # Express rate limiting
│   │   └── sanitize.js           # Input validation
│   └── services/
│       ├── riskEngine.js         # Heuristic scoring logic
│       ├── snsResolver.js        # SNS cascade resolver
│       └── exportService.js      # CSV generation
│
├── database/
│   ├── migrations/               # Schema versioned migrations
│   ├── seeds/                    # Reference data (wallets, protocols)
│   └── schema.sql                # Full DDL
│
├── docs/
│   ├── API.md                    # REST API reference
│   ├── ARCHITECTURE.md           # Detailed system diagrams
│   └── SECURITY.md               # Security model documentation
│
├── .env.example
├── .gitignore
├── package.json
└── README.md
```

---

## 🗺️ Roadmap

### ✅ Phase 1 — Frontend MVP (Completed)
- [x] Wallet auditor with SNS resolution (3-layer cascade)
- [x] SPL token and transaction history display
- [x] DEX transaction tagging (Jupiter, Raydium, Pump.fun)
- [x] Dark / Light theme system with zero-flash implementation
- [x] 10-language internationalization
- [x] NFT Scanner (Helius DAS API)
- [x] Live transaction monitor (5s polling)
- [x] Wallet comparator supporting mixed `.sol` + Base58
- [x] Rug/Risk detector (8-signal heuristic, 0–100 score)
- [x] Staking tracker (`getParsedProgramAccounts`)
- [x] CSV export (up to 500 transactions)
- [x] Bulk wallet analysis (up to 20 wallets)
- [x] SOL price panel with inline converter
- [x] API key obfuscation (Base64 fragment assembly)

### 🔄 Phase 2 — Backend & Database (In Progress)
- [ ] Node.js REST API with Helius proxy endpoint
- [ ] PostgreSQL schema deployment and migrations
- [ ] JWT-based user authentication
- [ ] Alias-to-wallet mapping (Social Pay directory)
- [ ] Persistent watchlist with webhook notifications
- [ ] Centralized log collection (`SystemLogs` table)

### 🔮 Phase 3 — Advanced Features (Planned)
- [ ] WebSocket-based live monitor (replace polling)
- [ ] Cross-wallet fund flow graph visualization (D3.js)
- [ ] Smart contract interaction scoring (ABI fingerprinting)
- [ ] Email/Telegram alert system for flagged wallets
- [ ] Mobile-responsive PWA packaging
- [ ] Pre-transfer risk validation gate for Social Pay
- [ ] Historical risk score timeline per wallet
- [ ] Multi-signature wallet support

---

## 🎓 Academic Context

This project was developed as part of the **ASIXc2 (Administració de Sistemes Informàtics en Xarxa)** curriculum at the **Institut de Formació Professional**, addressing the following competency modules:

| Module | Topic | How it's addressed |
|---|---|---|
| **M0369** | Implantació de sistemes operatius | Linux hardened server, `fail2ban`, `ufw`, user privilege separation, PM2 process management |
| **M0370** | Fonaments de maquinari | Server architecture decisions, hardware resource planning for RPC load |
| **M0371** | Implantació de sistemes operatius en xarxa | Network topology, firewall configuration, DNS, SSL/TLS deployment |
| **M0372** | Gestió de bases de dades | Normalized SQL schema (3NF), ER model, migration strategy, query optimization |
| **M0373** | Llenguatges de marques | Semantic HTML5, structured CSS with custom properties, JSON-RPC communication |
| **M0374** | Administració de sistemes gestors de BBDD | PostgreSQL administration, user roles, backup policy, performance tuning |

The project demonstrates end-to-end systems thinking: from infrastructure hardening and database design to client-side security and blockchain protocol interaction.

---

## 📜 License

```
MIT License

Copyright (c) 2026 Alberto Trujillo

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

This project is open-source under the MIT License, reflecting the transparency and collaborative spirit of the open-source blockchain community. Academic use, professional contribution, and derivative works are all explicitly encouraged.

---

## 👨‍💻 Author

<div align="center">

**Alberto Trujillo**

*Systems Administration Student · Blockchain Developer · OSINT Researcher*

Student of **Administració de Sistemes Informàtics en Xarxa (ASIXc2)**
Academic Year **2025–2026**

---

*"Blockchain data is public. SolanaForensics makes it legible."*

</div>

---

<div align="center">

**⭐ If this project helped you, consider leaving a star on GitHub.**

Built with 💜 on Solana · Powered by Helius · Secured by design

</div>
