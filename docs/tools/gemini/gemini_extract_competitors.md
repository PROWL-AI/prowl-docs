---
name: gemini_extract_competitors
provider: Google Gemini
provider_slug: gemini
category: ai
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `gemini_extract_competitors`

Analyze search results using Gemini AI to identify distinct competitor products.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Google Gemini |
| Category | `ai` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ai`, `competitors`, `google-gemini` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "gemini_extract_competitors",
  "params": {
    "search_results_text": "example",
    "target_product_name": "example",
    "target_website_url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `target_product_name` | string | yes |  | Name of the target product to exclude |
| `target_website_url` | string | yes |  | URL of the target product website |
| `search_results_text` | string | yes |  | Raw search results as text/JSON string (combined output from search tools) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "target_product_name": {
      "type": "string",
      "description": "Name of the target product to exclude"
    },
    "target_website_url": {
      "type": "string",
      "description": "URL of the target product website"
    },
    "search_results_text": {
      "type": "string",
      "description": "Raw search results as text/JSON string (combined output from search tools)"
    }
  },
  "required": [
    "target_product_name",
    "target_website_url",
    "search_results_text"
  ]
}
```

## Example request

```json
{
  "search_results_text": "example",
  "target_product_name": "example",
  "target_website_url": "https://example.com"
}
```

## Output

Identified competitors with structured data

Key fields: `[].website_url`, `[].product_name`, `[].summary`, `[].keywords`, `[].features`, `[].target_audience`, `[].positioning_in_the_market`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing GEMINI_API_KEY | Cannot use AI analysis tools — report available data without AI synthesis |
| 429 | Rate limit / quota exceeded | Wait 60s and retry once; Gemini has generous free tier |
| 500 | Gemini internal error | Retry up to 3 times (built-in); if all fail, returns None |

## When to use

- Use after collecting search results from exa/perplexity to identify distinct competitors

**Chain inputs:** `{'param': 'search_results_text', 'from_tool': 'perplexity_search_by_query', 'extract': '_raw_json_string'}`

**Chain groups:** `gemini`

## Alternatives

- `dataforseo_labs_amazon_product_competitors`
- `dataforseo_labs_apple_app_competitors`
- `dataforseo_labs_competitors_domain`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://ai.google.dev/gemini-api/docs
