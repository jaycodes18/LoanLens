# LoanLens 🔍
### See Through the Fine Print

LoanLens is a free, AI-powered loan scanner that decodes the fine print of any loan offer and explains it in plain English — instantly, with no account required.

---

## What It Does

Upload a photo of a loan document (or enter the terms manually), and LoanLens will:

- Extract every key financial term using Claude AI vision
- Calculate the **true APR** — not the advertised one
- Verdict the loan as **predatory**, **warning**, or **fair**
- Explain costs in plain English (e.g. "$6.43 per day")
- Show red flags and compare the APR against market rates
- Suggest better alternatives specific to your loan type and state
- Let you ask follow-up questions via an AI chatbot that knows your specific loan

---

## The APR Formula

The core calculation that drives every analysis:

```
APR = ((Total Payback + Fees - Principal) / Principal) × (365 / Term in days) × 100
```

Example — a typical payday loan:
- Borrow $300, repay $390 in 14 days
- APR = (90 / 300) × (365 / 14) × 100 = **391%**

---

## How to Run It

LoanLens is a single HTML file. You need:

1. An **Anthropic API key** (`ANTHROPIC_API_KEY`)
2. A simple backend proxy to forward requests to the Claude API (to keep the key server-side)

### Quick Start

```bash
# Set your API key
export ANTHROPIC_API_KEY=sk-ant-...

# Serve the file (any static server works)
npx serve .
```

Point your proxy at `https://api.anthropic.com/v1/messages` and make sure `/api/analyze` routes to it.

> The demo mode (payday, auto, rent-to-own scenarios) works fully without an API key.

---

## Project Structure

```
loanlens/
└── index.html        # The entire application — frontend + logic
```

That's it. No build step. No dependencies. No framework.

---

## Three Input Modes

| Mode | How it works |
|---|---|
| **Upload** | Drop a photo, screenshot, or scanned PDF — Claude reads it |
| **Manual** | Type in the loan numbers directly |
| **Demo** | Pre-loaded payday, auto, and rent-to-own scenarios |

---

## Privacy

- **No database.** Nothing is ever stored.
- **No account.** No signup, no login.
- **Stateless backend.** The proxy receives a request, calls Claude, and returns the result. Nothing is written to disk.
- Uploaded documents are sent to Claude AI for text extraction only. [Anthropic's privacy policy](https://www.anthropic.com/privacy) applies to that processing.

---

## Built With

- HTML, CSS, JavaScript (vanilla — no frameworks)
- [Claude API](https://www.anthropic.com/api) — vision extraction, analysis, and chat
- [Google Fonts](https://fonts.google.com) — Bebas Neue, DM Mono, DM Sans
- Canvas API — animated background
- FileReader API — client-side file handling

---

## Demo Scenarios

| Scenario | Details | APR |
|---|---|---|
| 🚨 Payday Loan | $300 → repay $390 in 14 days | ~391% |
| 🚗 Auto Loan | $12k, 84 months, hidden dealer markup | Warning |
| 📺 Rent-to-Own | $499 TV → $1,170 total over 18 months | Predatory |

---

## Disclaimer

LoanLens is for **educational purposes only** and does not constitute legal or financial advice.

If you've been targeted by predatory lending, contact the CFPB:
- 🌐 [consumerfinance.gov](https://www.consumerfinance.gov)
---

*Built at Hackonomics — financial literacy hackathon.*
