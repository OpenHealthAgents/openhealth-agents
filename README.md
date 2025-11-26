# OpenHealth Agents 🏥

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![FHIR Ready](https://img.shields.io/badge/Standard-HL7_FHIR_R4-firebrick)](https://hl7.org/fhir/)
[![Status](https://img.shields.io/badge/Status-Alpha-orange)]()

> **The Operating System for Sovereign, Compliant, and Agentic Healthcare AI.**

---

## 📖 Overview

**OpenHealth Agents** is an open-source framework designed to build, deploy, and manage autonomous AI agents for healthcare. Unlike generic agent frameworks, OpenHealth Agents is built from the ground up with **HIPAA compliance**, **clinical safety**, and **data interoperability** (FHIR) as first-class citizens.

We solve the "Trust Gap" in medical AI by ensuring every agent action is:
1.  **Interoperable:** Speaks native HL7 FHIR.
2.  **Auditable:** Every thought process and API call is cryptographically logged.
3.  **Safe:** Guarded by a dedicated "Guardian Layer" that prevents PII leaks and hallucinatory actions.

---

## 🏗️ Architecture

The platform follows a **Layered Safety Architecture**:

```mermaid
graph TD
    User((User/Clinician)) <--> UI[Interface Layer<br/>(API / Dashboard)]
    
    subgraph "The Guardian Layer (Safety)"
        Guard[Input/Output Guardrails]
        PII[PII Redactor]
        Critic[Clinical Critic Agent]
    end
    
    subgraph "The Agentic Core (Brain)"
        Orch[Orchestrator<br/>(LangGraph)]
        Mem[Vector Memory<br/>(Patient Context)]
        Planner[Reasoning Engine]
    end
    
    subgraph "Interoperability Layer (Hands)"
        FHIR[FHIR Connector]
        EHR[EHR Adapters<br/>(Epic/Cerner)]
        Tools[Medical Calculators<br/>/Search]
    end

    UI --> Guard
    Guard --> Orch
    Orch --> Planner
    Planner --> Tools
    Tools --> FHIR
```

---

## ⚡ Key Features

### 1. The Guardian Layer 🛡️
Safety is not an afterthought. It wraps the entire agentic core.
* **PII/PHI Redaction:** Automatically detects and masks patient identifiers before sending data to LLMs.
* **Clinical Guardrails:** Cross-references agent outputs against uploaded Clinical Practice Guidelines (CPGs).
* **Hallucination Checks:** A secondary, smaller model acts as a "Critic" to validate the primary agent's proposed actions.

### 2. Native Interoperability 🔗
* **FHIR-First:** Agents "think" in FHIR Resources (`Patient`, `Observation`, `Encounter`).
* **EHR Integration:** Pre-built connectors for **SMART on FHIR** compliant systems.

### 3. Human-in-the-Loop (HITL) 👤
* **Approval Workflows:** High-stakes actions (e.g., `DraftPrescription`, `DenyClaim`) trigger a "Request for Approval" state, requiring a human signature to proceed.
* **Immutable Audit Logs:** Full traceability of the agent's "Chain of Thought" stored in a tamper-evident log.

---

## 🚀 Getting Started

### Prerequisites
* Python 3.11+
* Docker & Docker Compose
* Access to an LLM Endpoint (Azure OpenAI, vLLM, or Bedrock)

### Quick Start (Local Sandbox)

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/OpenHealthAgents/openhealth-agents.git
    cd openhealth-agents
    ```

2.  **Set up Environment**
    ```bash
    cp .env.example .env
    # Edit .env with your API keys and configuration
    ```

3.  **Launch the Stack (Agents + HAPI FHIR Server + Vector DB)**
    ```bash
    docker-compose up -d
    ```

4.  **Run the "Scribe" Agent Demo**
    ```bash
    python -m agents.scribe.demo --audio ./sample_consult.wav
    ```

---

## 🤝 Contributing

We welcome contributions! Please read `CONTRIBUTING.md` (Coming Soon) for details on our clinical review process.

## ⚖️ Disclaimer

**OpenHealth Agents is a development framework.** It is not a medical device. The software is provided "as is", without warranty of any kind. Implementers are responsible for ensuring compliance with local regulations (HIPAA, GDPR) and clinical validation before deployment.
