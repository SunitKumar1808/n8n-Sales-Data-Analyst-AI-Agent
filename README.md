# n8n-Sales-Data-Analyst-AI-Agent
🤖 n8n Sales Data Analyst AI Agent

An autonomous AI agent built with n8n that reads live sales data from Google Sheets, analyzes it on request, and emails professionally formatted HTML reports via Gmail — all through natural language chat.

Ask it things like "Email me total sales by customer state" or "Which products generated the most revenue?" and it retrieves the data, analyzes it, and sends a clean report straight to your inbox — no dashboards, no manual queries.

✨ Features
📊 Live data retrieval — pulls the latest rows from a Google Sheet before every analysis, so answers are never stale
🧠 Natural language analysis — ask about revenue, top products, tax breakdowns, order status, regional performance, and more
✉️ Automated email reports — generates clean, structured HTML reports and sends them via Gmail automatically
🔒 Safe by design — recipient, subject, and Gmail account are pre-configured; the agent never needs (or asks for) email addresses
🗣️ Conversational interface — works through an n8n Chat Trigger, so no separate frontend is required
🧱 Tech Stack
Component	Tool
Workflow engine	n8n
AI Agent	LangChain Agent node (Claude / OpenAI compatible)
Data source	Google Sheets
Email delivery	Gmail (via n8n Gmail node)
Trigger	n8n Chat Trigger / Webhook
📋 Requirements

Before setting this up, you'll need:

n8n instance (self-hosted or n8n Cloud) — v1.0+ recommended for full AI Agent node support
An LLM API key/credential — e.g. Anthropic (Claude) or OpenAI, connected as a credential in n8n
Google account with:
A Google Sheet containing your sales data (see schema below)
Google Sheets OAuth2 credentials configured in n8n
Gmail account with OAuth2 credentials configured in n8n (for sending reports)
Basic familiarity with the n8n editor (nodes, credentials, tool-connections)
📊 Expected Data Schema

The agent is tuned for sales order data with the following columns (rename/adjust the prompt if your schema differs):

Order Id, Order Date, Item Id, Product Name, Brand Name, UPC,
Variant Description, Mapping on consumer app (L0, L1, L2), Business Category,
Supply City, Supply State, Supply State GST, Customer City, Customer State,
Order Status, HSN Code, IGST(%), CGST(%), SGST(%), CESS(%), Quantity,
MRP (Rs), Selling Price (Rs), IGST Value, CGST Value, SGST Value,
CESS Value, Total Tax, Total Gross Bill Amount

⚙️ Setup
Import the workflow
Import workflow.json into your n8n instance (Workflows → Import from File)
Connect credentials
Add your LLM credential (Claude/OpenAI) to the AI Agent node
Add Google Sheets OAuth2 credential to the getData node
Add Gmail OAuth2 credential to the Send a message in Gmail node
Point to your data
In the getData (Google Sheets) node, set the Document to your own sales sheet URL
Configure the email tool
Set a fixed recipient email and subject line in the Gmail node
Enable "Let the model fill this parameter" on the Message/Body field so the AI's generated HTML becomes the email content
Ensure the Gmail node's email type is set to HTML
Set the system prompt
Paste the agent system prompt (see prompt.md) into the AI Agent node's System Message field
Activate and test
Turn the workflow on
Open the chat trigger test panel and try: "Load the sheet and tell me how many rows there are"
Then try: "Email me total sales by customer state"
💬 Example Prompts
"Give me a summary of total sales and total tax collected."
"Which products generated the highest revenue? Email me the top 5."
"Email me a report of sales by Customer State."
"How many orders were delivered vs cancelled vs returned? Email the breakdown."
"Email me a full sales performance report — top products, top states, and total tax."

📁 Repository Structure
├── workflow.json     # n8n workflow export
├── prompt.md          # Full AI Agent system prompt
├── sample-data/       # Example sales sheet (anonymized)
└── README.md
