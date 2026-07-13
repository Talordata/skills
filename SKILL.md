---
name: talordata-serp-mcp
description: Use when a user needs structured Talordata SERP results through installed Talordata MCP for Google, Bing, Yandex, DuckDuckGo, news, images, videos, maps/local, shopping, SEO ranking, price/news/local monitoring, fresh public search data, or research with source links.
---

# Talordata SERP MCP

Use Talordata MCP when the user needs structured public search-engine result data, not ordinary web browsing or webpage extraction. MCP is responsible for the actual call; this skill is responsible for choosing a valid Talor SERP schema, required parameters, output fields, and interpretation boundaries.

Current Talor project schema source of truth: `api/talor-pay-package-view/configs/serp_schemas/engines/*.yaml`. If a schema file and old prose documentation disagree, prefer the schema file for supported schema keys and required parameters.

## First Checks

1. Check whether a Talordata MCP tool is installed and visible in the current agent. If it is missing, say it is unavailable and do not fabricate results.
2. Check whether API authentication is configured. If auth fails, report MCP/API-key configuration failure instead of "no results."
3. Identify the user intent and choose a Talor schema key from [rules/engines.md](rules/engines.md).
4. Ask one clarification question when the task depends on missing query, country, city, language, date/freshness, or batch scope.
5. Use the installed Talordata MCP tool. Do not hand-write guessed HTTP endpoints unless the user explicitly asks for API examples.
6. Preserve source links, query conditions, and query timestamp for freshness-sensitive tasks.

## Quick Schema Choices

| Intent | Prefer Talor schema key |
| --- | --- |
| General web search | `google_web`, fallback `bing` |
| News or public-opinion monitoring | `google_news`, fallback `bing_news` |
| Image search | `google_images`, fallback `bing_images` |
| Video search | `google_videos`, fallback `bing_videos` |
| Local business or map results | `google_maps`, `google_local`, fallback `bing_maps` |
| Product search or price monitoring | `google_shopping`, fallback `bing_shopping` |
| Finance or market data | `google_finance`, `google_finance_markets` |
| Flights | `google_flights` |
| Hotels | `google_hotels` |
| Jobs | `google_jobs` |
| Academic search | `google_scholar`, `google_scholar_author`, `google_scholar_cite` |
| Trends | `google_trends` |
| Google Lens | `google_lens` |
| Google Play | `google_play`, `google_play_product`, `google_play_books`, `google_play_games`, `google_play_movies` |
| Patents | `google_patents`, `google_patents_details` |
| Yandex search | `yandex` |
| DuckDuckGo search | `duckduckgo` |

For full supported schema keys, query fields, required parameters, and engine/type mapping, read [rules/engines.md](rules/engines.md). Never use SerpApi-specific names such as `google_light` or `google_news_light` for Talordata.

## Read The Right Rule File

- Exact supported schema keys and required fields: [rules/engines.md](rules/engines.md)
- Parameter defaults and clarification triggers: [rules/parameters.md](rules/parameters.md)
- Output fields, empty results, and API errors: [rules/response.md](rules/response.md)
- Common monitoring/research workflows: [rules/use-cases.md](rules/use-cases.md)
- Product boundary, privacy, and "do not" rules: [rules/guardrails.md](rules/guardrails.md)

## Output Defaults

- SEO ranking: table with `keyword`, `position`, `title`, `link`, `snippet`.
- News: table with `title`, `source`, `published_time`, `link`.
- Shopping: table with `title`, `price`, `seller`, `rating`, `link`.
- Maps/local: table with `name` or `business_name`, `address`, `rating`, `phone`, `website`.
- Research: list sources first, then summarize with source attribution.
- Batch tasks: prefer CSV or JSON and dedupe by URL/title/source.

Only include fields present in the MCP response. Do not infer missing prices, ratings, phone numbers, addresses, or publication times.

## Hard Stops

- Do not invent unsupported engines, schema keys, result types, parameters, or fields.
- Do not silently replace specialized schemas such as news, shopping, maps/local, jobs, scholar, finance, flights, hotels, or trends with generic web search.
- Do not claim success when MCP is missing, authentication failed, quota failed, timed out, or returned an API error.
- Do not treat Talordata SERP as a general-purpose crawler, full webpage extractor, anti-bot bypass, or private-data access tool.
- Do not omit source links or query conditions from summarized results.
