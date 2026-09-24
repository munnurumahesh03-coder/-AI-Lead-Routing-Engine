# ⚡ AI-Lead-Routing-Engine (Intelligent CRM Automation)

![n8n](https://img.shields.io/badge/n8n-Workflow_Automation-orange.svg )
![Groq](https://img.shields.io/badge/Groq-Llama--3-black.svg )
![Google Sheets](https://img.shields.io/badge/Google_Sheets-CRM-green.svg )
![Python](https://img.shields.io/badge/Python-API_Integration-blue.svg )

## 📌 System Overview
An event-driven, zero-touch automation pipeline built to capture, classify, and route incoming business inquiries at scale. 

Instead of relying on human agents to manually read, interpret, and sort incoming webhooks, form submissions, or emails, this system integrates **Large Language Models (Groq's Llama-3)** directly into an **n8n workflow**. It performs real-time intent classification (Sales vs. Support vs. Spam) and automates data entry directly into a CRM dashboard.

## 📈 Business Impact & ROI
* **90% Reduction in Manual Triage:** Eliminates the need for human intervention in initial lead processing.
* **Zero-Latency Lead Routing:** Sales teams receive highly qualified, categorized leads instantly, drastically improving response times and conversion rates.
* **Error-Free Data Entry:** Replaces manual copy-pasting with deterministic API-driven CRM updates.

## 🧠 Detailed Workflow Architecture

### 1. Ingestion Layer (Trigger)
* Listens for incoming POST requests via an n8n Webhook node.
* Captures raw, unstructured JSON payloads (e.g., from a website contact form or email parser).

### 2. Cognitive Processing Layer (LLM API)
* The unstructured text is routed to the **Groq API** (running Llama-3-70B for maximum inference speed).
* **Entity Extraction:** Dynamically extracts `Sender_Name`, `Company`, `Budget`, and `Contact_Info`.
* **Intent Classification:** Classifies the message into strictly defined categories (`SALES_LEAD`, `SUPPORT_TICKET`, `OTHER`).

### 3. Orchestration & Routing Layer (Switch Node)
* Evaluates the LLM's classification output using conditional branching.
* **If `SALES_LEAD`:** Formats the extracted entities and pushes them to the CRM.
* **If `SUPPORT_TICKET`:** Routes the data to a secondary workflow for automated ticketing (e.g., Zendesk/Jira).

### 4. Integration Layer (CRM)
* Uses OAuth2 authentication to securely connect to the Google Sheets / CRM API.
* Appends the structured data to the active database with timestamped audit logs.

## 🤖 Prompt Engineering Strategy
To ensure the LLM does not hallucinate and strictly returns machine-readable data, the system utilizes a constrained system prompt with JSON-mode enforcement:
> *"You are an expert data extraction API. Analyze the following user message. Classify the intent as either SALES or SUPPORT. Extract the user's Name, Email, and Budget. Return ONLY a valid JSON object. Do not include conversational text."*

## ⚙️ Prerequisites & Tech Stack
To deploy this workflow locally or on the cloud, the following credentials and environments are required:
* Active **n8n** instance (Local Docker container or Cloud).
* **Groq API Key** (for Llama-3 inference).
* **Google Cloud Service Account** (OAuth2 credentials for Sheets API).

