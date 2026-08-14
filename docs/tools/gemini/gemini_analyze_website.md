---
name: gemini_analyze_website
provider: Google Gemini
provider_slug: gemini
category: ai
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `gemini_analyze_website`

Analyze scraped website content using Google Gemini AI to extract structured product intelligence.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Google Gemini |
| Category | `ai` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ai`, `google-gemini` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "gemini_analyze_website",
  "params": {
    "website_data_text": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `website_data_text` | string | yes |  | Raw website data as text/JSON string (output from firecrawl_scrape_website or firecrawl_search) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "website_data_text": {
      "type": "string",
      "description": "Raw website data as text/JSON string (output from firecrawl_scrape_website or firecrawl_search)"
    }
  },
  "required": [
    "website_data_text"
  ]
}
```

## Example request

```json
{
  "website_data_text": "example"
}
```

## Output

Structured product intelligence from website content

Key fields: `product_name`, `product_description`, `features`, `benefits`, `niche`, `target_audience`, `audience_pains`, `tone_of_voice`, `conversion_flow`, `ctas`, `keywords`, `search_terms`, `pricing_structure`, `social_proof`, `app_store_url`, `google_play_url`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing GEMINI_API_KEY | Cannot use AI analysis tools — report available data without AI synthesis |
| 429 | Rate limit / quota exceeded | Wait 60s and retry once; Gemini has generous free tier |
| 500 | Gemini internal error | Retry up to 3 times (built-in); if all fail, returns None |

## When to use

- Use after firecrawl_scrape_website — pass the scraped content as input
- Returns None on failure after internal retries

**Chain inputs:** `{'param': 'website_data_text', 'from_tool': 'firecrawl_scrape_website', 'extract': '_raw_json_string'}`

**Chain groups:** `gemini`

## Alternatives

_None listed._

## Provider docs

https://ai.google.dev/gemini-api/docs
