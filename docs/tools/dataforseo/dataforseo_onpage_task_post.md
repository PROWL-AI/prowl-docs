---
name: dataforseo_onpage_task_post
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_onpage_task_post`

Start an OnPage website crawl — checks 60+ on-page SEO parameters.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `dataforseo`, `onpage` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_onpage_task_post",
  "params": {
    "target": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `accept_language` | string | no |  | language header for accessing the website |
| `allow_subdomains` | boolean | no |  | include pages on subdomains |
| `allowed_subdomains` | any[] | no |  | subdomains to crawl |
| `browser_preset` | string | no |  | preset for browser screen parameters |
| `browser_screen_height` | integer | no |  | browser screen height |
| `browser_screen_scale_factor` | number | no |  | browser screen scale factor |
| `browser_screen_width` | integer | no |  | browser screen width |
| `calculate_keyword_density` | boolean | no |  | calculate keyword density for the target domain |
| `check_spell` | boolean | no |  | check spelling |
| `check_spell_exceptions` | any[] | no |  | words excluded from spell check |
| `check_spell_language` | string | no |  | language of the spell check |
| `checks_threshold` | string | no |  | custom threshold values for checks |
| `crawl_delay` | integer | no |  | delay between hits, ms |
| `crawl_sitemap_only` | boolean | no |  | crawl only pages indicated in the sitemap |
| `custom_robots_txt` | string | no |  | custom robots.txt settings |
| `custom_sitemap` | string | no |  | custom sitemap url |
| `custom_js` | string | no |  | custom javascript executed on each crawled page |
| `custom_user_agent` | string | no |  | custom user agent |
| `disable_cookie_popup` | boolean | no |  | disable the cookie popup |
| `disable_page_checks` | any[] | no |  | prevent certain page checks from running |
| `disable_sitewide_checks` | any[] | no |  | prevent certain sitewide checks from running |
| `disallowed_subdomains` | any[] | no |  | subdomains not to crawl |
| `enable_browser_rendering` | boolean | no |  | emulate browser rendering to measure Core Web Vitals |
| `enable_content_parsing` | boolean | no |  | parse content on crawled pages |
| `enable_www_redirect_check` | boolean | no |  | check if the domain implemented the www redirection |
| `enable_xhr` | boolean | no |  | enable XMLHttpRequest on a page |
| `force_sitewide_checks` | boolean | no |  | enable sitewide checks when crawling a single page |
| `load_resources` | boolean | no |  | load resources |
| `max_crawl_depth` | integer | no |  | crawl depth |
| `pingback_url` | string | no |  | notification URL of a completed task |
| `priority_urls` | any[] | no |  | urls to be crawled bypassing the queue |
| `respect_sitemap` | boolean | no |  | respect sitemap when crawling |
| `return_despite_timeout` | boolean | no |  | return data on pages despite the timeout error |
| `robots_txt_merge_mode` | enum(merge, override) | no |  | merge with or override robots.txt settings |
| `store_raw_html` | boolean | no |  | store HTML of crawled pages |
| `support_cookies` | boolean | no |  | support cookies on crawled pages |
| `switch_pool` | boolean | no |  | switch proxy pool |
| `tag` | string | no |  | user-defined task identifier |
| `validate_micromarkup` | boolean | no |  | enable microdata validation |
| `target` | string | yes |  | Website URL to crawl |
| `max_crawl_pages` | integer | no |  | Max pages to crawl |
| `start_url` | string | no |  |  |
| `enable_javascript` | boolean | no |  |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "accept_language": {
      "type": "string",
      "description": "language header for accessing the website"
    },
    "allow_subdomains": {
      "type": "boolean",
      "description": "include pages on subdomains"
    },
    "allowed_subdomains": {
      "type": "array",
      "description": "subdomains to crawl"
    },
    "browser_preset": {
      "type": "string",
      "description": "preset for browser screen parameters"
    },
    "browser_screen_height": {
      "type": "integer",
      "description": "browser screen height"
    },
    "browser_screen_scale_factor": {
      "type": "number",
      "description": "browser screen scale factor"
    },
    "browser_screen_width": {
      "type": "integer",
      "description": "browser screen width"
    },
    "calculate_keyword_density": {
      "type": "boolean",
      "description": "calculate keyword density for the target domain"
    },
    "check_spell": {
      "type": "boolean",
      "description": "check spelling"
    },
    "check_spell_exceptions": {
      "type": "array",
      "description": "words excluded from spell check"
    },
    "check_spell_language": {
      "type": "string",
      "description": "language of the spell check"
    },
    "checks_threshold": {
      "type": "string",
      "description": "custom threshold values for checks"
    },
    "crawl_delay": {
      "type": "integer",
      "description": "delay between hits, ms"
    },
    "crawl_sitemap_only": {
      "type": "boolean",
      "description": "crawl only pages indicated in the sitemap"
    },
    "custom_robots_txt": {
      "type": "string",
      "description": "custom robots.txt settings"
    },
    "custom_sitemap": {
      "type": "string",
      "description": "custom sitemap url"
    },
    "custom_js": {
      "type": "string",
      "description": "custom javascript executed on each crawled page"
    },
    "custom_user_agent": {
      "type": "string",
      "description": "custom user agent"
    },
    "disable_cookie_popup": {
      "type": "boolean",
      "description": "disable the cookie popup"
    },
    "disable_page_checks": {
      "type": "array",
      "description": "prevent certain page checks from running"
    },
    "disable_sitewide_checks": {
      "type": "array",
      "description": "prevent certain sitewide checks from running"
    },
    "disallowed_subdomains": {
      "type": "array",
      "description": "subdomains not to crawl"
    },
    "enable_browser_rendering": {
      "type": "boolean",
      "description": "emulate browser rendering to measure Core Web Vitals"
    },
    "enable_content_parsing": {
      "type": "boolean",
      "description": "parse content on crawled pages"
    },
    "enable_www_redirect_check": {
      "type": "boolean",
      "description": "check if the domain implemented the www redirection"
    },
    "enable_xhr": {
      "type": "boolean",
      "description": "enable XMLHttpRequest on a page"
    },
    "force_sitewide_checks": {
      "type": "boolean",
      "description": "enable sitewide checks when crawling a single page"
    },
    "load_resources": {
      "type": "boolean",
      "description": "load resources"
    },
    "max_crawl_depth": {
      "type": "integer",
      "description": "crawl depth"
    },
    "pingback_url": {
      "type": "string",
      "description": "notification URL of a completed task"
    },
    "priority_urls": {
      "type": "array",
      "description": "urls to be crawled bypassing the queue"
    },
    "respect_sitemap": {
      "type": "boolean",
      "description": "respect sitemap when crawling"
    },
    "return_despite_timeout": {
      "type": "boolean",
      "description": "return data on pages despite the timeout error"
    },
    "robots_txt_merge_mode": {
      "type": "string",
      "description": "merge with or override robots.txt settings",
      "enum": [
        "merge",
        "override"
      ]
    },
    "store_raw_html": {
      "type": "boolean",
      "description": "store HTML of crawled pages"
    },
    "support_cookies": {
      "type": "boolean",
      "description": "support cookies on crawled pages"
    },
    "switch_pool": {
      "type": "boolean",
      "description": "switch proxy pool"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "validate_micromarkup": {
      "type": "boolean",
      "description": "enable microdata validation"
    },
    "target": {
      "type": "string",
      "description": "Website URL to crawl"
    },
    "max_crawl_pages": {
      "type": "integer",
      "description": "Max pages to crawl",
      "minimum": 1,
      "maximum": 100000
    },
    "start_url": {
      "type": "string"
    },
    "enable_javascript": {
      "type": "boolean"
    }
  },
  "required": [
    "target"
  ]
}
```

## Example request

```json
{
  "target": "example.com"
}
```

## Output

_No output schema or active profile response_format._

> Profile capture status: **error** — DataForSEOError: DataForSEO task errors: 40501: Invalid Field: 'max_crawl_pages'.

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing credentials | Check DATAFORSEO_LOGIN and DATAFORSEO_PASSWORD env vars |
| 402 | Insufficient balance | Top up DataForSEO account balance |
| 429 | Rate limit exceeded | Wait 10s and retry once |
| 500 | Server error | Retry after 30s; skip tool if persistent |

## When to use

- DataForSEO live calls bill per request — prefer Labs domain/keyword endpoints over full SERP scrapes when comparing domains
- Pass location_code + language_name (or language_code) for geo-correct volumes; defaults skew US/English
- Async/task endpoints need task_id follow-up; live endpoints return tasks[].result in one call

**Chain groups:** `dataforseo_onpage`

## Alternatives

- `dataforseo_ai_llm_mentions_top_pages`
- `dataforseo_labs_page_intersection`
- `dataforseo_labs_relevant_pages`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
