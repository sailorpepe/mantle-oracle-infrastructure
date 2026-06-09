<p align="center">
  <img src="assets/banner.png" alt="Mantle Sovereign Oracle" width="100%">
</p>

<h1 align="center">The Undesirables: Sovereign A2A Oracle Infrastructure</h1>

<h3 align="center">Bridging Real-World Assets & Parametric Data to Mantle Network for Agentic Execution.</h3>

<p align="center">
  <img src="https://img.shields.io/badge/Network-Mantle%20Testnet-000000?logo=mantle&logoColor=white" alt="Mantle">
  <img src="https://img.shields.io/badge/Oracle-Zero%20Trust-success" alt="Oracle">
  <img src="https://img.shields.io/badge/AI-Qwen%20Vision-blue" alt="AI">
  <img src="https://img.shields.io/badge/Agent-MCP%20Ready-orange" alt="MCP">
  <img src="https://img.shields.io/badge/License-BUSL--1.1-blue.svg" alt="License">
</p>

<p align="center">
  <a href="https://the-undesirables.com"><strong>Live Dashboard</strong></a> ·
  <a href="#on-chain-contracts"><strong>Mantle Contracts</strong></a> ·
  <a href="https://youtube.com"><strong>Demo Video</strong></a>
</p>

---

## 📑 Table of Contents
- [The Problem](#the-problem)
- [The Solution](#the-solution)
- [Ecosystem Architecture](#ecosystem-architecture)
  - [1. The Oracle Node (Vision AI)](#1-the-oracle-node-vision-ai)
  - [2. The Verification Layer (Mantle Network)](#2-the-verification-layer-mantle-network)
  - [3. The Agent Integration (MCP Server)](#3-the-agent-integration-mcp-server)
- [On-Chain Contracts](#on-chain-contracts)
- [Quick Start for Agents](#quick-start-for-agents)
- [License](#license)

---

## The Problem
Current blockchain oracles are built for *humans* to read crypto prices. They are opaque, heavily centralized, and rely on multi-sig committees to push data on-chain. 

If we want to build a true **Agentic Economy** where autonomous AI agents execute financial strategies, assess collateral, and manage portfolios, those agents cannot rely on blind trust. They need an **Agent-to-Agent (A2A) Oracle** that allows them to independently verify the data they are consuming.

## The Solution
We built the first Sovereign A2A Oracle Infrastructure specifically designed for the **Mantle Network**.

By combining local Vision AI models, the Model Context Protocol (MCP), and cryptographic Merkle Roots, we allow autonomous agents to trustlessly verify and trade against **Real-World Assets (physical trading cards)** and **Parametric Data (Weather)**.

---

## Ecosystem Architecture

This submission is an integrated suite of infrastructure. Below are the core components:

```mermaid
graph TD
    A[Physical Asset] -->|Scanned by| B(Rust Desktop App)
    B -->|Local Qwen Vision AI| C{Appraisal & Market Depth}
    C -->|Hashes data| D[Merkle Root]
    D -->|Pushes to| E[(Mantle Network)]
    F[Autonomous AI Agent] -->|Queries| G(MCP Server)
    G -->|Requests Proof| E
    E -->|Returns Verified Price| F
```

### 1. The Oracle Node (Vision AI)
A natively compiled Tauri/Rust desktop application. It uses local Vision AI to scan physical trading cards, grade their condition, query live market depths, and prepare the data for on-chain submission.
*   **Repository:** [tcg-oracle-app](https://github.com/sailorpepe/tcg-oracle-app) (Rust / React codebase)

### 2. The Verification Layer (Mantle Network)
Our smart contracts deployed on the **Mantle Testnet** act as the ultimate source of truth. We publish daily Merkle roots containing 276,000+ RWA prices and hourly TWAP feeds.
*   **Source Code:** [Mantle Smart Contracts Repository](./contracts)

### 3. The Agent Integration (MCP Server)
An open-source Python MCP server that allows any AI agent (Claude, ElizaOS) to query our market memory and instantly request a Merkle proof to verify the price against the Mantle blockchain.
*   **Source Code:** [Mantle MCP Agent Server](https://github.com/sailorpepe/litvm-tcg-oracle-mcp)
*   **Install:** `pip install litvm-tcg-oracle`

### 4. The Weather Engine (Parametric Data)
A secondary oracle engine that pulls 1-minute ASOS sensor data from the National Weather Service and cross-references it against Kalshi prediction markets to execute automated parametric DeFi payouts.
*   **Source Code:** [Mantle Weather Engine Repository](https://github.com/sailorpepe/litvm-weather-oracle)

---

## On-Chain Contracts

We have successfully deployed our infrastructure to the **Mantle Testnet** (Chain ID: `5003`).

| Contract Name | Address | Purpose |
|--------------|---------|---------|
| **TCGPriceOracleV2** | [`0xA6796...B344cD`](https://explorer.sepolia.mantle.xyz/address/0xA6796c86E9f9019B6ff2a5044be8D0211aB344cD) | Hourly TWAP for top 50 blue-chip RWA cards |
| **MerklePriceOracle** | [`0x6B31b...D8072c`](https://explorer.sepolia.mantle.xyz/address/0x6B31b3735D88b148d47255EdAa4DD74A65D8072c) | Daily Merkle root for 276,000+ products |
| **WeatherEdgeOracle** | [`0xe0dCD...53451`](https://explorer.sepolia.mantle.xyz/address/0xe0dCD77D245480CEB830EA66B74849101F853451) | Hourly NWS Parametric data verification |

*(Contract addresses will be updated upon final execution of the deploy scripts).*

---

## Quick Start for Agents

If you are evaluating this project and want to test the Agentic Integration, add the following to your `claude_desktop_config.json` or Cursor MCP settings:

```json
{
  "mcpServers": {
    "litvm-tcg-oracle": {
      "command": "litvm-tcg-oracle"
    }
  }
}
```

Then simply ask your AI: *"What is the verified price of a Charizard Base Set on the Mantle Network?"* The agent will automatically query the MCP server, retrieve the Merkle proof, and verify the price against the Mantle Testnet contract.

---

## License & Commercial Use

This project is licensed under the **[Business Source License 1.1 (BUSL-1.1)](LICENSE.md)**.
Built by The Undesirables LLC. We build in public and support the developer ecosystem, but we also protect our infrastructure. This code automatically converts to the fully open-source **MIT License** on June 1, 2030.
