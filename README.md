# MIClaim Compass 🧭  
_AI Insurance & Healthcare Navigator for Michigan (IBM watsonx Orchestrate)_

## Overview

MIClaim Compass is an AI-powered assistant designed to help Michigan residents and insurance members navigate:

- Auto & PIP claims (Michigan No-Fault)
- Health insurance claims
- Benefits & coverage questions
- In-network provider lookup
- Claim denials & appeals
- Notifications and reminders for key deadlines

The solution is built for the **IBM watsonx** ecosystem and demonstrates how a **master agent** can orchestrate several focused sub-agents and tools to deliver a unified user experience.

This project was created for an AI hackathon focused on **modernizing Michigan industries** using AI while keeping innovation and opportunities in-state.

---

## High-Level Features

- 💬 **Master conversational assistant** (“MIClaim Compass”) that routes requests to specialized agents
- 📂 **Domain-specific agents** for claims, benefits, providers, appeals, and notifications
- 🧱 **Mock datasets in YAML** (no live backend required) for:
  - Claims (auto, health, workers comp, FMLA)
  - Benefits (auto No-Fault/PIP & health plans)
  - Providers (Detroit, Dearborn, Flint)
  - Appeal guides (common denial reasons & steps)
  - Notifications (simulated reminders)
- 📘 **Health plan knowledge base**: summary of your plan benefits
- 🧠 Designed to work with **IBM watsonx Orchestrate / MCP tools** or as LLM prompts

---

## Architecture

### Agent Model

The system uses a **master + sub-agent** architecture:

- **MasterAgent (MIClaim Compass Orchestrator)**
  - Entry point for all user messages
  - Detects intent: FAQ, benefits, claim status, provider search, appeals, notifications
  - Routes to the correct sub-agent and aggregates responses

- **Sub-Agents**
  - `ClaimsAgent` – Claim status & key details  
  - `BenefitsAgent` – Plan coverage & benefits explanations  
  - `ProviderAgent` – In-network provider search (Michigan)  
  - `AppealsAgent` – Denial reasons & appeal steps  
  - `NotificationAgent` – Simulated reminders & alerts  
  - `FAQAgent` (optional) – General insurance & Michigan No-Fault FAQs

Each sub-agent works over **local YAML data** or a **document summary**, so the prototype can run without any external services.

---

## Repository Structure (Suggested)

```text
.
├─ README.md
├─ agents/
│  ├─ master-agent-prompt.md
│  ├─ claims-agent-prompt.md
│  ├─ benefits-agent-prompt.md
│  ├─ provider-agent-prompt.md
│  ├─ appeals-agent-prompt.md
│  ├─ notification-agent-prompt.md
│  └─ faq-agent-prompt.md
├─ data/
│  ├─ claims-data.yaml
│  ├─ benefits-data.yaml
│  ├─ providers-data.yaml
│  ├─ appeals-guides.yaml
│  └─ notifications-data.yaml
├─ knowledge/
│  └─ benefit-summary-hdhpq-oap-summary.md
├─ tools/
│  ├─ miclaim-tools-openapi.yaml      # Optional: OpenAPI spec for tools
│  └─ (any MCP / watsonx tool configs)
└─ slides/
   └─ pitch-deck/                    # Optional: hackathon presentation assets
