# Talordata SERP Use Cases

Use this file to choose the right schema and output pattern for common tasks.

## Intent Mapping

| User task | Primary schema | Secondary/fallback |
| --- | --- | --- |
| General public web research | `google_web` | `bing`, `duckduckgo` |
| SEO ranking check | `google_web` | `bing` |
| Latest news / monitoring | `google_news` | `bing_news` |
| Brand or competitor monitoring | `google_web` + `google_news` | `bing`, `bing_news` |
| Image search | `google_images` | `bing_images` |
| Video search | `google_videos` | `bing_videos` |
| Local business / maps | `google_maps` or `google_local` | `bing_maps` |
| Product and price monitoring | `google_shopping` | `bing_shopping`, `google_web` with site-specific query when requested |
| Finance / ticker data | `google_finance` | `google_finance_markets` |
| Flight search | `google_flights` | Ask before fallback |
| Hotel search | `google_hotels` | Ask before fallback |
| Job listings | `google_jobs` | Ask before fallback |
| Academic search | `google_scholar` | Ask before generic web fallback |
| Scholar author lookup | `google_scholar_author` | none without user approval |
| Citation lookup | `google_scholar_cite` | none without user approval |
| Trends | `google_trends` | Ask before fallback |
| Patents | `google_patents`, `google_patents_details` | Ask before fallback |
| Visual lookup | `google_lens` | Ask before fallback |
| Google Play search/product | `google_play`, `google_play_product` | Ask before fallback |
| Yandex-specific search | `yandex` | none unless user agrees |
| DuckDuckGo-specific search | `duckduckgo` | none unless user agrees |

## Common Patterns

### Research

Run the smallest useful set of searches, extract source links immediately, then synthesize:

1. Search the primary schema.
2. Extract `title`, `link`, `snippet/source/date`.
3. Add a secondary schema only when it changes the evidence quality, such as news plus web for brand monitoring.
4. Summarize only what is supported by returned results.

### SEO Ranking

Use one stable query setup per comparison:

- Same schema
- Same query
- Same country/region
- Same language
- Same device
- Same timestamp window when possible

Report ranking as "under these query conditions", not as permanent SEO truth.

### News Monitoring

Use `google_news` or `bing_news`, include query timestamp, and preserve `source`, `published_time/date`, and `link`. Do not use generic web search as a silent substitute.

### Shopping / Price Monitoring

Use `google_shopping` or `bing_shopping` for marketplace-style price results. If the user asks for a specific retailer's price, use a targeted web query only when that is the better match and explain the choice.

### Local Business

Use `google_maps` or `google_local`, not generic web search. Ask for city/region when missing. Separate map/local results from web organic results.

### Batch Monitoring

Before running:

- Confirm keyword list.
- Confirm schema/engine family.
- Confirm country, language, and location.
- Confirm result depth and output format.
- Avoid duplicate query + schema + region calls.

Prefer CSV or JSON output for large result sets.
