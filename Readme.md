# 🧠 AI-Powered RSS Feed Summarizer — End-to-End Automation Workflow

## 🌐 Overview
This n8n workflow automates the entire process of fetching RSS feeds, summarizing their contents using an AI model, and sending formatted digests through Telegram or email.  
It simplifies AI-driven news aggregation by combining automation, data parsing, and LLM-based summarization in a single workflow.

---

## ⚙️ Features
- 🔁 Automated feed fetching via **RSS Read** node  
- 🧩 Intelligent batching and filtering  
- 🧠 AI summarization using **Google Gemini** through n8n’s LangChain integration  
- 💌 Optional delivery through **Telegram** or HTML-formatted email  
- 🗂 Structured output files for further analysis or storage  

---

## 🧭 Workflow Overview

### 1️⃣ Configuration and Scheduling
- **Schedule Trigger:** defines when the workflow runs (daily, hourly, etc.)
- **Config Node:** loads parameters such as  
  - Input file path for feed URLs → `/data/your-feeds-2.csv`  
  - Output file path → `/data/output.json`  
  - Email and AI toggles (`active` flags)

### 2️⃣ Feed Extraction and Looping
- **Read/Write Files from Disk:** reads the CSV/JSON containing feed links  
- **Extract from File:** parses it into structured JSON  
- **Loop Over Items:** iterates through each feed URL and sends them to the RSS Reader

### 3️⃣ Fetch and Format Feed Items
- **RSS Read1:** reads the latest posts from each feed URL  
- **Limit Node:** restricts how many posts are fetched (`rss.maxitems`)  
- **Add New Fields:** adds site name and converts items into clickable HTML links  
- **Group HTML Items:** combines items into a single HTML block

### 4️⃣ AI-Based Summarization
- **If Output to Message1:** checks whether AI summarization is enabled  
- **HTML → Markdown → AI Agent → Markdown → HTML:**  
  transforms fetched content, summarizes via Gemini, and re-formats to HTML  
- **Google Gemini Chat Model:** provides the LLM connection for summarization

### 5️⃣ Output Generation
- **Set HTML Block / Page Nodes:** build the newsletter-style HTML layout  
- **Concatenate HTML:** aggregates all summaries  
- **Convert to File:** saves output locally  
- **Send Telegram Message:** delivers digest to Telegram chat

---

## 🧾 Example Feed File

**`your-feeds-2.csv`**
```csv
site,url,active
TechCrunch,https://techcrunch.com/feed/,True
The Verge,https://www.theverge.com/rss/index.xml,True
BBC News,https://feeds.bbci.co.uk/news/rss.xml,True
Wired,https://www.wired.com/feed/rss,True
NASA,https://www.nasa.gov/rss/dyn/breaking_news.rss,True
Analytics Vidhya,https://feeds.feedburner.com/AnalyticsVidhya,True
