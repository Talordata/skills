# Talordata SERP Guardrails

Use this file when a task risks overclaiming, unsupported access, privacy issues, or misuse of SERP data.

## Product Boundary

Talordata SERP provides search-engine result page data. It is suitable for:

- Search monitoring
- Ranking checks
- News discovery
- Product and price search
- Local business search
- Public research with source links

It is not:

- A general-purpose web crawler
- A full webpage text extractor
- A tool for bypassing anti-bot systems
- A login/session/private-data scraper
- A replacement for source verification

If the user needs webpage body content, use another approved crawler/browser tool or ask the user to provide the webpage content.

## Do Not

- Do not invent unsupported engines, schema keys, result types, parameters, or fields.
- Do not mix result types across engines.
- Do not call guessed raw HTTP endpoints when Talordata MCP tools are available.
- Do not claim success when MCP is not installed or API authentication failed.
- Do not treat API failures as empty search results.
- Do not treat SERP snippets as full webpage content.
- Do not omit source links from summaries.
- Do not silently replace specialized schemas with generic web search.
- Do not interpret one region's results as global results.
- Do not confuse ads, organic results, shopping results, local results, or news results.
- Do not run large batch queries without confirming scope.
- Do not treat one SERP query as a permanent ranking, market share, brand popularity, or public-opinion conclusion.

## Privacy And Compliance

Talordata SERP should only process public search-result data.

Do not help users:

- Access logged-in, paywalled, private-account, or non-public data.
- Bypass access controls, CAPTCHA, or platform restrictions.
- Bulk collect personal phone numbers, emails, addresses, or other sensitive personal data.
- Dox, track, harass, or profile individuals.
- Use SERP results for automated high-risk personal decisions such as credit, employment, insurance, medical, financial, or legal eligibility.

For personal, medical, financial, or legal topics, state that results come from search engines and the user should verify original sources.

## Multi-Turn Safety

- Do not silently inherit schema, query, country, language, or location from an unrelated previous task.
- If inheriting settings, state them explicitly.
- Re-evaluate the schema when the user changes intent.
- Stop and ask when a new turn changes from web/news to local/shopping/flights/hotels/jobs/scholar because required parameters differ.
