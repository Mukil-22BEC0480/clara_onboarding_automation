# Clara Onboarding Automation

## Overview

This project implements an automation pipeline that converts sales/demo call transcripts into structured account configuration files.

The system processes two stages of customer interaction:

1. **Demo Call → v1 Account Memo**
2. **Onboarding Call → v2 Account Memo (updated configuration)**

The pipeline is implemented using **n8n workflows** and structured JSON schemas.

---

# Project Structure

```
clara_onboarding_automation
│
├── dataset
│   ├── demo_calls
│   │   └── demo_001.txt
│   │
│   └── onboarding_calls
│       └── onboarding_001.txt
│
├── outputs
│   └── accounts
│       └── ben_electrical_001
│           │
│           ├── v1
│           │   ├── account_memo.json
│           │   └── agent_spec.json
│           │
│           └── v2
│               ├── account_memo.json
│               └── agent_spec.json
│
├── changelog
│   └── changes.json
│
├── schemas
│   ├── account_memo_schema.json
│   └── retell_agent_spec_template.json
│
├── workflows
│   ├── clara_pipeline.json
│   └── clara_pipeline_diagram.jpeg
│
└── README.md
```

---

# Workflow Overview

The automation pipeline works as follows:

```
Demo Transcript
        ↓
Generate v1 Account Memo
        ↓
Onboarding Transcript
        ↓
Generate v2 Account Memo
```

Each step extracts relevant configuration details from call transcripts and produces structured account configuration data.

---

# Running the Workflow

### 1. Install n8n

```
npm install n8n -g
```

### 2. Start n8n

```
n8n
```

Open in browser:

```
http://localhost:5678
```

---

### 3. Import the Workflow

Import:

```
workflows/clara_onboarding_pipeline.json
```

---

### 4. Run the Pipeline

Execute the workflow using the **Manual Trigger** node.

The workflow processes the transcripts and generates the structured configuration output.

---

# Output Example

Example structured configuration:

```json
{
  "account_id": "ben_electrical_001",
  "company_name": "Ben Electrical Services",
  "pricing": {
    "service_call_fee": 150,
    "hourly_rate": 175,
    "billing_increment_minutes": 30
  },
  "call_handling": {
    "initial_setup": "Forward calls to Clara when Ben does not answer",
    "future_setup": "Clara answers first then transfers calls if needed"
  }
}
```

---

# Key Features

* Automated transcript processing
* Versioned account configuration (v1 → v2)
* Structured JSON schema validation
* n8n workflow automation
* Clear output structure for downstream systems

---

# Notes

This implementation demonstrates how conversational onboarding data can be converted into structured operational configuration for an AI answering system.

---
