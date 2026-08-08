# Talordata SERP Parameters

Use this file to decide which parameters are safe to default and which ones require clarification. Prefer the active MCP tool schema when it is available; otherwise follow the Talor schema files summarized here.

## Common Parameters

| Parameter | Use |
| --- | --- |
| `q` | Search query for most Google, Bing, DuckDuckGo, maps/local, shopping, news, jobs, scholar, hotels, and trends schemas. |
| `text` | Required search text for `yandex`. |
| `gl` | Country code for Google-style localization. Project schema defaults commonly use `us`. |
| `hl` | Language code for Google-style localization. Project schema defaults commonly use `en`. |
| `location` | Country/city/region selector. Use when ranking, local, ads, shopping, or news depends on geography. |
| `device` | Device context for schemas that support desktop/mobile/tablet. Rankings can change by device. |
| `start` | Pagination offset. Confirm result depth before paging. |
| `num` | Result count when supported. Confirm scope for batch/monitoring tasks. |
| `no_cache` | Fresh/live fetch when supported. Use only when freshness matters because it can increase cost. |
| `tbs`, `period_unit`, `period_value`, `start_date`, `end_date` | Time filtering when supported. Prefer explicit user dates/freshness requirements. |
| `safe` | Safe-search option when supported. Preserve user preference. |

## Special Required Parameters

| Schema key | Required parameters | Clarification rule |
| --- | --- | --- |
| `google_flights` | `departure_id`, `arrival_id`, `trip_dates` | Ask for origin airport, destination airport, outbound date, and return date unless explicitly one-way support is available in the MCP schema. |
| `google_hotels` | `q`, `check_in_date`, `check_out_date` | Ask for destination/property query and dates. Ask adults/guests if needed for price interpretation. |
| `google_lens` | `url` | Ask for an image URL. Do not treat free text as enough. |
| `google_patents_details` | `patent_id` | Ask for the patent identifier. |
| `google_play_product` | `product_id` | Ask for the product/app identifier. |
| `google_product` | `product_id` | Ask for the product identifier. |
| `google_scholar_author` | `author_id` | Ask for the Scholar author id. |
| `google_finance_markets` | `trend` | Ask which market trend/market view is needed. |
| `yandex` | `text` | Map the user's query to `text`, not `q`, if the MCP exposes schema-style params. |

## Safe Defaults

- Default engine family: Google.
- Default general schema: `google` when a web result is enough.
- Default Google localization may follow schema defaults (`gl=us`, `hl=en`) when region/language is not material. State defaults when reporting results.
- Default Bing/Yandex/DuckDuckGo schema: `bing`, `yandex`, or `duckduckgo` only when the user asks for that engine or fallback is allowed.
- Default output: structured JSON or tables for analysis; concise source-backed summary for research.

## Must Ask Before Calling

Ask one concise question before calling when:

- Local, maps, ads, shopping, news, or SEO ranking depends on country/city/language and the user omitted it.
- The user asks to compare regions/countries but did not provide the list.
- The user asks for batch monitoring but omitted keywords, engines, schemas, country, language, or result depth.
- The user asks for prices/shopping but omitted the product or keyword.
- The query is ambiguous, such as "apple ranking."
- The task would require costly live/no-cache calls, deep pagination, or many repeated queries.

## Do Not

- Do not invent countries, cities, languages, date ranges, product ids, author ids, patent ids, airport codes, or batch sizes.
- Do not convert a vague request into a large batch job.
- Do not silently inherit region, language, schema, or query from a previous unrelated task.
- Do not loop retries after auth, quota, or parameter errors.
