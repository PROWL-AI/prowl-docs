---
name: gemini_reviews_report
provider: Google Gemini
provider_slug: gemini
category: ai
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `gemini_reviews_report`

Analyze customer reviews using Gemini AI to extract Voice of Customer insights.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Google Gemini |
| Category | `ai` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ai`, `google-gemini`, `reviews` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "gemini_reviews_report",
  "params": {
    "reviews_data_text": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `reviews_data_text` | string | yes |  | Raw review data as text/JSON string |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "reviews_data_text": {
      "type": "string",
      "description": "Raw review data as text/JSON string"
    }
  },
  "required": [
    "reviews_data_text"
  ]
}
```

## Example request

```json
{
  "reviews_data_text": "example"
}
```

## Output

Voice of Customer analysis from reviews

Key fields: `reviews_summary`, `top_5_problems`, `top_5_pros`, `top_5_cons`, `top_5_features`, `average_rating`, `sentiment_analysis`, `reviews_sentiment_score`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing GEMINI_API_KEY | Cannot use AI analysis tools — report available data without AI synthesis |
| 429 | Rate limit / quota exceeded | Wait 60s and retry once; Gemini has generous free tier |
| 500 | Gemini internal error | Retry up to 3 times (built-in); if all fail, returns None |

## When to use

- Collect reviews via firecrawl_search from G2, Capterra, Trustpilot, app stores first

**Chain inputs:** `{'param': '<from_template>', 'from_tool': 'firecrawl_search', 'extract': '?'}`

**Chain groups:** `gemini`

## Alternatives

- `scrape_review_platforms`
- `airbnb_property_reviews`
- `apple_product_reviews`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://ai.google.dev/gemini-api/docs
