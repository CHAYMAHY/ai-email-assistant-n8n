# 🤖 AI-Powered Email Assistant with n8n, OpenAI & Telegram

An intelligent, automated email management workflow built using **n8n**, **OpenAI (GPT-4o-mini)**, **Gmail API**, and **Telegram Bot API**. 

This workflow automatically monitors incoming emails, analyzes their urgency using AI, generates one-line summaries, drafts polite HTML responses, and requests human approval via Telegram before sending out any email.

---

## 🌟 Key Features

* 📩 **Automated Email Monitoring:** Continuously scans Gmail inbox for unread messages using the Gmail Trigger node.
* 🧠 **AI-Powered Analysis & Drafting:** Uses OpenAI (`gpt-4o-mini`) to summarize emails, detect if a reply is required (`Yes`/`No`), and generate formatted HTML draft replies.
* 🔀 **Smart Conditional Routing:** Automatically routes emails based on whether action is needed.
* 📱 **Human-in-the-Loop (HITL) Approval:** Sends notification alerts to Telegram with interactive **Approve / Disapprove** buttons.
* 📤 **Automated Dispatch:** Upon manual approval via Telegram, the workflow retrieves the draft and sends it out via Gmail API.

---

## 📐 Architecture & Workflow Diagram

```
[ Gmail Trigger ] 
        │
        ▼
[ OpenAI Summarizer & Drafter ]
        │
        ▼
[ Is Reply Needed? (If Node) ]
   ├── (No) ──► [ Telegram Notification: "No action needed" ]
   └── (Yes) ──► [ Create Gmail Draft ]
                       │
                       ▼
                 [ Telegram Approval Request ]
                       │
                 [ If Approved? ]
                    ├── (Approved) ──► [ Fetch Draft ] ──► [ Send Email via Gmail API ]
                    └── (Rejected) ──► [ Do Nothing ]
```

---

## 🛠️ Tech Stack & Integrations

* **Workflow Engine:** [n8n](https://n8n.io/)
* **AI Model:** OpenAI `gpt-4o-mini`
* **Email Platform:** Google Workspace / Gmail API (OAuth2)
* **Notifications & Approval:** Telegram Bot API (`sendAndWait` node)
* **API Protocol:** REST / HTTP Request (OAuth2)

---

## 🚀 Setup & Installation Instructions

### 1. Prerequisites
* An active **n8n** instance (Cloud or Self-Hosted).
* An **OpenAI API Key**.
* A **Telegram Bot Token** and your **Telegram Chat ID** (via `@BotFather`).
* A **Google Cloud Project** with Gmail API enabled and OAuth2 credentials set up.

### 2. Import the Workflow
1. Download the [`AI-Powered-Email-Assistant.json`](./AI-Powered-Email-Assistant.json) file from this repository.
2. In your n8n canvas, click **Workflows** > **Import from File**.
3. Select the `.json` file.

### 3. Configure Credentials
Update the nodes with your respective credentials:
* **OpenAI Node:** Select or add your OpenAI API Key.
* **Gmail Nodes:** Connect your Google OAuth2 account (requires `https://mail.google.com/` scope).
* **Telegram Nodes:** Add your Telegram Bot Credential and replace `YOUR_TELEGRAM_CHAT_ID` with your actual Chat ID.

### 4. Activate
Toggle the workflow status to **Active** to start monitoring your inbox.

---

## 🔒 Security & Privacy Notice
* All credentials, tokens, internal IDs, and private Telegram Chat IDs have been scrubbed from the provided template file.
* Always ensure your Google Cloud OAuth consent screen includes your test users when running in testing mode.

---

## 📜 License
This project is open-source and available under the [MIT License](LICENSE).
