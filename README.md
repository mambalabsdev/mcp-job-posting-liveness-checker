# Job Posting Liveness Checker MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-job-posting-liveness-checker)](https://www.npmjs.com/package/@mambalabsdev/mcp-job-posting-liveness-checker) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-job-posting-liveness-checker)](https://github.com/mambalabsdev/mcp-job-posting-liveness-checker/blob/main/LICENSE)

An MCP server for the Mamba Labs Job Posting Liveness Checker actor on Apify. Is the job still open, and how old is it.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Give job posting URLs from Greenhouse, Lever, Ashby, Workday, or SmartRecruiters. The actor asks each ATS's own public job API whether the posting is still served and returns live or closed, the posted date, the age in days, and the last time a run on your account saw it live. A posting counts as closed only after the company's board itself answers, so a wrong board name is never reported as closed.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-job-posting-liveness-checker": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-job-posting-liveness-checker"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `check_job_posting_liveness` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Are these 20 job postings still open, and how old is each one?"
- "Which of my target accounts' Greenhouse postings closed since last week?"

## Tool

`check_job_posting_liveness`. One tool. Example arguments:

```json
{
  "job_urls": [
    "https://job-boards.greenhouse.io/stripe/jobs/8172510"
  ]
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `job_urls` | array | no | Posting URLs from Greenhouse (boards.greenhouse.io, job-boards.greenhouse.io, or a company site with ?gh_jid=), Lever (jobs.lever.co), Ashby (jobs.ashbyhq.com), Workday (*.myworkdayjobs.com), or SmartRecruiters (jobs.smartrecruiters.com). Up to 5,000 per run. From Clay, put the column inside a one item list. |
| `max_charge_usd` | string | no | Optional. The run stops before a charge that would pass this amount. Rows already checked are returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `posting-check`, one posting checked, live or closed | $0.003 | $0.00285 | $0.0027 | $0.00255 |
| `apify-actor-start`, per run start | $0.002 | $0.002 | $0.002 | $0.002 |

Unsupported URLs, a board that does not exist, a refused request, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/job-posting-liveness-checker](https://apify.com/mambalabs/job-posting-liveness-checker)

## License

MIT. See [LICENSE](LICENSE).
