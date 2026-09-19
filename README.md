# Enterprise Repository Transfer Automation System

<div align="center">

[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/MishraShardendu22/repo-transfer-engine)
[![CI Status](https://github.com/MishraShardendu22/repo-transfer-engine/actions/workflows/ci.yml/badge.svg)](https://github.com/MishraShardendu22/repo-transfer-engine/actions/workflows/ci.yml)
[![License: Proprietary](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE)
[![Architecture: Microservices](https://img.shields.io/badge/Architecture-Microservices-blue.svg)](#conceptual-architecture)
[![Frontend: Go Templ](https://img.shields.io/badge/Frontend-Go%20Templ-orange.svg)](https://templ.guide)
[![Runtime: Go 1.25](https://img.shields.io/badge/Runtime-Go%201.25%2B-00ADD8?logo=go)](https://go.dev)

<p align="center">
  <b>High-throughput, fault-tolerant microservice platform engineered to orchestrate large-scale bulk repository migrations across GitHub user accounts and organizations with adaptive rate-limit auto-tuning.</b>
</p>

</div>

---

> [!IMPORTANT]
> **PROPRIETARY & CLOSED-SOURCE SPECIFICATION**
> This repository serves as the official public product showcase, architectural specification, and capability documentation. The underlying source code, microservice binaries, concurrency engines, and rate-limit algorithms are strictly **closed source and proprietary**, owned by **Shardendu Mishra**.
> Unauthorized duplication, reproduction, reverse engineering, or commercial imitation is prohibited under international intellectual property law.

---

## Live Resources

- **Video Demonstration**: [YouTube Walkthrough](https://youtu.be/0Rhfgxg6YyE?si=IV2DMjMSYAom9KqA)
- **Developer Portfolio**: [mishrashardendu22.is-a.dev](https://mishrashardendu22.is-a.dev)
- **Security Policy**: [SECURITY.md](SECURITY.md)
- **Commercial Licensing Guide**: [CONTRIBUTING.md](CONTRIBUTING.md)

---

## Executive Overview

Migrating dozens or hundreds of repositories between personal GitHub accounts and enterprise organizations typically requires tedious, manual UI confirmation or fragile, unthrottled shell scripts that quickly trigger GitHub's secondary rate limits (`403 Forbidden` / `429 Too Many Requests`).

The **Enterprise Repository Transfer Automation System** solves this systemic operational risk by decoupling migration execution into independent, fault-tolerant microservices:
1. **Interactive Web Dashboard**: Ultra-low latency, server-rendered interface built with Go and `templ` (zero Node.js runtime overhead).
2. **Transfer Orchestrator REST API**: Manages OAuth 2.0 sessions, repository discovery, and queue dispatch.
3. **Adaptive Execution Worker**: Employs exponential backoff with jitter, quota calculation, and secondary rate-limit auto-throttling.

---

## Core Capabilities

| Capability | Specification | Enterprise Benefit |
| :--- | :--- | :--- |
| **Concurrent Batch Migration** | Channel-driven worker pool with configurable parallelism | Migrates 100+ repositories in minutes with zero manual UI clicks |
| **Adaptive Rate-Limit Auto-Tuning** | Exponential backoff (2s base, factor 2, max 10s) with 10% random jitter | Prevents account abuse flags and GitHub API suspension |
| **Zero-Token OAuth 2.0 Security** | Ephemeral, scoped OAuth token exchange with HttpOnly cookies | Eliminates persistent Personal Access Token (PAT) leaks |
| **Compiled Type-Safe Frontend** | Server-rendered Go `templ` components with dark mode telemetry | Instant sub-millisecond page loads with zero browser bundle bloat |
| **Dual Execution Modalities** | Persistent containerized web service or headless CI/CD CLI | Seamlessly integrates into automated DevOps & M&A migration pipelines |
| **Cryptographic Audit Trail** | Granular per-repository status codes, target acceptance logs, and timestamps | Complete compliance transparency for enterprise audits |

---

## Conceptual Architecture

```text
┌─────────────────────────────────────────────────────────────┐
│                 Go + Templ Web Dashboard                   │
│         (Compiled Type-Safe SSR Frontend /web)              │
└───────────────┬─────────────────────────────┬───────────────┘
                │ Form Actions / Fetch        │ Live Status Polling
                ▼                             ▼
┌─────────────────────────────────────────────────────────────┐
│                  Go Backend REST Server                     │
│    (Fiber / Standard HTTP · Auth, Repos, Job Dispatch)      │
└───────────────┬─────────────────────────────────────────────┘
                │ In-Memory / Channel Dispatch
                ▼
┌─────────────────────────────────────────────────────────────┐
│                 Transfer Worker Engine                      │
│   (Exponential Backoff · Rate Limiter · GitHub REST API)    │
└───────────────┬─────────────────────────────────────────────┘
                │ HTTPS (Personal Access Token / OAuth)
                ▼
┌─────────────────────────────────────────────────────────────┐
│                    GitHub REST API v3                       │
│        (POST /repos/{owner}/{repo}/transfer)                │
└─────────────────────────────────────────────────────────────┘
```

---

## Benchmark Performance Targets

- **Throughput**: ~120 repository transfers per hour (fully rate-limit compliant).
- **Frontend Latency**: < 5ms TTFB (Time-to-First-Byte) via compiled Go Templ.
- **Memory Footprint**: < 25MB total RAM for backend and worker services.
- **Failure Recovery**: 100% automatic recovery on transient `502` / `503` / `429` upstream errors.

---

## Commercial Licensing & Enterprise Inquiries

Access to the proprietary implementation codebase, pre-built multi-arch Docker images (`linux/amd64`, `linux/arm64`), and automated deployment blueprints is provided exclusively under commercial agreement.

- **Author & Copyright Holder**: Shardendu Mishra
- **Direct Email**: mishrashardendu22@gmail.com
- **Website**: [mishrashardendu22.is-a.dev](https://mishrashardendu22.is-a.dev)
- **GitHub Profile**: [@MishraShardendu22](https://github.com/MishraShardendu22)

---

## License

Copyright &copy; 2026 Shardendu Mishra. All Rights Reserved.
This project is proprietary and closed-source software. See [LICENSE](LICENSE) for full terms.
