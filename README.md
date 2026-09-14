# An Extensible LLM-Powered Crowdsourcing Pipeline for Real-Time Urban Flood Monitoring: The Case of Surabaya

[![Template: IEEE](https://img.shields.io/badge/Template-IEEEtran-blue.svg)](https://www.ieee.org/conferences/publishing/templates.html)
[![Inference: Groq LPU](https://img.shields.io/badge/LLM%20Inference-Groq%20LPU-orange.svg)](https://groq.com/)
[![Orchestration: n8n](https://img.shields.io/badge/Orchestrator-n8n-red.svg)](https://n8n.io/)

Official LaTeX source files, diagrams, and documentation repository for the research paper: **"A Low-Latency LLM Architecture for Real-Time Urban Flood Sensing: The Case of Surabaya"** (The SIBANJIR framework).

---

## 📌 Abstract

Urban flooding poses severe threats to metropolitan mobility and infrastructure. Conventional disaster monitoring often suffers from verification delays and limited telemetry coverage. Conversely, citizens proactively broadcast unstructured, colloquial eyewitness reports (e.g., Javanese Suroboyoan vernacular) on social media platforms. 

**SIBANJIR** presents an extensible, automated end-to-end crowdsourcing pipeline leveraging Large Language Models (LLMs) for real-time flood detection, cognitive zero-shot geoparsing, and multi-tier dissemination. Evaluated against a comprehensive real-world dataset ($N=850$), key technical highlights include:
- **Headless Ingestion**: Selenium-based crawler wrapped in a Flask microservice with cookie session persistence (`fb_cookies.json`) and PM2 process monitoring.
- **Upstream Deduplication Gate**: Cross-query fuzzy matching via n8n and MongoDB Atlas that suppresses redundant incoming reports by **76.4%**, drastically minimizing token usage and cloud operational costs[cite: 4].
- **Cognitive Information Extraction & Geoparsing**: Zero-shot entity parsing using **Llama-3.1-8b-instant** on high-throughput **Groq LPUs** (achieving an exceptional **97.1% F1-score** in relevance classification and **89.4% relaxed spatial accuracy** without external geocoding APIs)[cite: 4].
- **Multi-Tier Dissemination**: Real-time push alerts via Telegram broadcast channel (`t.me/SiBanjir_Jatim`), interactive two-way route inquiry bot (`@SiBanjir_Bot`), and the Metabase spatial analytics portal (`pantausurabaya.my.id`)[cite: 4].
- **Ultra-Low Latency**: Demonstrates an end-to-end processing latency of **7.50 seconds**, providing a vital operational leap for real-time smart city disaster management[cite: 4].

---

## 🏗️ System Architecture

The pipeline consists of five decoupled layers:
1. **Tier 1 (Ingestion):** Headless Selenium scraping Facebook E100 Suara Surabaya feed, exposed as an on-demand Flask REST API.
2. **Tier 2 (Orchestration):** n8n event-driven state manager and scheduled workflow executor running on Linux Systemd.
3. **Tier 3 (Upstream Deduplication):** Pre-inference MongoDB database check using a normalized signature and Levenshtein fuzzy matching within a 6-hour temporal window.
4. **Tier 4 (Cognitive Processing):** Llama-3.1-8b zero-shot extraction via Groq API, followed by regex sanitization and coordinate bounding box enforcement.
5. **Tier 5 (Storage & Dissemination):** MongoDB Atlas cloud storage feeding Telegram push broadcasts, a conversational bot, and Metabase spatial analytics.

---

## 📂 Repository Structure

```text
CENIM_FLOOD_MONITORING/
│
├── img/                      # Manuscript figures, architecture diagrams, and charts
├── .gitignore                # Git ignore rules for LaTeX auxiliary files
├── conference_101719.tex     # Main LaTeX document source file of the paper
├── IEEEtran.tex              # Official IEEE conference document class file
├── references.bib            # BibTeX bibliography file
└── README.md                 # Project documentation

```

---

## 🛠️ Compilation Instructions
Prerequisites
Make sure you have a working TeX distribution installed (e.g., TeX Live, MacTeX, or MiKTeX), or import this repository directly into Overleaf.

Building Locally via CLI
To compile the document with citations properly resolved, run the standard build sequence:

pdflatex conference_101719
bibtex conference_101719
pdflatex conference_101719
pdflatex conference_101719

Or using latexmk (recommended):
latexmk -pdf conference_101719.tex

---

## 👥 Authors
Devanka Raditanti Citasevi

Erdi Yanto

Ahmad Zaini

Arief Kurniawan

Arta Kusuma Hernanda

Department of Computer Engineering, Sepuluh Nopember Institute of Technology (ITS), Surabaya, Indonesia.