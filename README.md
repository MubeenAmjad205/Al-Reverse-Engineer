# 🕵️‍♂️ AI Reverse Engineer

An automated, LLM-driven pipeline designed to scrape, analyze, and reverse-engineer the algorithmic logic, workflows, and data pipelines of any target website. 

Built for technical analysts, security researchers, and developers, this tool bypasses visual noise (CSS/UI) and extracts pure operational logic, compiling it into a professional, human-readable executive report.

---

## ✨ Key Features

- 🕷️ **Automated Web Discovery:** Utilizes the TinyFish Search & Fetch APIs to recursively discover and scrape target domain pages.
- 🧠 **Algorithmic Analysis:** Uses advanced LLMs to identify decision trees, state flows, and control logic from raw HTML/Markdown.
- 🔄 **Multi-Provider Support:** Seamlessly switch between **Google Gemini**, **OpenAI**, and **OpenRouter** with a single configuration flag.
- 🛡️ **Dynamic API Key Rotation:** Built-in support for rotating up to 20 Gemini API keys automatically to bypass strict free-tier rate limits (`429 Resource Exhausted`).
- 🧩 **Smart Data Pipeline:** Automatically cleans boilerplate (cookie policies, footers), deduplicates content, and implements overlapping chunking strategies for large documents.
- 📦 **Comprehensive Reporting:** Automatically synthesizes hundreds of chunk analyses into a unified Executive Reverse Engineering Report and a searchable Source Index, packaged into a downloadable ZIP.

---

## 🚀 Quick Start

This tool is designed to be run efficiently in a Jupyter Notebook environment (like Google Colab).

### 1. Prerequisites (API Keys)
You will need API keys for the services you intend to use. Add these to your environment variables or Colab Secrets Manager:
- `TINYFISH_API_KEY` (Required for web scraping/search)
- `GEMINI_API_KEY` (If using Gemini)
- `OPENAI_API_KEY` (If using OpenAI)
- `OPENROUTER_API_KEY` (If using OpenRouter)

### 2. Configuration
At the top of the notebook, configure your target and preferred AI provider:

```python
LLM_PROVIDER = "gemini"  # Options: "gemini", "openai", "openrouter"

TARGET_DOMAIN = "example.com"
ROOT_URL = "https://example.com"
```

### 3. Execution
Run all cells sequentially. The pipeline will:
1. Search and discover URLs on the target domain.
2. Fetch and clean the markdown content.
3. Chunk the data and pass it to the selected LLM for algorithmic analysis.
4. Synthesize the findings into a final report.
5. Download a `reverse_engineering_outputs.zip` containing all raw data, analyses, and reports.

---

## ⚙️ Multi-Provider & Model Setup

The system is highly flexible and allows you to configure specific models for different stages of the pipeline (Chunk Analysis vs. Final Report Synthesis).

### Google Gemini (with Auto-Rotation)
If you are using Gemini's free tier, you may hit strict rate limits. You can bypass this by adding multiple keys to your Colab Secrets: `GEMINI_API_KEY_1`, `GEMINI_API_KEY_2`, etc. (up to 20 keys). The system will automatically detect rate limits and rotate the active key without crashing.
```python
GEMINI_ANALYSIS_MODEL = "gemini-2.5-flash" 
GEMINI_FINAL_REPORT_MODEL = "gemini-2.5-pro"
```

### OpenAI
```python
OPENAI_ANALYSIS_MODEL = "gpt-4o-mini"
OPENAI_FINAL_REPORT_MODEL = "gpt-4o"
```

### OpenRouter
OpenRouter provides access to almost any open-source or proprietary model.
```python
OPENROUTER_ANALYSIS_MODEL = "anthropic/claude-3-haiku" 
OPENROUTER_FINAL_REPORT_MODEL = "anthropic/claude-3.5-sonnet"
```

---

## 📂 Output Artifacts

Upon completion, the script generates a ZIP file containing:
- `/raw/` - Raw JSON outputs from TinyFish fetch requests.
- `/clean/` - Boilerplate-free, cleaned Markdown files per URL.
- `/chunks/` - Overlapping textual chunks ready for LLM consumption.
- `/findings/` - Individual algorithmic analysis reports for *each* chunk.
- `reverse_engineering_report.md` - The master synthesized executive report.
- `short_algorithm_summary.md` - A high-level brief.
- `source_index.md` - A complete index of all analyzed URLs and their properties.

---

## 🤝 Contributing
Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](../../issues).

## 📝 License
This project is open-source and available under the [MIT License](LICENSE).