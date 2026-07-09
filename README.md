# Real-Time AI Stock Analyst Pipeline 📊🤖

An automated data pipeline that continuously monitors live market telemetry, evaluates asset volatility via programmatic filtering, synthesizes fundamental/macro market analysis using the Gemini LLM, and broadcasts interactive alerts to an enterprise monitoring gateway.

## 🏗️ Architecture Overview

The pipeline orchestrates data flow across multiple disparate APIs to handle ingestion, processing, storage, and notification:

```text
[HTTP API Ingestion] 
       │
       ▼
[Volatility Filter] ──(Drops non-moving assets)──► [Exit]
       │
       ▼
[Gemini LLM Inference Engine] 
       │
       ├──────────────────────────────┐
       ▼                              ▼
[Google Sheets Data Warehouse]   [Telegram Gateway Alert]
