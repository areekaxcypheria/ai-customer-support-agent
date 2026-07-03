# ai-customer-support-agent
AI Customer Support Agent 🤖💬

An AI-powered customer support agent built with n8n that reads live data from Google Sheets to answer customer questions automatically — no hardcoded answers, no manual replies.
This is my first step into AI automation. The demo use case is a fruit & vegetable delivery business (FreshCart), but the workflow is generic and can be reused for any business by just swapping the Google Sheet and the system prompt.

**What it does**
When a customer sends a WhatsApp message, the agent:
1. Receives the message via a chat trigger
2. Passes it to an AI Agent node (LLM-powered, via Groq)
3. Uses memory to keep track of the ongoing conversation
4. Looks up relevant info (hours, delivery areas, payment methods, pricing, etc.) directly from a Google Sheet used as a live knowledge base
5. Responds naturally, in the voice of the business — without ever revealing it's an AI
6. 
In short: it's a lightweight **RAG (Retrieval-Augmented Generation) pattern** — the AI retrieves real answers from a spreadsheet instead of guessing or hallucinating.

**Why Google Sheets as the knowledge base?**
1. No database setup required
2. Non-technical staff can update FAQs/answers directly in the sheet
3. Changes reflect instantly — no redeploying the workflow

**Architecture**
Chat Trigger (When chat message received)
        ↓
    AI Agent
    ├── Chat Model  → Groq Chat Model (LLM)
    ├── Memory      → Simple Memory (per conversation/session)
    └── Tool        → Get row(s) in Google Sheets (live FAQ/knowledge lookup)

**Tech stack**
1. n8n — no-code/low-code workflow automation platform
2. Groq — fast LLM inference (Llama models)
3. Google Sheets — knowledge base / FAQ source

**Setup**
1. Import workflow.json into your n8n instance: Editor → ... menu (top right) → Import from File
2. Add credentials:
    Groq API key
    Google Sheets OAuth credentials
3. Create your own Google Sheet with two columns, e.g. Question / Answer, and connect it in the Google Sheets tool node
4. Edit the AI Agent's system prompt with your business name, tone, and rules
5. Activate the workflow and connect your WhatsApp trigger

**Example interaction**
Customer: What are your opening hours?
AI: (looks up the Google Sheet) We're open Monday–Saturday, 9 AM–8 PM!
in this repo
