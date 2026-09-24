# TaskFlow — AI Customer Support Agent

An AI customer support agent that answers product questions instantly using a real knowledge base, and honestly escalates to a human whenever it shouldn't be the one answering — no invented policies, no guessed troubleshooting steps.

> Built as a portfolio project for an AI automation agency. Demonstrates a full RAG (Retrieval-Augmented Generation) pipeline: knowledge base → grounded AI answers → honest escalation → logged handoff.

## Demo

[Watch the demo video](https://youtu.be/Y9EK6LU_fBg) — a real conversation, from an accurate documented answer through to an escalated billing question landing in Airtable, recorded live.

**Live chat:** [Talk to the TaskFlow Support Agent](https://udify.app/chat/VcvllA163Y0Ktuln)

## The Problem

Most AI support chatbots do one of two things badly: they refuse to answer anything beyond the most basic FAQ, or — worse — they confidently invent an answer when they don't actually know one. Both erode customer trust. This system is built to do neither: it answers accurately when the knowledge base actually covers the question, and it says so honestly — with a clear next step — when it doesn't.

TaskFlow is a fictional project-management SaaS product, used here as a realistic demo business with genuine product documentation: account setup, team permissions, task management, integrations, billing, and troubleshooting.

## What It Does

- Answers customer questions using only TaskFlow's real documentation — never outside knowledge or invented policy
- Retrieves the most relevant documentation using hybrid semantic + keyword search, reranked for accuracy
- Recognizes when a question needs a human — billing disputes, refunds, account security, unconfirmed bugs, or anything the knowledge base doesn't clearly cover
- Walks customers through documented troubleshooting steps before escalating, rather than escalating and troubleshooting at the same time
- Hands off escalations through a simple form that logs directly into Airtable for a support team to follow up
- Declines off-topic questions and stays honest about what it doesn't know, rather than guessing

## Architecture

```
Customer question
        ↓
Dify (Chatbot app)
        ↓
Knowledge Base retrieval (Hybrid Search: vector + keyword, reranked)
        ↓
   ┌────┴────┐
   ↓         ↓
Answered   Escalated
from docs  (billing / security / bug / uncertain)
              ↓
     Airtable handoff form (customer-facing)
              ↓
     Airtable Escalations table (support team's queue)
```

The knowledge base itself is built as a Dify pipeline: uploaded documents → text extraction → chunking → indexed knowledge base (OpenAI `text-embedding-3-small`, Hybrid Search retrieval with reranking).

## Tech Stack

| Layer | Tool | Purpose |
|---|---|---|
| AI / RAG | [Dify](https://dify.ai) | Knowledge base, retrieval pipeline, and the conversational chatbot |
| Embeddings | OpenAI `text-embedding-3-small` | Powers semantic search over the knowledge base |
| Escalation log | [Airtable](https://airtable.com) | System of record for questions the AI hands off to a human |
| Handoff | Airtable Form | Customer-facing form that captures escalation details |

## Key Design Decisions

- **SaaS over e-commerce or generic FAQ demo:** A project-management SaaS product was chosen deliberately over a more common e-commerce support demo. Answering "how do I use this feature" questions requires more retrieval precision than shipping/returns FAQs, and it's a more realistic vertical for an AI automation agency's actual client base.
- **Escalation is a form, not an automated write:** Rather than building automation (e.g. n8n) to silently log every escalated conversation, escalation routes through a simple Airtable form the customer fills in. This is simpler, has fewer points of failure, and mirrors how real small-business support handoffs often work — the AI's job is to recognize when to step back, not to own the entire pipeline end-to-end.
- **Hybrid Search over pure keyword search:** Initial testing with Dify's Economical (keyword-only) indexing produced weak retrieval — a question like "how do I invite a team member" matched loosely-related chunks about permissions and comments instead of the actual invite instructions. Switching to High Quality embeddings with Hybrid Search (semantic + keyword, reranked) fixed this immediately and was worth the small added cost for the accuracy gain.
- **Troubleshoot-then-escalate, not both at once:** Early testing revealed the AI would say "I'm connecting you with a human" and then continue troubleshooting in the same message — confusing and contradictory. The system prompt was revised to enforce one clear behavior: walk through documented troubleshooting first, and only claim escalation once it's actually happening.

## Known Limitations

This is a portfolio-ready demo, not a production deployment. Specifically:

- Knowledge base covers a realistic but limited set of documentation (6 documents) — a production system would need broader, continuously updated content.
- Escalation is a manual customer-submitted form, not a live human handoff or ticketing system integration (e.g. Zendesk, Intercom).
- No authentication or account-specific context — the AI cannot look up a real customer's account, billing history, or data; it answers only from general documentation.
- Response time is roughly 7-8 seconds per message, typical for a RAG pipeline (retrieval + reranking + generation), but slower than a simple non-grounded chatbot.

## Repository Contents

- `/Screenshots/` — screenshots of the working system across the full pipeline: knowledge base setup, retrieval testing, chatbot configuration, and end-to-end tests
- `/system-prompt/` — the full Dify system prompt (instructions) used by the chatbot
- `/Knowledge-base/` — the 6 source documents that make up TaskFlow's knowledge base

## Testing Performed

- Accurate, documented how-to questions — answered correctly from source content
- Billing/refund requests — correctly escalated, never resolved by the AI itself
- Questions with no documented answer — AI admits it doesn't know rather than inventing a plausible-sounding answer
- Off-topic questions — declined and redirected, not answered
- Frustrated customer tone — AI stays calm, troubleshoots using documented steps, escalates cleanly without contradicting itself
- Vague reports ("it's not working") — AI asks a clarifying question instead of guessing what's wrong
- Full end-to-end escalation flow — confirmed a real submission through the Airtable form correctly lands in the Escalations table
