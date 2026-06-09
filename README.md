# SMS Fraud Shield

Built during a Google ADK live workshop.

SMS Fraud Shield is an AI agent that helps users — especially 
elderly and less digitally literate Indians — verify whether a 
received message is genuine or fraudulent.

Users can copy-paste suspicious text messages or attach screenshots 
to get an instant verdict.

---

## Problem Context

SMS fraud is a growing threat in India targeting people through 
fake bank alerts, KYC notices, lottery scams, and OTP phishing.
Most victims — particularly the elderly — lack tools to quickly 
verify suspicious messages before acting on them.

---

## How It Works

The agent classifies any SMS into one of three categories:

| Category   | Meaning |
|------------|---------|
| GENUINE    | Legitimate bank alert, UPI notification, or known service |
| SUSPICIOUS | Unclear intent — some unusual elements but no explicit fraud |
| FRAUD      | Malicious intent — KYC traps, phishing links, OTP harvesting |

**Inputs accepted:**
- Text — paste the suspicious message directly
- Screenshot — attach an image of the message

**Output (strict JSON):**
```json
{
  "category": "FRAUD",
  "icon": "🛑",
  "reason": "Message asks user to click a link to update KYC — 
             a known phishing pattern. Legitimate banks never 
             send KYC update links via SMS.",
  "actions": ["Do not click the link", "Report to your bank"],
  "youtube": "https://www.youtube.com/watch?v=VCU6hRjLxKM"
}
```

---

## Why Indian Banking Context Matters

The agent is trained on Indian-specific fraud patterns:
- Real banks use masked account numbers (XXXX1234) and 
  business sender IDs (AX-HDFCBK, VK-SBIINB)
- Real banks never send KYC update links or request OTPs via SMS
- Urgency language ("within 24hrs", "account will be blocked") 
  is a fraud signal, not a bank behaviour

This prevents false positives — legitimate debit/credit alerts 
are correctly identified as GENUINE, not flagged as fraud.

---

## Tech Stack

- Google Agent Development Kit (ADK)
- Gemini 2.5 Flash---

## Setup

```bash
git clone https://github.com/LakshmanSurampudi/sms-fraud-shield
cd sms-fraud-shield/smsfraudshield

# Add your Google API key
export GOOGLE_API_KEY=your_key_here

adk run smsfraudshield
```
- Python

---

## Project Structure
sms-fraud-shield/
└── smsfraudshield/
    ├── agent.py        # ADK agent with classification logic
    ├── init.py
    └── .adk/           # ADK configuration
