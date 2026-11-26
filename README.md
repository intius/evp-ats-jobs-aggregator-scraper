# tech jobs Scraper & Unofficial API (Python, Node.js, MCP)

[Run Multi-ATS Tech Jobs Scraper - Greenhouse, Ashby & Lever on Apify](https://apify.com/evpp/ats-jobs-aggregator) to export tech jobs data as clean JSON, CSV, Excel, or an API feed. This repository is a developer quick-start kit with working Python and Node.js clients, an MCP configuration, a real sample dataset, and an n8n automation template.

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-orange)](https://apify.com/evpp/ats-jobs-aggregator)

[Open the documentation and crawlable sample explorer](https://intius.github.io/evp-labs-data-extractors/actors/ats-jobs-aggregator/) for quick inputs, integration links, real sample rows, and ready-made task examples.

## Why use this tech jobs scraper?

- Export tech jobs data without building or maintaining a custom scraper
- Get flat, schema documented JSON ready for analytics, lead generation, market research, and AI agents
- Run manually, on a schedule, through the Apify API, or through MCP compatible AI tools
- Use the included 25+ row sample dataset to prototype before running the live Actor

Built for B2B lead generation teams, market researchers, growth operators, AI workflow builders.

## Quick start on Apify

Open [https://apify.com/evpp/ats-jobs-aggregator](https://apify.com/evpp/ats-jobs-aggregator) and use this input:

```json
{
  "query": "software engineer",
  "remoteOnly": true,
  "postedWithinDays": 30,
  "includeDescriptions": false,
  "maxItems": 12
}
```

## Python

```bash
pip install -r requirements.txt
export APIFY_TOKEN=your_apify_token
python python/run.py
```

On Windows PowerShell, use `$env:APIFY_TOKEN="your_apify_token"` instead of `export`.

## Node.js

```bash
npm install
export APIFY_TOKEN=your_apify_token
node node/run.mjs
```

## MCP and AI agents

Add the hosted Apify MCP server from `mcp-config.json` to your MCP client:

```json
{
  "mcpServers": {
    "apify": {
      "type": "http",
      "url": "https://mcp.apify.com/?tools=evpp/ats-jobs-aggregator"
    }
  }
}
```

Then ask your agent to run `evpp/ats-jobs-aggregator`, inspect the output schema, or export the latest dataset. The direct MCP URL is `https://mcp.apify.com/?tools=evpp/ats-jobs-aggregator`.

For multi-source public data agents, use the [EVP Public Data MCP server](https://github.com/intius/evp-public-data-mcp). It is published in the Official MCP Registry as `io.github.intius/evp-public-data-mcp` and is also available as a one-click Claude Desktop MCPB release.

## n8n automation

Import `n8n-workflow.json` into n8n, select your Apify credential, replace the webhook placeholder, and activate the schedule. The workflow runs the Actor every morning and posts fresh dataset items to your webhook.

## Output schema

| Field | Type | Description |
|---|---|---|
| `jobId` | string | Stable job ID prefixed by ATS platform |
| `ats` | string | Applicant tracking system |
| `company` | string | Company name |
| `companySlug` | string | ATS board slug |
| `title` | string | Job title |
| `location` | string | Normalized location text |
| `remote` | boolean | True when the job is remote |
| `department` | string | Department or team |
| `employmentType` | string | Employment type when available |
| `postedAt` | string | Posting or first-published timestamp |
| `updatedAt` | string | Last update timestamp when available |
| `salaryMin` | number | Normalized minimum annual salary in original currency when detectable |
| `salaryMax` | number | Normalized maximum annual salary in original currency when detectable |
| `salaryCurrency` | string | ISO-like salary currency code when detectable |
| `jobUrl` | string | Canonical job posting URL |
| `applyUrl` | string | Application URL when distinct |
| `description` | string | Clean plain-text description excerpt |
| `sourceRegistry` | string | Registry source used for the board |

## Real sample output

The first sanitized row from the included sample dataset:

```json
{
  "jobId": "lever:755229fc-faa7-4af5-983e-c3dbb3c1e693",
  "ats": "lever",
  "company": "Veeva Systems",
  "companySlug": "veeva",
  "title": "Senior Software Engineer - Fullstack with Rust",
  "location": "Wisconsin - Madison",
  "department": "Engineering",
  "employmentType": "Full-Time",
  "postedAt": "2026-11-04T23:09:19.541Z",
  "jobUrl": "https://jobs.lever.co/veeva/755229fc-faa7-4af5-983e-c3dbb3c1e693",
  "applyUrl": "https://jobs.lever.co/veeva/755229fc-faa7-4af5-983e-c3dbb3c1e693/apply",
  "sourceRegistry": "builtin-420",
  "remote": true
}
```

## Files in this kit

| File | Purpose |
|---|---|
| `python/run.py` | Working Python Apify API example |
| `node/run.mjs` | Working Node.js Apify API example |
| `mcp-config.json` | MCP server configuration for AI agents |
| `sample-output.json` | First five sanitized sample rows |
| `dataset-snapshot.csv` | 25+ row evaluation snapshot |
| `DATASET_CARD.md` | Dataset documentation and provenance |
| `n8n-workflow.json` | Scheduled n8n automation template |

## Fresh data

This repository contains a static evaluation sample. For current data, run the live Actor: https://apify.com/evpp/ats-jobs-aggregator

## Responsible use

The Actor reads public data from `greenhouse.io`. Review the source site's terms and applicable privacy rules before production use.
