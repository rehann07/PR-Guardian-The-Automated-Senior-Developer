# 🛡️ PR Guardian: The Automated Senior Developer

> **2025 Kaggle AI Agents Capstone Project Submission**
> *Track C: Enterprise Agents*

PR Guardian is a multi-agent system designed to automate the "first pass" of code reviews. It acts as an intelligent gatekeeper, using parallel AI agents to instantly detect security flaws, enforce style standards, and identify performance bottlenecks before a human reviewer ever sees the code.

## 🚀 Key Features

* **⚡ Parallel Orchestration:** Uses `concurrent.futures` to run three specialized agents simultaneously, delivering reviews in < 3 seconds.
* **🔒 Security Agent (The Paranoid):** Combines deterministic regex tools with Llama 3.3 reasoning to catch hardcoded secrets (`sk-...`) and logic vulnerabilities (SQLi).
* **🎨 Style Agent (The Pedant):** Enforces PEP8, proper variable naming (snake_case), and clean code practices.
* **🚀 Performance Agent (The Architect):** Identifies $O(n^2)$ algorithmic inefficiencies and suggests specific built-in optimizations (e.g., using `set()` vs `list()`).
* **🛠️ Robust & Resilient:** Implements exponential backoff retry logic to handle API rate limits gracefully.

## 🏗️ Architecture

The system follows a **Manager-Worker Pattern**:

1.  **Orchestrator:** Ingests the code diff and spawns thread workers.
2.  **Workers:** Three specialized prompts running on **Llama 3.3 (70B)** via the **Groq API** for blazing-fast inference (~300 tokens/s).
3.  **Tooling:** Custom Python-based `scan_for_secrets` tool injected into the Security Agent.
4.  **Observability:** Real-time logging of agent execution and timing.

## 🛠️ Installation

### Prerequisites
* Python 3.8+
* A free [Groq API Key](https://console.groq.com/keys)

### Setup

1.  **Clone the repository**
    ```bash
    git clone [https://github.com/yourusername/pr-guardian.git](https://github.com/yourusername/pr-guardian.git)
    cd pr-guardian
    ```

2.  **Install dependencies**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Configure API Key**
    * **Option A (Environment Variable - Recommended):**
        ```bash
        export GROQ_API_KEY="your_groq_api_key_here"
        ```
    * **Option B (Direct Edit):**
        Edit `pr_guardian.py` and set the fallback key variable (not recommended for public repos).

## 💻 Usage

Run the main script to analyze the sample "bad code" snippet provided in `__main__`:

```bash
python pr_guardian.py
````

**Expected Output:**

```text
==================================================
🚦 STARTING PR GUARDIAN (Powered by Llama 3 on Groq)
==================================================
🤖 SecurityAgent: Starting analysis...
🤖 StyleAgent: Starting analysis...
🤖 PerfAgent: Starting analysis...
==================================================
✅ REVIEW COMPLETE in 2.57 seconds
==================================================
🛡️ [SECURITY REPORT]
...
```

## 📂 Project Structure

```text
pr-guardian/
├── README.md           # Documentation
├── pr_guardian.py      # Main Agent Code (Orchestrator + Agents)
├── requirements.txt    # Dependencies
└── assets/             # Screenshots/images for this README
```

## 🔮 Future Roadmap

  * **GitHub App Integration:** Deploy as a bot that comments directly on PRs.
  * **Auto-Fix Agent:** A fourth agent that generates the corrected code block to apply fixes with one click.
  * **RAG Knowledge Base:** Connect to internal company wikis to enforce organization-specific coding guidelines.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](https://www.google.com/search?q=LICENSE) file for details.

-----

*Created for the [Kaggle AI Agents Intensive Course](https://www.kaggle.com/learn-guide/5-day-agents) Capstone Project.*

```
```
