# Email Automation Workflow (n8n)

An AI-powered email triage and response system built with n8n, Google Gemini, and WhatsApp notifications. The workflow automatically classifies incoming Gmail messages, labels them, drafts contextual responses, and alerts you in real time.

## Overview

Manually sorting through emails, deciding priority, and drafting replies is time-consuming. This workflow automates that process end-to-end: every new email is read, classified by an AI model, routed to a category-specific handler, and acted upon — with a WhatsApp notification so you never miss something important.

## Features

- **Automatic email classification** into five categories: High Priority, Finance/Billing, Customer Support, Promotion, and General
- **Gmail auto-labeling** based on classification, keeping your inbox organized without manual sorting
- **AI-generated drafts and summaries** tailored to each category using Google Gemini
- **Structured output parsing** to ensure consistent, reliable data flows between nodes
- **Real-time WhatsApp notifications** so you can act on important emails immediately
- **Modular branch design**, allowing each category's logic and prompts to be tuned independently

## How It Works

1. **Trigger**: A Gmail Trigger node watches the inbox for new incoming emails.
2. **Classification**: A Text Classifier node analyzes the email content and routes it into one of five categories.
3. **Labeling**: Each category applies a corresponding Gmail label (e.g., High Priority, Finance/Billing, Customer Support, Promotion) for easy filtering and searchability.
4. **AI Processing**: Each branch passes the email to a dedicated AI agent (Google Gemini Chat Model + Structured Output Parser) that either:
   - Drafts a suggested reply, or
   - Generates a concise summary of the email's content and intent
5. **Action & Notification**:
   - Drafts are saved directly to Gmail for review before sending
   - A WhatsApp message is sent to notify you of the new email and its classification, so you can respond quickly from anywhere

## Categories & Routing

| Category | Label Applied | AI Action | Notification |
|---|---|---|---|
| High Priority | High Priority | Draft creation | WhatsApp alert |
| Finance/Billing | Finance/Billing | Summarization | WhatsApp alert |
| Customer Support | Customer Support | Summarization | WhatsApp alert |
| Promotion | Promotion | Summarization | WhatsApp alert |
| General | — | — | WhatsApp alert |

## Tech Stack

- **[n8n](https://n8n.io/)** — Workflow automation and orchestration
- **Gmail API** — Email trigger, labeling, and draft creation
- **Google Gemini** — LLM-based classification, summarization, and drafting
- **WhatsApp Business API** — Real-time notifications
- **Structured Output Parsers** — Enforce consistent JSON output from AI nodes for reliable downstream processing

## Setup

### Prerequisites
- An active [n8n](https://n8n.io/) instance (self-hosted or cloud)
- A Google Cloud project with Gmail API access and OAuth2 credentials configured in n8n
- A Google Gemini API key
- A WhatsApp Business API integration configured in n8n (e.g., via Meta's Cloud API or a supported connector)

### Installation
1. Import the workflow JSON into your n8n instance.
2. Configure credentials for:
   - Gmail (OAuth2)
   - Google Gemini (API key)
   - WhatsApp (API credentials)
3. Update the Gmail labels referenced in each branch to match labels that exist (or will be created) in your Gmail account.
4. Adjust the classification prompt in the Text Classifier node if you want to add, remove, or redefine categories.
5. Test each branch individually with sample emails before activating the workflow.
6. Activate the workflow so it runs automatically on new incoming emails.

## Usage

Once activated, the workflow runs automatically in the background. Every new email that arrives in the connected Gmail inbox will be:
1. Classified
2. Labeled
3. Processed by the relevant AI agent
4. Summarized or drafted as appropriate
5. Flagged to you via WhatsApp

No manual intervention is required unless you want to review or edit an AI-generated draft before sending.

## Future Improvements

- Add auto-send capability for low-risk, high-confidence categories (e.g., promotions)
- Consolidate the AI agents into a single model with dynamic prompting per category to reduce node overhead
- Add a feedback loop to fine-tune classification accuracy over time
- Extend notifications to additional channels (Slack, Telegram, email digest)
- Add error handling and retry logic for API rate limits or failures

## Notes

This is an early-stage personal automation project built to explore AI-driven email management using n8n. Contributions, suggestions, and improvements are welcome.
