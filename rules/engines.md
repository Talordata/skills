# Talordata SERP Engines

Use this file to validate Talor SERP schema keys and required parameters before any MCP call. These schema keys come from `api/talor-pay-package-view/configs/serp_schemas/engines/*.yaml`.

## Contents

- Supported schema keys
- Schema key to engine/type mapping
- Required parameters
- Unsupported names
- Fallback rules

## Supported Schema Keys

| Schema key | Category | Query field | Required parameters |
| --- | --- | --- | --- |
| `google_web` | `google` | `q` | `q` |
| `google` | `google` | `q` | `q` |
| `google_news` | `google` | `q` | `q` |
| `google_images` | `google` | `q` | `q` |
| `google_videos` | `google` | `q` | `q` |
| `google_maps` | `google` | `q` | `q` |
| `google_local` | `google` | `q` | `q` |
| `google_shopping` | `google` | `q` | `q` |
| `google_ai_mode` | `google` | `q` | `q` |
| `google_finance` | `google` | `q` | `q` |
| `google_finance_markets` | `google` | `trend` | `trend` |
| `google_flights` | `google` | `q` | `departure_id`, `arrival_id`, `trip_dates` |
| `google_hotels` | `google` | `q` | `q`, `check_in_date`, `check_out_date` |
| `google_jobs` | `google` | `q` | `q` |
| `google_lens` | `google` | `url` | `url` |
| `google_patents` | `google` | `q` | `q` |
| `google_patents_details` | `google` | `patent_id` | `patent_id` |
| `google_play` | `google` | `q` | `q` |
| `google_play_books` | `google` | `q` | none in schema |
| `google_play_games` | `google` | `q` | none in schema |
| `google_play_movies` | `google` | `q` | none in schema |
| `google_play_product` | `google` | `product_id` | `product_id` |
| `google_product` | `google` | `product_id` | `product_id` |
| `google_scholar` | `google` | `q` | `q` |
| `google_scholar_author` | `google` | `author_id` | `author_id` |
| `google_scholar_cite` | `google` | `q` | `q` |
| `google_trends` | `google` | `q` | `q` |
| `bing` | `bing` | `q` | `q` |
| `bing_news` | `bing` | `q` | `q` |
| `bing_images` | `bing` | `q` | `q` |
| `bing_videos` | `bing` | `q` | `q` |
| `bing_maps` | `bing` | `q` | `q` |
| `bing_shopping` | `bing` | `q` | `q` |
| `yandex` | `yandex` | `text` | `text` |
| `duckduckgo` | `duckduckgo` | `q` | `q` |

Prefer the specific schema key (`google_web`, `google_images`, `google_news`) over the generic `google` schema when the task has a clear vertical. Use generic `google` only when the MCP/tool surface exposes it directly or the task needs advanced generic Google options.

## Engine/Type Mapping

When the MCP exposes `engine` plus `type` instead of a Talor schema key, map as follows:

| Talor schema key | Engine/type |
| --- | --- |
| `google_web` or `google` | `google/web` |
| `google_news` | `google/news` |
| `google_images` | `google/images` |
| `google_videos` | `google/videos` |
| `google_maps` | `google/maps` |
| `google_local` | `google/local` |
| `google_shopping` | `google/shopping` |
| `google_ai_mode` | `google/ai_mode` |
| `google_finance` | `google/finance` |
| `google_finance_markets` | `google/finance_markets` |
| `google_flights` | `google/flights` |
| `google_hotels` | `google/hotels` |
| `google_jobs` | `google/jobs` |
| `google_lens` | `google/lens` |
| `google_patents` | `google/patents` |
| `google_patents_details` | `google/patents_details` |
| `google_play` | `google/play_search` |
| `google_play_books` | `google/play_books` |
| `google_play_games` | `google/play_games` |
| `google_play_movies` | `google/play_movies` |
| `google_play_product` | `google/play_product` |
| `google_product` | `google/product` when exposed by the MCP schema |
| `google_scholar` | `google/scholar` |
| `google_scholar_author` | `google/scholar_author` |
| `google_scholar_cite` | `google/scholar_cite` |
| `google_trends` | `google/trends` |
| `bing` | `bing/search` |
| `bing_news` | `bing/news` |
| `bing_images` | `bing/images` |
| `bing_videos` | `bing/videos` |
| `bing_maps` | `bing/maps` |
| `bing_shopping` | `bing/shopping` |
| `yandex` | `yandex/search` |
| `duckduckgo` | `duckduckgo/search` |

If the MCP tool's own schema uses different names, follow the MCP tool schema but preserve the same product boundaries. Do not invent a key not present in either Talor schema files or the MCP tool schema.

## Unsupported Names

Do not use:

- SerpApi-specific names: `google_light`, `google_news_light`, `google_images_light`, `search_index`, `youtube`, `amazon`, `walmart`, `ebay`, `yelp`.
- Unsupported engines from the requirements: `baidu`, `yahoo`, `naver`, `seznam`, `ask`.
- Cross-engine types: DuckDuckGo `news/images/videos`, Yandex `images/news/maps`, Bing `finance/flights/hotels/jobs/scholar`.

`google scholar` and `google finance` are not engines. Use `google_scholar`, `google_finance`, or the matching `google/<type>` pair.

## Fallback Rules

Allowed automatic fallback:

- `google_web` or `google/web` -> `bing` or `bing/search`
- `google_news` -> `bing_news`
- `google_images` -> `bing_images`
- `google_videos` -> `bing_videos`
- `google_shopping` -> `bing_shopping`
- `google_maps` or `google_local` -> `bing_maps`

Do not automatically fallback without user approval for:

- `google_flights`
- `google_hotels`
- `google_jobs`
- `google_scholar`
- `google_trends`
- `google_finance`
- `google_finance_markets`
- `google_patents`
- `google_patents_details`
- `google_lens`
- Google Play and product-detail schemas

When fallback is used, state the original schema, fallback schema, and reason.
