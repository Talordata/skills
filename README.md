# TalorData SERP Skill

Use `talordata-serp-mcp` to guide AI agents when working with TalorData SERP through an installed MCP tool.

The skill helps agents choose valid engines, result types, parameters, output fields, fallback behavior, and safety rules for real-time public search results.

This repository contains the skill instructions only. It does not run a server or call the API by itself.

## Quick Start

### Install the skill

Copy this folder into your agent runtime's skills directory:

```plaintext
<skills-directory>/
`-- talordata-serp-mcp/
    |-- SKILL.md
    |-- agents/
    |   `-- openai.yaml
    `-- references/
        `-- serp-rules.md
```

Restart or reload the runtime after installation.

### Connect TalorData SERP

Configure a TalorData SERP MCP tool in the same runtime. The skill assumes the tool is already available and authenticated.

If the MCP tool or authentication is missing, the agent should report the setup issue instead of inventing results.

## Features

*   Maps user intent to the right SERP workflow
    
*   Supports web, news, images, videos, maps, shopping, finance, jobs, scholar, trends, and local search use cases
    
*   Preserves source links, query conditions, and timestamps
    
*   Guides SEO ranking, price monitoring, local research, news tracking, and batch SERP tasks
    
*   Prevents unsupported engines, invalid parameters, fabricated fields, and unsafe personal-data use
    

## Example prompts

```plaintext
Use Talordata SERP to search recent news about OpenAI and return title, source, published time, and link.
```

```plaintext
Check the Google organic ranking for "best CRM software" in the United States.
```

```plaintext
Compare shopping results for wireless earbuds and return title, price, seller, rating, and link.
```

## Skill behavior

Agents using this skill should:

*   Ask for missing query, location, country, language, freshness, or batch scope when required
    
*   Use specialized result types instead of silently falling back to generic web search
    
*   Include only fields returned by the MCP response
    
*   Treat API errors as errors, not empty results
    
*   Keep public source links visible in summaries and tables
    

## Project structure

| Path | Responsibility |
| --- | --- |
| `SKILL.md` | Main workflow, intent mapping, output guidance, and safety rules |
| `references/serp-rules.md` | Detailed engine/type validation, fallback, freshness, batch, and error-handling rules |
| `agents/openai.yaml` | Optional skill metadata for compatible agent UIs |

## Safety

Use this skill only for public search result data.

Do not use it to access private data, bypass restrictions, bulk collect sensitive personal data, profile individuals, or make automated high-risk decisions.

## Learn more

Explore TalorData SERP API integrations and use cases:

[TalorData SERP MCP](https://github.com/Talordata/talordata-mcp)

[Skill installation guides](https://docs.talordata.com/serp-api/mcp-server/skill-installation)
