# Ignyte × ElevenLabs AI Challenge: Track 2 — RERA & DLD Rights Verification Agent

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100.0+-green.svg)](https://fastapi.tiangolo.com/)
[![ElevenLabs](https://img.shields.io/badge/ElevenLabs-Conversational_AI-orange.svg)](https://elevenlabs.io/)

Official submission for **Track 2 (Government Services)** in the **Ignyte × ElevenLabs Voice Agent Challenge**. 

This repository implements **Amal**, an inbound multilingual AI voice agent for the **Dubai Land Department (DLD)** and **Rental Dispute Centre (RDC)**. It dynamically evaluates tenant and landlord rental inquiries against public RERA rules (Decree No. 43 of 2013) and Ejari contract records, providing authoritative factual clarity and automated pre-filing draft preparation.

---

## 🏛️ Architecture Overview[ Caller (WebRTC / Phone) ]
│
▼
[ ElevenLabs Voice Engine ]
├── Scribe v2 STT (Keyterm Biased for Dubai Real Estate)
├── Agent Workflow Engine (Multi-Node Sub-Agents)
└── Knowledge Base (RAG over Decree No. 43 / DLD Rules)
│
├── HTTPS Webhook Calls (REST API)
▼
[ FastAPI Webhook Middleware ]
├── Ejari Verification Engine (/api/v1/lookup-ejari)
├── RERA Index Decree 43 Calculator (/api/v1/check-rera-index)
├── RDC Draft Dispute Generator (/api/v1/create-draft-dispute)
└── Human Warm Handoff Queue (/api/v1/escalate-human)


### Component Breakdown
- **ElevenLabs Conversational AI:** Handles speech recognition (Scribe v2 with keyterm biasing), multi-dialect Gulf Arabic/English TTS (Eleven v3), and RAG knowledge retrieval over RERA legal decrees.
- **FastAPI Webhook Middleware:** Implements official Law No. 43 of 2013 calculation logic, validates Ejari contracts, creates draft tickets, and handles agent transfer payloads
- ## 🚀 Key Features & Stack Selection

- **Speech-to-Text:** Scribe v2 Realtime STT with custom keyterm biasing (`Ejari`, `RERA`, `DLD`, `Decree 43`, `Makani`).
- **Voice & Language:** Eleven v3 localized TTS with native Gulf Arabic and English switching.
- **Workflow & Scoping:** Multi-node branching with isolated tool execution and strict context boundaries.
- **Regulatory Precision:** Grounded in Decree No. 43 of 2013 rental index rules with zero ungrounded legal outputs.
- **Human-in-the-Loop:** Automated drafting of RDC dispute tickets; immediate warm transfers for legal advice or out-of-scope disputes.

---

## 🛠️ Quickstart Guide

### 1. Repository Setup & Installation
```bash
git clone [https://github.com/YOUR_USERNAME/ignyte-elevenlabs-rera-agent.git](https://github.com/YOUR_USERNAME/ignyte-elevenlabs-rera-agent.git)
cd ignyte-elevenlabs-rera-agent

# Set up virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
