<div align="center">

<img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n"/>
<img src="https://img.shields.io/badge/OpenAI-GPT--5_Mini-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI"/>
<img src="https://img.shields.io/badge/Status-Active-22c55e?style=for-the-badge" alt="Active"/>
<img src="https://img.shields.io/badge/License-MIT-3b82f6?style=for-the-badge" alt="MIT"/>

<br/><br/>

# 🤖 AI Coding Agent

### An intelligent coding assistant built with n8n — no backend required.

Powered by **OpenAI GPT-5 Mini** · Persistent **Conversation Memory** · Live **Tool Calling**

Ask it to write code, debug errors, run calculations, or fetch live API data — all in one n8n workflow.

<br/>

[🚀 Quick Start](#%EF%B8%8F-setup--installation) &nbsp;·&nbsp; [📐 Architecture](#-workflow-architecture) &nbsp;·&nbsp; [💬 Examples](#-example-interactions) &nbsp;·&nbsp; [🔮 Roadmap](#-planned-improvements)

<br/>

</div>

---

## ✨ Features

| Feature | Description |
|--------|-------------|
| 🧠 **Agentic Reasoning** | GPT-5 Mini autonomously decides which tool to call based on your question |
| 💬 **Conversation Memory** | Window Buffer Memory keeps last **10 messages** for multi-turn context |
| 🧮 **Calculator Tool** | Built-in math engine for numerical computations and expressions |
| ⚙️ **Code Executor** | Runs JavaScript snippets live and returns real output |
| 🌐 **API Request Tool** | Makes HTTP GET requests to any external endpoint |
| 💡 **Streaming Chat UI** | Built-in n8n chat with welcome screen, subtitle, and session memory |
| 🔁 **Up to 15 Iterations** | Agent can chain multiple tool calls per response for complex tasks |
| 🔗 **Webhook Ready** | Publicly accessible chat URL — connect any frontend instantly |

---

## 📸 Workflow Screenshot

> Full n8n agent workflow — Chat Trigger → AI Agent → Memory + 3 Tools

![AI Coding Agent Workflow](assets/workflow.png)

---

## 📐 Workflow Architecture

```
                        ┌──────────────────────────────┐
                        │        Chat Interface          │
                        │  (n8n Chat Trigger — Public)  │
                        │                               │
                        │  • Welcome Screen: ON          │
                        │  • Response Mode: Streaming    │
                        │  • Session: Loaded from Memory │
                        └──────────────┬────────────────┘
                                       │  main
                                       ▼
                        ┌──────────────────────────────┐
                        │        AI Coding Agent        │
                        │   (@n8n/langchain.agent v3.1) │
                        │                               │
                        │  • Max Iterations: 15         │
                        │  • Intermediate Steps: hidden  │
                        └───┬──────────┬───────┬────────┘
                            │          │       │
               ai_memory    │  ai_llm  │  tools│
                   ┌────────┘          │       └─────────────────────┐
                   │                   │                             │
      ┌────────────▼──────┐  ┌─────────▼──────────┐                 │
      │  Conversation     │  │  OpenAI GPT-5 Mini  │    ┌───────────▼──────────────┐
      │     Memory        │  │  (lmChatOpenAi)     │    │          Tools           │
      │                   │  │                     │    │                          │
      │  Window Buffer    │  │  • Model: gpt-5-mini│    │  🧮 Calculator           │
      │  Context: 10 msgs │  │  • Max Tokens: 4000 │    │  ⚙️  Code Executor (JS)  │
      │                   │  │  • n8n free credits │    │  🌐 API Request Tool     │
      └───────────────────┘  └─────────────────────┘    └──────────────────────────┘
```

### Node Reference

| Node | Type | Key Config |
|------|------|------------|
| **Chat Interface** | `chatTrigger v1.4` | Public URL · Streaming · Session from memory · Welcome screen ON |
| **AI Coding Agent** | `agent v3.1` | Max 15 iterations · Intermediate steps hidden |
| **OpenAI GPT-5 Mini** | `lmChatOpenAi v1.3` | Model: `gpt-5-mini` · Max tokens: 4000 |
| **Conversation Memory** | `memoryBufferWindow v1.4` | Context window: last **10 messages** |
| **Calculator** | `toolCalculator v1` | Built-in math expression evaluator |
| **Code Executor** | `toolCode v1.3` | Runs JavaScript · Returns query result |
| **API Request Tool** | `httpRequestTool v4.4` | Configurable HTTP GET endpoint |

---

## 🧠 System Prompt

The agent runs with this exact system prompt baked into the workflow:

```
You are an expert AI coding assistant with access to powerful tools.

Your capabilities include:
  1. Calculator      — for mathematical operations and calculations
  2. Code Executor   — to run JavaScript code snippets and demonstrate examples
  3. API Request Tool — to make HTTP requests to external APIs

When helping users:
  - Provide clear, concise explanations
  - Show working code examples using the Code Executor tool
  - Break down complex concepts into simple steps
  - Use the Calculator for any mathematical operations
  - Make API calls when needed to fetch real-time data
  - Remember previous conversations to provide contextual help

Always be helpful, accurate, and educational in your responses.
```

---

## 🛠️ Tech Stack

<div align="center">

![n8n](https://img.shields.io/badge/n8n-Workflow_Engine-EA4B71?style=flat-square&logo=n8n)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--5_Mini_·_4000_tokens-412991?style=flat-square&logo=openai)
![Memory](https://img.shields.io/badge/Memory-Window_Buffer_·_10_msgs-f97316?style=flat-square)
![Tools](https://img.shields.io/badge/Tools-Calculator_|_JS_Executor_|_HTTP-3b82f6?style=flat-square)
![Trigger](https://img.shields.io/badge/Trigger-Public_Chat_Webhook-22c55e?style=flat-square)

</div>

---

## 📁 Repository Structure

```
ai-coding-agent-n8n/
│
├── 📄 ai_coding_agent.json       ← Import this into n8n to run the full workflow
│
├── 📂 assets/
│   └── workflow.png              ← Workflow screenshot
│
└── README.md
```

> **Only one file needed** — import `ai_coding_agent.json` and the entire workflow is ready.

---

## ⚙️ Setup & Installation

### Prerequisites

- ✅ [n8n](https://n8n.io/) — self-hosted or [n8n Cloud](https://app.n8n.cloud)
- ✅ OpenAI API key — [Get one here](https://platform.openai.com/api-keys)
- ✅ Node.js v18+ *(only for self-hosted)*

---

### Step 1 — Clone the Repository

```bash
git clone https://github.com/your-username/ai-coding-agent-n8n.git
cd ai-coding-agent-n8n
```

### Step 2 — Start n8n

```bash
npx n8n
```
Open [http://localhost:5678](http://localhost:5678) in your browser.

### Step 3 — Import the Workflow

1. Go to **Workflows → Import from file**
2. Upload **`ai_coding_agent.json`**
3. The complete 7-node workflow loads automatically

### Step 4 — Add Your OpenAI Credentials

1. Go to **Credentials → New → OpenAI**
2. Paste your **OpenAI API Key**
3. Link it to the **OpenAI GPT-5 Mini** node

### Step 5 — (Optional) Configure the API Request Tool

1. Open the **API Request Tool** node
2. Replace the placeholder URL with your actual API endpoint
3. Add any required headers or auth

### Step 6 — Activate & Chat

1. Toggle **Activate** in the top-right
2. Click the **Chat** button to open the interface
3. You'll see the welcome screen — click **"Start Coding"** 🎉

---

## 💬 Example Interactions

<details>
<summary><b>🐍 Code Generation — Python</b></summary>

```
You   → Write a Python function to find all duplicates in a list.

Agent → Here's a clean solution:

        def find_duplicates(lst):
            seen = set()
            duplicates = []
            for item in lst:
                if item in seen:
                    duplicates.append(item)
                else:
                    seen.add(item)
            return list(set(duplicates))

        # Example
        print(find_duplicates([1, 2, 3, 2, 4, 3, 5]))
        # Output: [2, 3]

        Uses a set to track seen elements — O(n) time complexity.
```

</details>

<details>
<summary><b>☕ Debugging — Java</b></summary>

```
You   → Getting NullPointerException in Java. My code:
        String name; System.out.println(name.length());

Agent → The issue: name is declared but never initialized.
        In Java, uninitialized local variables are null by default.
        Calling .length() on null throws NullPointerException.

        Fix:
        String name = "";               // initialize to empty string
        System.out.println(name.length()); // Output: 0

        Always initialize variables before use!
```

</details>

<details>
<summary><b>🧮 Math Calculation — uses Calculator Tool</b></summary>

```
You   → What is the time complexity of merge sort and
        how many operations for n = 1000?

Agent → [invokes Calculator tool]

        Time complexity: O(n log n)
        For n = 1000:
          log₂(1000) ≈ 9.96
          1000 × 9.96 ≈ 9,966 operations

        Much better than bubble sort's ~499,500 for the same input!
```

</details>

<details>
<summary><b>⚙️ JavaScript Execution — uses Code Executor</b></summary>

```
You   → Show me how Array.reduce() works with an example.

Agent → [invokes Code Executor]

        const numbers = [1, 2, 3, 4, 5];
        const sum = numbers.reduce((acc, curr) => acc + curr, 0);
        console.log(sum); // 15

        reduce() takes a callback with (accumulator, currentValue).
        It processes each element left-to-right, passing the result
        forward until a single value remains.
```

</details>

<details>
<summary><b>🌐 API Fetch — uses API Request Tool</b></summary>

```
You   → Fetch data from the configured API endpoint.

Agent → [invokes API Request Tool]

        Successfully fetched response:
        { "status": "ok", "data": [ ... ] }

        Here's what the response means...
```

</details>

---

## 🔮 Planned Improvements

- [ ] 🐙 GitHub API tool — fetch files and review code from any repository
- [ ] 📱 Telegram / Slack trigger — chat with the agent from messaging apps
- [ ] 🔍 Web search tool — look up docs and Stack Overflow answers live
- [ ] ⚛️ React frontend — custom UI connected via the public webhook URL
- [ ] 🐍 Python executor — extend Code Executor to support Python alongside JS
- [ ] ☁️ Deploy on n8n Cloud with a custom domain

---

## 🎓 About the Developer

<div align="center">

**Malla Sai Vardan**
B.Tech Computer Science & Engineering — 3rd Year
RV Institute of Technology (RVIT), Guntur, Andhra Pradesh
*Building AI agents and automation workflows*

<br/>

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/malla-sai-vardan/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/saivardanmalla)

</div>

---

## 📄 License

This project is licensed under the **MIT License** — free to use, modify, and distribute.

---

<div align="center">

⭐ **Found this useful? Give it a star!** ⭐
*It helps other developers discover this project.*

</div>
