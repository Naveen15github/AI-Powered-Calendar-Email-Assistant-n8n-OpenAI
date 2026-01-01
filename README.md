# 🤖 AI-Powered Calendar & Email Assistant (n8n + OpenAI)

An intelligent, end-to-end automation workflow built using **n8n**, **OpenAI**, **Google Calendar**, and **Gmail** that enables natural language scheduling, calendar management, and professional email communication — all handled autonomously by an AI agent.

This project demonstrates how modern AI agents can reason, coordinate tools, and execute real-world tasks with minimal human intervention.

---

![Alt text](https://github.com/Naveen15github/AI-Powered-Calendar-Email-Assistant-n8n-OpenAI-/blob/c8d501b3736f58ae9253eb0662f9026f8ada26ca/Screenshot%20(319).png)


## 🚀 Overview

This workflow allows users to interact with a conversational AI that can:

* Understand natural language scheduling requests
* Automatically create Google Calendar events
* Send professionally formatted Gmail notifications
* Maintain conversation context across multiple messages
* Coordinate multiple tools without manual branching logic

The system is fully automated and designed for real-world usage such as meeting scheduling, reminders, and professional communication.
---
# Proof Of Work

![Alt text](https://github.com/Naveen15github/AI-Powered-Calendar-Email-Assistant-n8n-OpenAI-/blob/c8d501b3736f58ae9253eb0662f9026f8ada26ca/Screenshot%20(317).png)
![Alt text](https://github.com/Naveen15github/AI-Powered-Calendar-Email-Assistant-n8n-OpenAI-/blob/c8d501b3736f58ae9253eb0662f9026f8ada26ca/Screenshot%20(318).png)
![Alt text](https://github.com/Naveen15github/AI-Powered-Calendar-Email-Assistant-n8n-OpenAI-/blob/c8d501b3736f58ae9253eb0662f9026f8ada26ca/Screenshot%20(320).png)
![Alt text](https://github.com/Naveen15github/AI-Powered-Calendar-Email-Assistant-n8n-OpenAI-/blob/c8d501b3736f58ae9253eb0662f9026f8ada26ca/Screenshot%20(321).png)

---

## 🧠 Architecture Overview

```
User (Chat Interface)
        │
        ▼
Chat Trigger (Webhook)
        │
        ▼
AI Agent (Decision & Reasoning Engine)
        │
 ┌──────┴─────────┐
 │                │
 ▼                ▼
Google Calendar   Gmail
(Event Creation)  (Email Notification)
```

---

## 🧩 Workflow Components

### 1️⃣ Chat Trigger (Entry Point)

**Node:** `@n8n/n8n-nodes-langchain.chatTrigger`
**Version:** 1.4

* Acts as the entry point for user messages
* Receives conversational input via webhook
* Generates session-based context for each user

**Webhook URL**

```
https://naveeng15.app.n8n.cloud/webhook/d905392e-8c17-467b-88a5-8fb075697de6/chat
```

**Outputs:**

* `sessionId`
* `chatInput`
* `action`

---

### 2️⃣ AI Agent (Core Orchestration Engine)

**Node:** `@n8n/n8n-nodes-langchain.agent`
**Version:** 3.1

This is the brain of the workflow.

**Responsibilities:**

* Interprets user intent
* Decides which tools to use
* Chains multiple actions intelligently
* Produces final user-facing responses

**System Prompt (Excerpt):**

```
You are a helpful assistant to send a Gmail message.
Add emojis and ensure clean formatting.

Best Regards,
Naveen G

The current date and time is: {{ $now }}
```

**Capabilities:**

* Tool selection and chaining
* Contextual reasoning
* Dynamic content generation
* Autonomous decision-making

---

### 3️⃣ OpenAI Chat Model

**Node:** `@n8n/n8n-nodes-langchain.lmChatOpenAi`
**Model:** `gpt-4.1-mini`

**Purpose:**

* Natural language understanding
* Date/time extraction
* Content generation
* Reasoning and planning

**Configuration:**

* Response Mode: Enabled
* Timeout: 60 seconds
* Retry Attempts: 2

---

### 4️⃣ Conversation Memory

**Node:** `@n8n/n8n-nodes-langchain.memoryBufferWindow`

**Purpose:**

* Maintains conversational continuity
* Stores recent interactions per session

**Configuration:**

* Context Window: 5 messages
* Session Key: `{{ $json.sessionId }}`

---

### 5️⃣ Google Calendar Integration

**Node:** `n8n-nodes-base.googleCalendarTool`

**Functionality:**

* Creates calendar events dynamically
* Extracts date & time from natural language
* Automatically sets reminders

**Key Parameters:**

* Calendar: Primary
* Start Time: `{{ $fromAI('Start') }}`
* End Time: `{{ $fromAI('End') }}`
* Default Reminders: Enabled

---

### 6️⃣ Gmail Integration

**Node:** `n8n-nodes-base.gmailTool`

**Purpose:**

* Sends professionally formatted emails
* Uses AI-generated subject and body content

**Features:**

* Emoji-enhanced formatting
* Calendar links included
* Clean and readable structure

**Dynamic Fields:**

* To: `{{ $fromAI('To') }}`
* Subject: `{{ $fromAI('Subject') }}`
* Message Body: `{{ $fromAI('Message') }}`

---

## 🔁 Execution Flow (Example)

**User Input:**

> “Schedule a Google Meet on Jan 10, 2026 at 9 AM IST and email me the details.”

### Step-by-Step Flow

1. Chat Trigger receives message
2. AI Agent interprets intent
3. Memory loads past context
4. Calendar event is created
5. Google Meet link generated
6. Email drafted and sent
7. Confirmation returned to user

**Execution Time:** ~8 seconds total

---

## 📊 Performance Metrics

| Component           | Avg Time | Status |
| ------------------- | -------- | ------ |
| Chat Trigger        | 0 ms     | ✅      |
| AI Agent            | ~1.6s    | ✅      |
| OpenAI Model Calls  | ~4.6s    | ✅      |
| Calendar Tool       | ~0.4s    | ✅      |
| Gmail Tool          | ~0.3s    | ✅      |
| **Total Execution** | **~8s**  | ✅      |

---

## 🧠 Key Features

* ✅ Natural language understanding
* ✅ Multi-tool orchestration
* ✅ Context-aware memory
* ✅ Automatic date & time parsing
* ✅ Clean, professional email formatting
* ✅ Fully autonomous execution

---

## ⚙️ Customization Options

### Modify AI Behavior

* Adjust system prompt for tone and style
* Change default meeting duration
* Customize email formatting

### Extend Capabilities

* Add Slack or WhatsApp notifications
* Store logs in a database
* Integrate CRM systems

### Memory Control

* Increase or decrease conversation window
* Enable long-term memory via external storage

---

## 🔐 Security & Reliability

* OAuth2 authentication for Google services
* Secure credential storage in n8n
* Session-based access control
* Controlled API usage with retries

---

## 🚀 Deployment

**Chat Endpoint:**

```
https://naveeng15.app.n8n.cloud/webhook/d905392e-8c17-467b-88a5-8fb075697de6/chat
```

**Requirements:**

* n8n (self-hosted or cloud)
* OpenAI API Key
* Google OAuth credentials
* Active workflow state

---

## 📌 Use Cases

* Meeting scheduling
* Interview coordination
* Client follow-ups
* Task reminders
* Calendar-based automation

---

## 👤 Author

**Naveen G**
AI & Automation Engineer
Focused on building intelligent workflow automation using AI, cloud, and low-code platforms.


