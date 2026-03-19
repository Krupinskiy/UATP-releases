# UATP User Guide

## Table of Contents

- [First Launch](#first-launch)
- [Getting a DATABASE_URL from Supabase](#getting-a-database_url-from-supabase)
- [Running a Test from the Library](#running-a-test-from-the-library)
- [Creating a Custom Template in YAML](#creating-a-custom-template-in-yaml)
- [Environments](#environments)
- [Schedules](#schedules)
- [Load Testing](#load-testing)
- [FAQ](#faq)

---

## First Launch

1. **Download and install** UATP from the [Releases](https://github.com/Krupinskiy/UATP-releases/releases) page.
2. **Run the installer** (.exe on Windows, .dmg on macOS, .AppImage on Linux) and follow the on-screen prompts.
3. **Open UATP**. On the first launch you will see the Settings page.
4. **Configure the database connection:**
   - Navigate to **Settings** (gear icon in the sidebar).
   - Enter your **API Server URL** (the backend address).
   - The backend requires a `DATABASE_URL` environment variable pointing to a PostgreSQL 16 database. See below for how to get one from Supabase.
5. **Install a browser** — Go to Settings → Browser Management and install Chromium (required for web tests). Firefox and WebKit are optional.
6. You're ready! Head to the **Library** to browse 500+ templates and run your first test.

---

## Getting a DATABASE_URL from Supabase

[Supabase](https://supabase.com) provides a free hosted PostgreSQL database.

1. Go to [supabase.com](https://supabase.com) and sign up or log in.
2. Click **New Project**.
3. Enter a project name, set a database password, and choose a region close to you. Click **Create new project**.
4. Wait for the project to finish provisioning (about 1–2 minutes).
5. Once ready, go to **Project Settings** → **Database**.
6. Find the **Connection string** section and select **URI**.
7. Copy the connection string. It will look like:
   ```
   postgresql://postgres.[ref]:[YOUR-PASSWORD]@aws-0-[region].pooler.supabase.com:6543/postgres
   ```
8. Replace `[YOUR-PASSWORD]` with the database password you set in step 3.
9. Use this connection string as your `DATABASE_URL` environment variable when starting the UATP backend.

> **Tip:** You can also use any other PostgreSQL 16 provider or a local PostgreSQL instance.

---

## Running a Test from the Library

1. Open the **Library** page from the sidebar.
2. Browse or search for a template. Use the filters to narrow by type (Web, API, Load) or category.
3. Click on a template card to view its details.
4. Click **Run** to open the Run Configuration page.
5. Fill in any required variables (e.g., `baseUrl`, `username`, `password`). If you have an Environment configured, select it to auto-fill variables.
6. Click **Start Run**.
7. The **Runner** page opens automatically, showing live execution progress — status, elapsed time, and step-by-step messages.
8. When the run completes, results appear with pass/fail status, assertions, screenshots, and any artifacts.
9. View past runs anytime from the **Reports** page.

---

## Creating a Custom Template in YAML

You can create your own test templates using the built-in Template Editor.

1. Open the **Library** page and click **Create Template**.
2. Choose a basic template type (Web, API, or Load) as a starting point.
3. Switch to the **YAML** editing tab for full control.

### API Template Example

```yaml
id: my-api-test
name: Check User API
type: api
tags: [api, users]
steps:
  - action: send-request
    params:
      method: GET
      url: "{{baseUrl}}/api/users/1"
      headers:
        Authorization: "Bearer {{token}}"
    save_as:
      userName: body.name
assertions:
  - type: status
    expected: 200
  - type: json-path
    path: body.name
    expected: "John"
```

### Web Template Example

```yaml
id: my-web-test
name: Login Flow
type: web
tags: [web, login]
steps:
  - action: open-page
    params:
      url: "{{baseUrl}}/login"
  - action: fill
    params:
      selector: "#email"
      value: "{{email}}"
  - action: fill
    params:
      selector: "#password"
      value: "{{password}}"
  - action: click
    params:
      selector: "button[type=submit]"
  - action: screenshot
    params:
      name: "after-login"
assertions:
  - type: url-matches
    expected: "/dashboard"
  - type: text-visible
    expected: "Welcome"
```

### Key Concepts

- **`{{variable}}`** — Placeholders resolved at runtime from run config, environments, or response chaining.
- **`save_as`** — Extract values from responses using JSONPath and reuse them in later steps.
- **`assertions`** — Validate results after steps execute (status codes, JSON paths, element visibility, etc.).

4. Click **Save** when done. Your template appears in the Library under Custom Templates.

---

## Environments

Environments let you store different configurations for each deployment stage (dev, staging, production).

1. Open the **Environments** page from the sidebar.
2. Click **Create Environment**.
3. Enter a name (e.g., "Production") and add key-value pairs:
   - `baseUrl` → `https://api.example.com`
   - `token` → `your-api-token`
   - Any custom variables your templates need.
4. Click **Save**.

**Using an environment in a test:**

- When configuring a run, select the environment from the dropdown. All variables defined in the environment are automatically injected into `{{variable}}` placeholders.
- You can still override individual variables in the run configuration.

> **Tip:** Use separate environments for dev, staging, and production to avoid hardcoding URLs and credentials in templates.

---

## Schedules

Schedules allow you to run tests automatically at defined intervals.

1. Open the **Schedules** page from the sidebar.
2. Click **Create Schedule**.
3. Select a **template** or **suite** to schedule.
4. Choose a frequency:
   - **Hourly** — run every hour
   - **Daily** — run once per day at a specified time
   - **Weekly** — run once per week on a chosen day
   - **Custom** — enter a cron expression (e.g., `0 9 * * 1-5` for weekdays at 9 AM)
5. Optionally select an environment to use for the scheduled run.
6. Click **Save**.

Each schedule can be enabled or disabled independently. Scheduled run results appear in Reports alongside manual runs.

---

## Load Testing

UATP supports load testing with configurable virtual users, duration, and real-time metrics.

### Running a Load Test

1. Open the **Library** and select a Load template, or navigate directly to **Load Testing** in the sidebar.
2. Click **Configure** on a load template to open the Load Config page.
3. Set the parameters:
   - **Mode** — Choose from: Smoke (3 VUs / 30s), Load (50 VUs / 2m), Stress (200 VUs / 3m), Spike (150 VUs / 1m), Soak (20 VUs / 1h), Breakpoint (300 VUs / 4m), or Custom.
   - **Virtual Users (VUs)** — Number of concurrent simulated users.
   - **Duration** — How long the test runs (in seconds).
   - **Ramp-up** — Seconds to gradually increase users from 0 to VUs.
   - **Ramp-down** — Seconds to gradually decrease users at the end.
   - **Think Time** — Pause between actions (simulates real user behavior).
4. Click **Start Load Test**.
5. The **Load Runner** page shows real-time metrics:
   - Requests: total, failed, requests per second (avg and peak)
   - Latency percentiles: p50, p95, p99
   - Error rate
   - Throughput (bytes sent/received)
   - Status code distribution
   - Time-series charts

### Viewing Results

- After the test completes, open the **Load Report** for a detailed breakdown with charts.
- Export results to **CSV** for further analysis.
- Use **Load Compare** to compare two load test runs side by side.
- All past load runs are available in the **Load Runs** history page.

---

## FAQ

### 1. What databases does UATP support?

UATP requires **PostgreSQL 16** for its backend. For data-driven testing, you can connect to PostgreSQL, MySQL, or SQLite as data sources.

### 2. Do I need Redis?

Yes. UATP uses **Redis 7** with BullMQ for asynchronous job processing (running tests in the background). You need a running Redis instance.

### 3. Can I import tests from Postman?

Yes. Go to the Library and click **Import → Postman Collection**. Upload your Postman JSON file and UATP will convert each request into an API template.

### 4. How do I update UATP?

Download the latest release from the [Releases](https://github.com/Krupinskiy/UATP-releases/releases) page and run the installer. Your data and settings are preserved.

### 5. Can I run tests without a browser installed?

API and load tests do not require a browser. For web tests, you need at least Chromium installed — go to Settings → Browser Management to install it.

### 6. How does visual regression work?

When you add a `screenshot` step to a web template, you can save the resulting image as a baseline. On subsequent runs, UATP compares each screenshot against its baseline pixel-by-pixel and reports the diff percentage. You can manage baselines from the Reports page.

### 7. Is my data stored locally?

UATP is a local-first application. Your test data, templates, and artifacts are stored in your PostgreSQL database and the local `artifacts/` directory. Nothing is sent to external servers unless you configure it (e.g., webhook notifications).
