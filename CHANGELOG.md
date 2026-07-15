# Changelog

All notable changes to the Dataset Metadata Augmenter project.

## [2.1.0] - 2026-07-15

### Added

**Quality Scoring System (Two-Agent Architecture)**
- Proponent-Judge architecture inspired by the World Bank AI metadata framework
- Judge Agent auto-scores each field 0-10 using a quality rubric after generation
- Quality Summary Card with overall score, progress bar, and per-category counts
- Per-field visual indicators (🟢 🟡 🔴)
- Editable feedback — modify the judge's suggestions before regenerating
- Accept / Regenerate / Dismiss actions per field
- Up to 3 regeneration attempts per field with feedback loop
- Re-Judge All button to re-assess after manual edits
- Quality rubric documented in the Guide page

**Ashoka Datalake Schema Preset**
- 18-field preset for social sector datasets in India
- Fields include Domain/Cluster, Coverage (Spatial/Temporal), Methodology Notes, Data Quality Notes
- Purple gradient button in the Schema tab

**Browse OpenMetadata Catalog**
- New "🔗 Browse Catalog" tab in navigation
- Quick access button in Datasets tab
- Fetches tables from OpenMetadata via the existing CORS proxy
- Search/filter by table name, description, or FQN
- One-click "Load →" to import a table as a dataset with sample data
- Pre-populates title, description, and source URL from OpenMetadata

**Groq Provider**
- New "Groq (Fast & Free)" provider
- 6 models: Llama 3.3 70B, Llama 3.1 8B, Llama3 70B/8B, Mixtral 8x7B, Gemma 2 9B
- Uses OpenAI-compatible format
- Free tier: 1,000 requests/day

**UI Redesign — Multi-Page Site**
- Professional landing page with hero section, feature cards, comparison table
- Getting Started Guide with step-by-step documentation and quality rubric
- Tool page (existing app functionality preserved)
- Site navigation: Home | Guide | GitHub | Theme Toggle | Open Tool
- Modern design system: DM Sans + JetBrains Mono, indigo→purple→pink gradient
- Glassmorphism navigation bar

**Light/Dark Theme Toggle**
- Toggle button (☀️/🌙) in navigation
- Persists preference to localStorage
- Respects `prefers-color-scheme` on first visit
- All CSS variables adapt via `[data-theme]` attribute

**Smart Schema Import**
- Supports 3 JSON formats: native `{name, type}`, Ashoka `{Field, Description}`, plain string array
- Auto-converts unfamiliar formats to internal schema
- Removed auto-enum detection (was forcing enum on Domain, Coverage, etc.)
- AI Infer enabled by default for all fields except URL/Link

**CORS Proxy Hijack Detection**
- Removed unreliable proxies (corsproxy.io, corsproxy.org) that started serving VPN ads
- Added content validation to detect hijacked responses
- Automatic fallback through reliable proxies (allorigins.win, cors.sh, thingproxy, codetabs)
- Increased timeout to 15s for slower government sites

### Fixed
- Export dropdowns now collapse when clicking outside
- Schema import correctly handles the Ashoka Datalake JSON format
- Fields marked as "enum" no longer default to `aiInfer: false`

### Changed
- Feedback panel only shows for fields scoring below 7 (cleaner UI)


## [2.0.0] - 2026-04-09

### Added
- OpenMetadata Integration — push datasets directly to OpenMetadata catalog
- World Bank Schema Presets: Microdata (DDI 2.5), Document, Timeseries, Table, Geospatial (ISO 19115)
- DuckDuckGo Web Search — free web search integration
- Source URL Fetching — extract metadata from data portal pages
- Full Data Statistics — computed from entire dataset
- Custom Schema Management — save, load, manage custom schemas
- Local Model Support — Ollama, LM Studio, vLLM via custom endpoint
- Multiple Export Formats — CSV, Excel, JSON, Full Dataset
- Dark Mode — auto-switching based on system preferences

### Changed
- Complete UI redesign with card-based layout
- Improved prompt engineering for better metadata quality


## [1.0.0] - 2026-04

### Added
- Initial release
- LLM Integration — Anthropic, OpenAI, Google, Mistral, Perplexity
- CSV/Excel/JSON upload
- Per-field inference
- Metadata export — CSV, Excel, JSON formats


---

## Version Comparison

| Version | Highlights |
|---------|-----------|
| **2.1.0** (current) | Quality scoring, Ashoka preset, Browse catalog, Groq, UI redesign, theme toggle |
| 2.0.0 | OpenMetadata push, Web search, World Bank presets, Local models |
| 1.0.0 | Initial release |
