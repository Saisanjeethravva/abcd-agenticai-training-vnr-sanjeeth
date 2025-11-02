# 🧠 AI-Powered RSS Feed Summarizer — End-to-End Automation Workflow

## 🌐 Overview
This **n8n workflow** automates the process of fetching RSS feeds, summarizing them using AI, and sending formatted digests through Telegram or Email.  
It is an **end-to-end AI-driven content pipeline** combining automation, feed parsing, summarization, and publishing.

---

## ⚙️ Features
- 🔁 **Automated RSS Fetching** via n8n’s RSS node  
- 🧩 **Looping & Filtering** to handle multiple feeds  
- 🧠 **AI Summarization** using Google Gemini via n8n’s LangChain integration  
- 💌 **Email or Telegram Delivery** of AI summaries  
- 📂 **JSON & HTML File Outputs** for archiving or sharing  

---

## 🧭 Workflow Overview

### 1️⃣ Configuration and Scheduling
- **Schedule Trigger:** Sets the workflow frequency (e.g., daily 8 AM)
- **Config Node:** Loads parameters like:
  - `inputFile`: path to your RSS feed list  
  - `outputFile`: path to save summaries  
  - `active` flags for enabling/disabling nodes

---

### 2️⃣ Feed Extraction and Looping
- **Read/Write Files from Disk:** Reads your feed list from a `.csv` or `.json` file  
- **Extract from File:** Parses and converts data into n8n JSON format  
- **Loop Over Items:** Iterates through each feed URL and sends it to the **RSS Read** node  

---

### 3️⃣ Fetch and Format Feed Items
- **RSS Read1:** Reads latest posts from each feed  
- **Limit Node:** Restricts how many items to fetch (e.g., 3 per site)  
- **Add New Fields:** Adds metadata like site name and date  
- **Group HTML Items:** Combines fetched articles into an HTML-friendly block  

---

### 4️⃣ AI Summarization
- **If Node:** Checks whether AI summarization is active  
- **HTML → Markdown → AI Agent → Markdown → HTML:**  
  Transforms content, summarizes via **Gemini**, and reconverts to HTML.  
- **Google Gemini Chat Model:** Connects to Google’s LLM for text summarization  

---

### 5️⃣ Output and Delivery
- **Set HTML Block / Page Nodes:** Build final email/HTML layout  
- **Concatenate HTML:** Combines all site summaries  
- **Convert to File:** Saves the output locally  
- **Telegram Node:** Sends summarized text directly to a Telegram chat  
- **Email Node (optional):** Sends formatted digest to inbox  

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
