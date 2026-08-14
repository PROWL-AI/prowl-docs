---
name: extract_domain_from_url
provider: Project Utility
provider_slug: project_utility
category: utility
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `extract_domain_from_url`

Extract a clean domain name from a URL.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Project Utility |
| Category | `utility` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `domain`, `project-utility`, `utility` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "extract_domain_from_url",
  "params": {
    "url": "https://www.example.com/landing?utm=1"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `url` | string | yes |  | URL to extract domain from |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "URL to extract domain from"
    }
  },
  "required": [
    "url"
  ]
}
```

## Example request

```json
{
  "url": "https://www.example.com/landing?utm=1"
}
```

## Output

Extracted domain and original URL

Key fields: `domain`, `original_url`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| validation | Missing or invalid required argument | Fix the input and retry; check the tool's input_schema |
| io | Local filesystem or cache operation failed | Retry once; if it persists, skip the utility step and continue the hunt |

## When to use

- Helper to clean URLs to domain format (e.g. 'https://www.example.com/page' -> 'example.com')
- Use before passing URLs to domain-based tools like spyfu_get_domain_stats

## Alternatives

- `find_subdomains`
- `google_about_this_domain`
- `dataforseo_ai_llm_mentions_top_domains`

_Full paths: [catalog index](../README.md)._
