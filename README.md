# AI Customer Support Agent

An intelligent, multi-tool AI agent built with n8n and Google Gemini 
that handles customer support conversations on Telegram — answering 
product questions, checking order status, resolving FAQs, and 
escalating complex issues to human agents automatically.

##  Architecture
Telegram Message → AI Agent (Gemini 1.5 Flash)
├── Memory (conversation context)
├── Tool: Search Products (Google Sheets)
├── Tool: Search FAQs (Google Sheets)
├── Tool: Check Order Status (Google Sheets)
└── Tool: Escalate to Human Admin (Telegram)
↓
Response → Customer (Telegram)
↓
Logged → Conversations Sheet

## Tech Stack

- **n8n** — AI Agent orchestration and workflow automation
- **Google Gemini 1.5 Flash** — LLM reasoning engine
- **Telegram Bot API** — customer-facing chat interface
- **Google Sheets** — knowledge base (Products, FAQs, Orders) & 
  conversation logging

##  Features

### Multi-Tool Reasoning
The agent dynamically decides which tool to call based on the 
customer's intent — no hardcoded if/else logic.

### Conversation Memory
Maintains context across messages using a windowed memory buffer, 
enabling natural multi-turn conversations.

### Knowledge-Grounded Responses
All product, pricing, and policy answers are pulled live from a 
structured knowledge base — preventing hallucinated information.

### Human-in-the-Loop Escalation
When the agent can't resolve a request (e.g. order modifications, 
complaints), it automatically notifies a human admin via Telegram 
with full context — and informs the customer transparently.

### Full Conversation Logging
Every interaction (timestamp, user, question, answer) is logged 
to Google Sheets for analytics and quality review.

## Knowledge Base Structure

**Products Sheet**
| product_id | name | price | stock | description |

**FAQs Sheet**
| question | answer |

**Orders Sheet**
| order_id | customer_name | product | status | date |

**Conversations Sheet** (auto-logged)
| timestamp | chat_id | username | question | answer |

##  Setup

1. Import `workflow.json` into your n8n instance
2. Connect credentials:
   - Telegram Bot (via BotFather)
   - Google Gemini API (Google AI Studio)
   - Google Sheets OAuth2
3. Create a Google Sheet with the 4 tabs above
4. Update the System Message with your business context
5. Activate the workflow

## Example Conversation

User: What's the price of the Smart Watch Pro?
Agent: The Smart Watch Pro is priced at $60. It is currently
in stock with 30 units available.
User: Check order ORD1005
Agent: Order ORD1005 for a USB-C Hub 7-in-1 was cancelled on
June 11, 2026. Please let me know if you have any
other questions.
User: Make it delivered
Agent: I apologize, but I don't have the ability to change
order statuses. I will escalate your request to a
human agent.
User: Yes
Agent: I have escalated your request to a human agent. They
will review your order status and get back to you
shortly!

##  Author

**Ahmed Wael Anwar** — AI Automation Engineer  
[LinkedIn](https://www.linkedin.com/in/ahmed-wael-b209111b2) | 
[GitHub](https://github.com/ahmedwael2)
