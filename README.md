💸✨ Expense Tracker AI – n8n Workflow

Automatically extract, classify & store expenses from chat messages using AI + Google Sheets.

🚀 Overview

This n8n workflow turns your normal chat messages into structured expense entries and logs them in a Google Sheet.
It uses an OpenAI-powered extraction agent with conversation memory, ensuring accurate parsing and smooth interactions.

🧩 Workflow Components
🔔 1. Chat Trigger

Node: When Chat Message Received

Triggers workflow on every new chat input

Loads previous session using memory

🧠 2. Conversation Memory

Node: Memory Buffer Window

Stores past messages within the same session

Helps the AI maintain conversational context

🤖 3. Expense Extraction Agent

Node: LangChain Agent

Extracts:

📝 description

💰 cost

📅 date (auto-fills with today’s date if missing)

🧩 category (food, travel, grocery, shopping, other)

🔑 sessionid

🎯 action ("record" or "other")

💬 chatInput (original message)

If NOT an expense → returns:

{
  "action": "other",
  "chatInput": "..."
}


Follows strict rules to always output clean JSON.

🧹 4. JSON Output Parser

Ensures the agent output is valid structured JSON.
No explanations or extra text allowed.

🕵️ 5. Check if Expense Record

Node: IF Condition

If action == "record" → continue

Else → stop workflow

📄 6. Add to Google Sheet

Node: Google Sheets Append
Writes to columns:

Description

Cost

Date

Type

Sessionid

Action

Chatinput

Adds one clean row per message.

🔧 Requirements

n8n instance

OpenAI API key

Google Sheets OAuth Credentials

Google Sheet with matching headers

🧪 Example
Input:

“Bought groceries for 350 today”

Output saved:
{
  "description": "groceries",
  "cost": "350",
  "date": "2024-01-15",
  "type": "grocery",
  "sessionid": "",
  "action": "record",
  "chatInput": "Bought groceries for 350 today"
}

