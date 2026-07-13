# Talordata SERP Response Handling

Use this file when converting MCP responses into user-facing answers. Talordata SERP response shapes vary by schema; inspect the returned JSON instead of assuming one universal key.

## Preserve Fields By Scenario

| Scenario | Preserve when present |
| --- | --- |
| Ranking / web | `position`, `title`, `link`, `snippet` |
| News | `title`, `source`, `published_time`, `date`, `link` |
| Shopping | `title`, `price`, `seller`, `source`, `rating`, `link` |
| Maps/local | `business_name`, `name`, `address`, `rating`, `reviews`, `phone`, `website`, `link` |
| Images | `title`, `image_url`, `thumbnail`, `source`, `link` |
| Videos | `title`, `link`, `source`, `duration`, `published_time`, `views` |
| Finance | `symbol`, `name`, `price`, `change`, `currency`, `market`, `link` |
| Flights/hotels | price, dates/times, provider, airline/hotel name, location, rating when present |
| Scholar | `title`, `link`, `snippet`, authors/source/year/citation fields when present |

Keep the original `link` or source URL whenever available. Do not replace links with only a summary.

## Output Formats

| Task | Recommended output |
| --- | --- |
| SEO ranking | Table: `keyword`, `position`, `title`, `link`, `snippet` |
| News monitoring | Table: `title`, `source`, `published_time`, `link` |
| Shopping monitoring | Table: `title`, `price`, `seller/source`, `rating`, `link` |
| Maps/local | Table: `name`, `address`, `rating`, `phone`, `website` |
| Research | Sources first, then concise synthesis tied to sources |
| Batch | CSV or JSON; dedupe by URL/title/source |

## Freshness And Query Conditions

Include the query timestamp for:

- News
- Prices
- Rankings
- Ads
- Inventory or availability
- "latest", "today", "current", or "now" requests

When relevant, state the schema key, query, country/region, language, device, and time filter used. Do not describe one country's results as global.

## API Errors Are Not Empty Results

Never explain API failure as "no results."

| Condition | Response |
| --- | --- |
| MCP unavailable | Say Talordata MCP is not installed/visible in this agent. |
| Authentication failure | Say API key or MCP auth configuration failed. |
| Parameter error | Identify the invalid/missing schema, engine/type, or parameter. |
| Quota/usage failure | Say it may be quota, usage, billing, or account related. |
| Timeout | Suggest narrowing scope or retrying later. |
| Successful empty response | Only then say no results were returned for the given query conditions. |

## Interpretation Limits

- Do not fabricate missing fields or normalize uncertain values as facts.
- Do not re-rank results subjectively unless the user asks for secondary analysis.
- Do not treat snippets as full webpage content.
- Do not treat SERP summaries as verified facts.
- If results conflict, state the conflict.
- If results are insufficient, say current results are insufficient to determine.
