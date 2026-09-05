# AI-Powered Gmail Triage & Auto-Labeling Automation

An end-to-end automation built with **n8n** that monitors a Gmail inbox, classifies incoming emails with AI, and routes each one to the right action labeling, archiving to a spreadsheet, or creating a task without any manual sorting.

The workflow combines the **Gmail API**, a **Groq-hosted LLM (gpt-oss-20b)** for classification and extraction, **Google Sheets**, and **Google Tasks** to turn a messy inbox into a self-organizing system.

---

## How It Works

The automation polls Gmail every minute for unread messages that haven't already been processed (`is:unread -label:n8n-processed`).

Each new email's subject and snippet are sent to an **AI Text Classifier** node, which sorts it into one of eight categories: **Social**, **Promotions**, **Offers**, **Action Required**, **Personal**, **Receipts**, **Recruitment**, or **Uncategorized**.

From there, the email is routed down a category-specific path:

- **Social / Promotions** labeled accordingly in Gmail and marked as read. Social emails are also queued into workflow static data for a potential future digest.
- **Personal** simply labeled and left in the inbox for the user to read.
- **Action Required** labeled, then passed to an **AI Agent** that extracts a structured task (title, description, due date, priority) from the email content and automatically creates a corresponding **Google Task**.
- **Receipts** labeled, then parsed with regex/JS to pull out the vendor, amount, and date, which are appended as a new row in a **"My purchases" Google Sheet** for expense tracking.
- **Recruitment** labeled, then run through a **second AI classifier** that determines the hiring outcome (**Accepted**, **Refused**, or **Received**) so the email is triaged twice: once by type, once by hiring stage. The email is then marked as read.

Throughout, the workflow uses Gmail's label system to prevent re-processing the same email twice and to keep the inbox visually organized by category.

---

## Technologies Used

- n8n
- Gmail API (trigger, labeling, read status)
- Groq (LLM inference  `gpt-oss-20b`)
- LangChain Text Classifier & AI Agent nodes
- Google Sheets API
- Google Tasks API
- JavaScript (Code nodes)
