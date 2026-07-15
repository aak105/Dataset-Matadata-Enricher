# 📚 Dataset Metadata Augmenter

> AI-powered metadata enrichment for research datasets with two-agent quality scoring and OpenMetadata integration

![MIT License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Version](https://img.shields.io/badge/version-2.1.0-blue.svg)
![OpenMetadata](https://img.shields.io/badge/OpenMetadata-v1.3+-green.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

## Overview

Dataset Metadata Augmenter is a browser-based tool that helps researchers and data professionals catalog datasets with AI-powered metadata extraction. It uses a two-agent architecture (Proponent + Judge) inspired by the World Bank's AI metadata framework to ensure quality.

**🌐 Live Demo:** [aak105.github.io/Dataset-Metadata-Enricher](https://aak105.github.io/Dataset-Metadata-Enricher/)

---

## What's New in v2.1

### ⚖️ Quality Scoring System

Two-agent architecture for metadata quality assurance:

- **Proponent Agent** generates metadata values
- **Judge Agent** auto-scores each field 0-10 using a quality rubric
- **Editable feedback** — modify judge suggestions before regenerating
- **Accept / Regenerate / Dismiss** actions per field
- **Up to 3 regeneration attempts** per field with feedback loop
- **Quality Summary Card** with overall score and progress bar

### 🏛️ Ashoka Datalake Preset

18-field schema for social sector datasets in India, covering Domain/Cluster, Coverage, Methodology Notes, Data Quality Notes, and more.

### 🔗 Browse OpenMetadata Catalog

Browse tables directly from OpenMetadata:
- Search by name, description, or FQN
- One-click load with schema + sample data
- Pre-populates title, description, source URL

### ⚡ Groq Provider

Fast & Free provider with 6 models including Llama 3.3 70B. Free tier: 1,000 requests/day.

### 🎨 Multi-Page Site

- Landing page with hero section, feature cards, comparison table
- Getting Started Guide with quality rubric documentation
- Light/dark theme toggle (persistent)
- Modern DM Sans typography, glassmorphism nav

### 📥 Smart Schema Import

- Supports 3 JSON formats (native, Ashoka `{Field, Description}`, string array)
- No more auto-enum detection — AI inference enabled for all fields
- Auto-detects field types from name (URL, longtext, date, tags)

### 🛡️ CORS Proxy Reliability

Detects and skips hijacked proxies that serve ads instead of requested content. Uses 5 reliable proxies with automatic fallback.

---

## Full Feature List

| Feature | Description |
|---------|-------------|
| 🤖 **Multi-LLM Support** | Anthropic, OpenAI, Google Gemini, Mistral, Perplexity, Groq |
| 🏠 **Custom / Local Models** | Ollama, LM Studio, vLLM, any OpenAI-compatible API |
| ⚖️ **Quality Scoring** | Two-agent Proponent-Judge with editable feedback |
| 📊 **OpenMetadata Integration** | Push and Browse datasets from OM catalog |
| 🌍 **6 Schema Presets** | 5 World Bank + Ashoka Datalake |
| 💾 **Custom Schemas** | Save and reuse metadata templates |
| 🔍 **DuckDuckGo Web Search** | Free web search context (no API key) |
| 🌐 **URL Fetching** | Extract metadata from source URLs with proxy fallbacks |
| 📈 **Auto Statistics** | Column-level fill rates, unique counts, samples |
| 🎨 **Dark/Light Theme** | Toggle with persistence |
| 📄 **Multi-Page Site** | Home, Guide, Tool pages with modern design |

---

## Quality Scoring Rubric

| Score | Rating | Description |
|-------|--------|-------------|
| 9-10 | 🟢 Excellent | Clear, precise, contextually relevant, aligned with standards |
| 7-8 | 🟢 Good | Mostly clear and accurate, minor issues |
| 5-6 | 🟡 Satisfactory | Understandable but lacks precision or specificity |
| 3-4 | 🔴 Needs Improvement | Lacks clarity, broad, or technically inaccurate |
| 0-2 | 🔴 Poor | Unclear, irrelevant, or unusable |

---

## Quick Start

### Option 1: Use Online (No Install)
Visit [aak105.github.io/Dataset-Metadata-Enricher](https://aak105.github.io/Dataset-Metadata-Enricher/)

### Option 2: Run Locally
```bash
git clone https://github.com/aak105/Dataset-Metadata-Enricher.git
cd Dataset-Metadata-Enricher
python3 server.py  # starts CORS proxy at http://localhost:3000
```

---

## Usage

1. **Configure LLM** — Settings tab → pick provider → enter API key
2. **Select Schema** — Load a preset (Ashoka, Microdata, etc.) or customize
3. **Upload or Browse** — Drag CSV/Excel, or browse OpenMetadata
4. **Generate Metadata** — Click "Augment with AI"
5. **Review Quality** — Check scores, edit feedback, regenerate low-scoring fields
6. **Export or Push** — CSV/Excel/JSON download, or push to OpenMetadata

---

## Schema Presets

| Preset | Fields | Best For |
|--------|--------|----------|
| 📊 Microdata (DDI 2.5) | 31 | Surveys (NSSO, PLFS), censuses |
| 📄 Document | 33 | Reports, PDFs, publications |
| 📈 Timeseries | 33 | Indicators (WDI, RBI stats) |
| 📋 Table | 30 | Cross-tabulations, aggregates |
| 🗺️ Geospatial (ISO 19115) | 40 | GIS data, satellite imagery |
| 🏛️ Ashoka Datalake | 18 | Social sector datasets (India) |

---

## Supported LLM Providers

| Provider | Models | Web Search | Free Tier |
|----------|--------|-----------|-----------|
| **Anthropic** | Claude Opus/Sonnet/Haiku 4.x | ❌ | ❌ |
| **OpenAI** | GPT-5.4, GPT-4.1, GPT-4o | ✅ (Responses API) | ❌ |
| **Google** | Gemini 3.1 Pro, 2.5 Pro/Flash | ❌ | ✅ generous |
| **Mistral** | Magistral, Codestral | ❌ | Limited |
| **Perplexity** | Sonar, Sonar Pro/Reasoning | ✅ built-in | ❌ |
| **Groq** | Llama 3.3, Mixtral, Gemma | ❌ | ✅ 1000/day |
| **Custom / Local** | Ollama, LM Studio, vLLM | ❌ | ✅ (self-hosted) |

**Bonus:** DuckDuckGo web search works with any provider.

---

## OpenMetadata Setup

1. Install OpenMetadata via Docker (v1.3.8+ recommended)
2. Get JWT token: Settings → Bots → ingestion-bot → Copy Token
3. Run the proxy: `python3 server.py`
4. Configure in Settings:
   - URL: `http://localhost:8585`
   - JWT Token: (paste yours)
5. Test Connection → Push datasets or Browse catalog

---

## Project Structure

```
Dataset-Metadata-Enricher/
├── index.html          # Main application (standalone, 257KB)
├── server.py           # CORS proxy for OpenMetadata
├── README.md           # This file
├── CHANGELOG.md        # Version history
├── CONTRIBUTING.md     # Contribution guide
└── LICENSE             # MIT
```

---

## Roadmap

### Completed in v2.1
- ✅ Quality scoring with two-agent architecture
- ✅ Ashoka Datalake schema preset
- ✅ Browse OpenMetadata catalog
- ✅ Groq provider
- ✅ Multi-page site design
- ✅ Theme toggle
- ✅ Smart schema import
- ✅ CORS proxy reliability improvements

### v2.2 (Planned)
- [ ] Vocabulary alignment (constrained prompts + fuzzy matching)
- [ ] PDF table extraction
- [ ] Batch push multiple datasets
- [ ] Column-level PII detection
- [ ] Indian government data source recipes (PAI, MoSPI, UPAg, NFHS)

### v3.0 (Future)
- [ ] React migration
- [ ] Team collaboration
- [ ] Bidirectional PostgreSQL sync via OpenMetadata

---

## Privacy & Security

- ✅ Runs entirely in your browser
- ✅ No tracking, no analytics, no telemetry
- ✅ API keys in memory only, never persisted
- ✅ Local data storage via localStorage
- ✅ Direct LLM calls — data goes only to your chosen provider

---

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## License

MIT License — see [LICENSE](LICENSE).

---

## Author

**Aakash Sharma**  
Dataset Lead, Ashoka University Social Datalake Project

- [LinkedIn](https://www.linkedin.com/in/aakashsharma8a6888131/)
- [GitHub](https://github.com/aak105)

---

## Acknowledgments

- [World Bank AI Metadata Framework](https://blogs.worldbank.org/en/opendata/efficient-metadata-enhancement-with-ai-for-better-data-discovera) by Aivin Solatorio and Olivier Dupriez — inspired the quality scoring approach
- [World Bank Metadata Schemas](https://github.com/worldbank/metadata-schemas) for schema standards
- [OpenMetadata](https://open-metadata.org/) for the data catalog platform
- [PapaParse](https://www.papaparse.com/), [SheetJS](https://sheetjs.com/) for parsing
- [DuckDuckGo](https://duckduckgo.com/) for free web search

---

**Made with ❤️ for researchers working with secondary data**
