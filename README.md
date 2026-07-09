Markdown
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
Data Ingestion: Executes low-latency GET requests to financial market telemetry endpoints to fetch live stock data.

Conditional Routing: A stateless filtering layer evaluates the asset payload, halting execution if market volatility thresholds are not breached.

Contextual Analysis Engine: High-volatility payloads dynamically inject into a structured prompt framework leveraging gemini-3.1-flash-lite to generate institutional-grade briefings.

Structured Storage: Unstructured inference outputs are structured and logged to a persistent Google Sheets data warehouse alongside core telemetry data.

Notification Gateway: Dispatches instantaneous plain-text payloads to a dedicated Telegram client via automated bot hooks.

🛠️ Tech Stack & Integrations
Orchestration: Make.com iPaaS Engine

Inference Engine: Google Gemini AI API (gemini-3.1-flash-lite)

Data Sources: Alphavantage / Market Data API via HTTPS

Data Storage: Google Sheets API

Alerting Mechanism: Telegram Bot API

📂 Repository Structure
blueprint.json - The visual workflow configuration exported directly from the orchestration server. Import this file into a fresh environment to reproduce the full canvas layout.

README.md - Technical systems documentation and implementation details.

⚙️ Core Technical Challenges & Solutions
1. Eliminating Gateway Invalidation via Parse Mode Toggles
Challenge: Initial testing using MarkdownV2 constraints on the Telegram gateway caused systematic pipeline failures ([400] Bad Request: can't parse entities). The strict parsing engine threw exceptions on raw markdown formatting tokens (, -, .) generated dynamically by the LLM response payload.
Solution: Refactored the notification payload to enforce an explicit text-only schema by stripping strict markup dependencies and neutralizing the Parse Mode property. This ensured unbroken data transmission across asynchronous runtime cycles.

2. State-Less Telemetry Filtering
Challenge: Minimizing redundant computation and unnecessary credit overhead from flat/sideways market actions.
Solution: Configured upstream data-validation rules ensuring the downstream inference engine only wakes up when volatility criteria are actively met, maintaining clean operational efficiency.

🚀 Deployment Instructions
Prerequisites
A Make.com account

A Gemini API key configured via Google AI Studio

A custom Telegram Bot Token generated via @BotFather

Steps
Clone this repository to your local machine.

Create a new scenario in your Make canvas.

Click the menu options icon in the bottom toolbar, select Import Blueprint, and select the blueprint.json file.

Update your module authorization tokens (HTTP credentials, Google Sheets access tokens, Gemini API secrets, and your unique Telegram Chat ID).

Initialize the system state by executing a manual scenario runtime test.
