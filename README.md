# UATP — Universal Automation Testing Platform

![Version](https://img.shields.io/badge/version-v1.0.0-blue)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-brightgreen)
![License](https://img.shields.io/badge/license-free%20to%20use-orange)

**UATP** is a local-first desktop application for QA engineers to run automated web, API, and load tests — all configured in YAML, no code required. It ships with 500+ ready-made templates, a built-in template editor, and a real-time dashboard so you can start testing in minutes.

---

## Key Features

- 🧪 **500+ Test Templates** — Ready-to-use YAML templates for API, Web, and Load testing across 30+ categories (CRUD, Auth, Forms, E-Commerce, Security, Performance, and more)
- 🌐 **Web Testing (Playwright)** — 25+ browser actions: click, fill, hover, drag-drop, file upload, keyboard input, device emulation, screenshots, and accessibility audits
- 🔗 **API Testing** — Full HTTP method support (GET/POST/PUT/PATCH/DELETE/HEAD/OPTIONS) plus WebSocket connections
- ⚡ **Load Testing** — 6 modes (Smoke, Load, Stress, Spike, Soak, Breakpoint) with real-time metrics: RPS, p50/p95/p99 latency, error rate, and throughput
- 📊 **Dashboard & Trends** — Pass rate trends (7/14/30 days), duration charts, flaky test detection, top templates, and upcoming scheduled runs
- 📝 **Visual Template Editor** — Create and edit templates in Visual, YAML, or BDD mode with live validation
- 🔄 **Response Chaining** — Extract values from responses via JSONPath (`save_as`) and reuse them across steps with `{{variable}}` placeholders
- 📂 **Data-Driven Testing** — 10 data sources: CSV, JSON, YAML, XLSX, Table Editor, Environment Variables, Database queries, API responses, and Faker-generated data
- 🖼️ **Visual Regression** — Pixel-level screenshot comparison with baseline management and diff reporting
- 🗂️ **Environments** — Manage separate configurations (dev/staging/prod) for API URLs, headers, and credentials
- 📅 **Schedules** — Cron-based automated test execution (hourly, daily, weekly, or custom)
- 🧩 **Test Suites** — Group templates into suites, run them together, and re-run only failed tests
- 🔍 **Command Palette** — Quick access (Ctrl+K / Cmd+K) to search pages, templates, and recent runs
- 📥 **Postman Import** — Convert Postman collections to UATP templates with one click
- 🌙 **Dark Theme** — Full dark/light mode with system theme detection
- 📤 **Export** — Download templates as YAML, load test results as CSV, and test reports
- ♿ **Accessibility Audits** — Automated WCAG compliance checks with violation counting
- 🌍 **Internationalization** — English and Russian UI
- 🖥️ **Cross-Platform** — Native desktop app for Windows, macOS, and Linux

---

## Download

Go to the [**Releases**](https://github.com/Krupinskiy/UATP-releases/releases) page and download the latest installer for your OS.

| OS | File |
|----|------|
| Windows | `UATP-Setup-1.0.0.exe` |
| macOS | `UATP-1.0.0.dmg` |
| Linux | `UATP-1.0.0.AppImage` |

---

## Quick Start

1. **Download** the installer from [Releases](https://github.com/Krupinskiy/UATP-releases/releases)
2. **Install** — run the installer and follow the prompts
3. **Launch** — open UATP, configure your database connection in Settings, and run your first test from the Library

---

## Screenshots

### Dashboard
> Screenshot coming soon

### Template Library
> Screenshot coming soon

### Test Runner
> Screenshot coming soon

### Load Testing
> Screenshot coming soon

### Visual Regression
> Screenshot coming soon

---

## Requirements

| OS | Minimum Version |
|----|-----------------|
| Windows | 10 or later |
| macOS | 12 (Monterey) or later |
| Linux | Ubuntu 20.04+ / Fedora 36+ / Debian 11+ |

**Additional:**
- A PostgreSQL 16 database (local or hosted, e.g. [Supabase](https://supabase.com))

---

## Documentation

- [User Guide](docs/USER_GUIDE.md) — setup, first test, environments, schedules, load testing, and FAQ

---

## Bug Reports & Feature Requests

Found a bug or have an idea? Open an issue:

- 🐛 [Bug Report](https://github.com/Krupinskiy/UATP-releases/issues/new?template=bug_report.yml)
- 💡 [Feature Request](https://github.com/Krupinskiy/UATP-releases/issues/new?template=feature_request.yml)

---

## License

UATP is free to use. The source code is not publicly available.
