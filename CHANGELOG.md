# Changelog

All notable changes to UATP will be documented in this file.

## [1.0.0] - 2026-03-20

### Initial Release

#### Template Library
- **500+ ready-to-use YAML templates** across three categories:
  - **API Testing (203 templates):** CRUD & REST, Authentication (JWT, OAuth2, API keys), Pagination (offset/cursor), Error Handling (4xx/5xx codes), Caching (ETags, Cache-Control), Content Negotiation, WebSocket (connect/disconnect/echo/binary/auth), Webhooks (delivery, retry, signatures), GraphQL (queries, mutations, fragments, introspection), File Operations (upload/download/validation), Security (SQL injection, XSS, XXE, path traversal, CORS, HSTS, CSP), Performance (response time assertions), Monitoring (health checks, readiness/liveness probes), Idempotency (keys, deduplication), Batch Operations (bulk CRUD), Filters & Search (nested fields, date ranges), Versioning (header/query-param), E2E Flows (register-login-profile, order lifecycle)
  - **Web Testing (251 templates):** Accessibility (WCAG audits, heading structure, ARIA, keyboard nav, color contrast), Forms & Input (validation, masking, multi-step wizards, autocomplete, date pickers, file uploads), UI Components (modals, dropdowns, tabs, tables with sorting/pagination, carousels, tooltips, accordions, infinite scroll, lazy loading), E-Commerce (cart, checkout, wishlist, product compare, promo codes, order tracking), Security (XSS prevention, CSRF tokens, session timeout, clickjacking), Performance & SEO (Web Vitals — LCP, FID, CLS, page load time, meta tags, image optimization), Responsive & Localization (mobile/tablet viewports, RTL layout, language switching, GDPR consent), Social Features (login integration, profiles, follow/like, share, comments, activity feeds), Content (video players, image galleries, PDFs, markdown, iframes), Dashboard (KPI cards, charts, real-time updates, data tables, export), Navigation (menus, breadcrumbs, sidebar collapse, sticky headers)
  - **Load Testing (45 templates):** Smoke (health, auth, general), Load (CRUD, auth refresh, pagination, search, file ops, WebSocket), Stress (general, auth, database, file storage), Spike (search, payment, file upload, homepage), Soak (auth sessions, database reads), Breakpoint (CRUD, create operations), Web Load (login, registration, forms, dashboard, checkout), Mixed (WebSocket, user journeys)

#### Web Testing Engine (Playwright)
- 25+ browser actions: open-page, fill, click, hover, select, wait, screenshot, scroll, keyboard, drag-drop, file-upload, set-viewport, clear-input, emulate-device, collect-web-vitals, block-resources, accessibility-audit
- Multi-browser support: Chromium, Firefox, WebKit with in-app installation and management
- Device emulation for mobile and tablet testing
- Network resource blocking for performance testing
- Core Web Vitals collection (LCP, FID, CLS)
- Accessibility audits with WCAG violation counting

#### API Testing Engine
- Full HTTP method support: GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS
- Custom headers, request body (JSON, form data), and query parameters
- WebSocket connections with message send/receive
- Response chaining via JSONPath (`save_as` / `{{variable}}` placeholders)
- Response time assertions and status code validation

#### Load Testing
- 6 test modes: Smoke, Load, Stress, Spike, Soak, Breakpoint
- Configurable virtual users (VUs), duration, ramp-up, ramp-down, think time
- Custom multi-phase ramp stages
- Real-time metrics: total/failed requests, RPS (avg/peak), p50/p95/p99 latency, error rate, throughput
- Status code distribution and time-series response snapshots
- Load test comparison — side-by-side run analysis
- CSV export of load test results

#### Data-Driven Testing
- 10 data source types: UI Form, CSV, JSON, YAML, XLSX (with sheet selection), Table Editor, Environment Variables, Database queries (PostgreSQL/MySQL/SQLite), API responses (JSONPath extraction), Faker-generated data (names, emails, addresses, etc.)
- Automatic parameterization — run template once per data row

#### Visual Regression Testing
- Baseline screenshot saving from any test step
- Pixel-level comparison using pixelmatch
- Diff image generation highlighting changed pixels
- Diff percentage tracking
- Baseline management — view and delete per template

#### Dashboard
- Recent runs overview (last 50 executions)
- Pass rate trend charts (7/14/30-day)
- Duration trend — average execution time over time
- Flaky test detection — templates with inconsistent results
- Top templates — most frequently run tests
- Upcoming scheduled runs (next 3)
- Load test status summary

#### Template Editor
- Three editing modes: Visual, YAML, BDD
- Live Zod validation
- Step and assertion builder
- Custom template creation and management

#### Environments
- Create and manage named environment configurations
- Store API URLs, headers, credentials per environment (dev/staging/prod)
- Environment variable injection into test templates

#### Schedules
- Cron-based automated test execution
- Schedule templates or entire suites
- Presets: hourly, daily, weekly, or custom cron expressions
- Enable/disable individual schedules

#### Test Suites
- Group multiple templates into suites
- Run all tests in a suite together
- View per-test status breakdown
- Re-run only failed tests

#### Reports & Artifacts
- Full test run history with grid/list views
- Filter, sort, and search past runs
- Re-run tests from history
- Add notes to test runs
- Artifacts: screenshots, video recording, HAR files, trace files, diff images, JSON reports

#### Postman Import
- Convert Postman collection JSON files to UATP API templates
- Automatic endpoint and header mapping

#### Command Palette
- Quick access via Ctrl+K / Cmd+K
- Search pages, templates, and recent runs

#### Playground
- Ad-hoc Playwright/API script execution
- Built-in code examples and console output

#### Notifications
- Webhook integrations: Generic, Slack, Discord, Telegram
- Event filtering: test pass, test failure
- Configurable per-webhook event types

#### Desktop Application
- Built with Electron 28 + React 18 + shadcn/ui
- Cross-platform: Windows, macOS, Linux
- Dark/light theme with system theme detection
- Internationalization: English and Russian
- In-app browser management (install/update Chromium, Firefox, WebKit)
- File system access for uploads, downloads, and artifact management

#### Authentication & Security
- JWT-based authentication with token refresh
- User registration and login
- Per-user data isolation (templates, runs, bookmarks, schedules)
- Secure password hashing

#### Infrastructure
- NestJS backend with REST API
- BullMQ + Redis job queue for async test execution
- PostgreSQL 16 database with TypeORM migrations
- Configurable API server URL and execution timeout
