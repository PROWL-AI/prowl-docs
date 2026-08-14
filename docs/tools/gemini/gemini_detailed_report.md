---
name: gemini_detailed_report
provider: Google Gemini
provider_slug: gemini
category: ai
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `gemini_detailed_report`

Generate a comprehensive competitive analysis report from a PDF document using Gemini AI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Google Gemini |
| Category | `ai` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `ai`, `google-gemini` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "gemini_detailed_report",
  "params": {
    "domain": "example.com",
    "pdf_filename": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `domain` | string | yes |  | Target domain name for the report |
| `pdf_filename` | string | yes |  | Path to the PDF file containing collected data |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domain": {
      "type": "string",
      "description": "Target domain name for the report"
    },
    "pdf_filename": {
      "type": "string",
      "description": "Path to the PDF file containing collected data"
    }
  },
  "required": [
    "domain",
    "pdf_filename"
  ]
}
```

## Example request

```json
{
  "domain": "example.com",
  "pdf_filename": "example"
}
```

## Output

Comprehensive competitive analysis report from PDF data

Key fields: `target_product_data`, `competitors_data`, `product_summary`, `target_audience_summary`, `seo_performance_summary`, `marketing_strategy_summary`, `marketing_ideas`, `creative_ideas`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing GEMINI_API_KEY | Cannot use AI analysis tools — report available data without AI synthesis |
| 429 | Rate limit / quota exceeded | Wait 60s and retry once; Gemini has generous free tier |
| 500 | Gemini internal error | Retry up to 3 times (built-in); if all fail, returns None |
| pdf_error | Cannot read PDF file | Check file path exists; ensure PDF was saved properly |

## When to use

- This is the final synthesis step — use only after ALL data has been collected and saved to PDF
- Retries up to 3 times internally on Gemini errors

## Alternatives

_None listed._

## Provider docs

https://ai.google.dev/gemini-api/docs
