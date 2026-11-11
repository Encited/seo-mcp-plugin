# Encited SEO MCP and Plugin

SEO MCP and Plugin for Claude Code, Claude, ChatGPT, Codex, Cursor and Grok.

Ask about your own site from your AI tool and get answers from live data: is Googlebot visiting, why a page is not indexed, which queries earn clicks, what ChatGPT says about your brand, and what to write next. Then run the fix from the same chat: start an audit, launch a content workflow, or build a client report.

- **Hosted MCP server:** `https://encited.com/api/mcp` (streamable HTTP, OAuth). Nothing to install or run.
- **Plugin:** the same server plus the `encited` skill, packaged for Claude Code, Codex, Cursor and Grok.
- **83 tools:** Search Console, technical SEO audits, index status, keyword research, AI search visibility, content workflows, crawl logs, pre-rendering and client reports.

Listed in the [official MCP Registry](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.encited) as `com.encited/encited`, on [Glama](https://glama.ai/mcp/connectors/com.encited/encited), and in the [Claude connector directory](https://claude.ai/directory/encited).

## Installation

Every client signs in the same way: on first use of an Encited tool, the client opens Encited sign-in in the browser. Sign in with your Encited account. Do not paste an API key or token into chat.

### Claude Code

1. Install the plugin:
    ```bash
    claude plugin marketplace add Encited/seo-mcp-plugin
    claude plugin install encited@encited
    ```

    Or add the server alone, without the skill:
    ```bash
    claude mcp add --transport http encited https://encited.com/api/mcp
    ```

2. Authenticate via OAuth:
    ```bash
    claude
    # Then run /mcp, select encited, and press Enter
    /mcp
    ```
    Then follow the browser prompts to log into Encited.

### Claude (web and desktop)

Add Encited from the [Claude connector directory](https://claude.ai/directory/encited), then sign in when the browser window opens.

### ChatGPT

Add `https://encited.com/api/mcp` as a custom connector, then sign in when ChatGPT asks. Step-by-step instructions are at [encited.com/seo-mcp](https://encited.com/seo-mcp).

### Cursor

Add manually in Cursor Settings > Plugins, or add `https://encited.com/api/mcp` to `~/.cursor/mcp.json` under `mcpServers`.

### Codex

1. Add the marketplace:
    ```bash
    codex plugin marketplace add Encited/seo-mcp-plugin
    ```

2. Install the plugin from inside Codex:
    ```
    codex
    # Then run /plugins, select Encited, and install
    /plugins
    ```

### Grok Build

```bash
grok plugin install Encited/seo-mcp-plugin --trust
```

### Any other MCP client

Add `https://encited.com/api/mcp` as an HTTP (streamable) server. Per-client steps for Lovable and others are at [encited.com/seo-mcp](https://encited.com/seo-mcp).

## Example usage

```
> Is Googlebot crawling my site?
> Did ClaudeBot read my pricing page this week?

> Why isn't /blog/new-post indexed?
> Which pages should Google recrawl so the new page gets found?

> What queries do we rank for?
> Which pages get impressions but no clicks?

> Audit my site and give me a prioritized fix list
> What does the crawler actually see on /pricing?

> Find keywords a competitor ranks for that we don't
> Do we already rank for these keywords?

> How does ChatGPT describe my brand?
> Which sites do AI answers cite in my space?

> Build a content plan from our AI visibility gaps
> Write the monthly SEO report for this client
```

## Tools

Every tool takes a domain from your account; the agent calls `list_domains` first. A connection approved read-only exposes the Read tools only. Tools that a plan does not include return `plan_upgrade_required` with the plan needed. Keyword searches and workflows spend credits from the account.

### Search Console

| Tool | What it does | Scope |
| --- | --- | --- |
| `get_gsc_connection_status` | Check whether a Search Console property is connected and verified | Read |
| `connect_gsc_property` | Get a link that connects Google Search Console for a domain | Write |
| `get_gsc_keywords` | Top Google queries for a domain: clicks, impressions, CTR and average position | Read |
| `get_gsc_page_analytics` | Clicks, impressions, CTR and average position per page | Read |
| `get_gsc_site_health` | Total clicks, impressions, CTR and average position over the last N days | Read |
| `query_gsc_analytics` | Search Console rows by any dimensions and filters | Read |
| `inspect_gsc_url` | Ask Google whether one URL is indexed, and why not if it isn't | Read |

### Technical SEO audit

| Tool | What it does | Scope |
| --- | --- | --- |
| `start_seo_audit` | Start an SEO audit crawl for a domain | Write |
| `list_seo_audit_runs` | List SEO audit runs, newest first | Read |
| `get_seo_audit_run` | One audit run: summary plus per-page status, load time, health score and issues | Read |
| `get_seo_audit_page` | One audited page's full record | Read |
| `get_seo_audit_issues` | Current SEO issues across the domain, with severity and affected pages | Read |

### Index status

| Tool | What it does | Scope |
| --- | --- | --- |
| `get_index_rush_pages` | Sitemap URLs with their Google index status, SEO issue counts and inbound links | Read |
| `get_index_rush_inbound_links` | Internal-link data for getting not-indexed pages discovered | Read |

### Keyword research

| Tool | What it does | Scope |
| --- | --- | --- |
| `search_keywords` | Keyword ideas with search volume, difficulty, CPC, intent and your own Search Console position | Write |
| `check_keyword_coverage` | Which keywords from a list the domain already ranks for | Write |
| `list_keyword_searches` | Stored keyword searches for a domain, newest first | Read |
| `get_keyword_search` | One stored keyword search with every keyword row | Read |
| `delete_keyword_search` | Remove a stored keyword search | Write |

### AI search visibility

| Tool | What it does | Scope |
| --- | --- | --- |
| `get_visibility_by_prompt` | Visibility score per tracked prompt: mention rate, position, sentiment and citations | Read |
| `get_visibility_by_provider` | Visibility score per AI engine, so you see where the brand shows up and where it does not | Read |
| `list_competitors` | Share of AI answers that mention the brand vs each competitor | Read |
| `list_citations` | Domains AI engines cite in their answers, with counts | Read |
| `list_fanout_queries` | Web searches AI engines ran while answering your prompts | Read |
| `list_ai_prompts` | The prompts tracked for a domain | Read |
| `list_ai_prompt_runs` | Completed AI answers per prompt, engine and day | Read |
| `get_ai_prompt_run` | One AI answer in detail: competitors mentioned, cited domains and the searches behind it | Read |
| `get_ai_visibility_reports` | The weekly AI visibility reports for a domain | Read |
| `generate_ai_visibility_report` | Generate the first AI visibility report now instead of waiting for the scheduled one | Write |
| `add_ai_prompt` | Track a new prompt | Write |
| `update_ai_prompt` | Change a tracked prompt's text, intent, engines or tags | Write |
| `pause_ai_prompt` | Pause or resume a tracked prompt | Write |
| `get_brand_book` | The brand book: name, description, facts, competitors and personas | Read |
| `generate_brand_book` | Build the brand book from the site itself | Write |
| `create_brand_book` | Create a brand book for a domain that has none | Write |
| `update_brand_book` | Update an existing brand book | Write |

### Content workflows

| Tool | What it does | Scope |
| --- | --- | --- |
| `write_article` | Research ranking pages and draft an article with outline, FAQs, structured data and internal links | Write |
| `refresh_page` | Read an existing page and its competitors, then draft a revised version with a change list | Write |
| `build_content_plan` | A content plan from seed keywords, a competitor's keywords, or AI visibility gaps | Write |
| `build_refresh_plan` | A prioritized refresh plan for pages close to page one | Write |
| `audit_search_console` | Ranking opportunities, low CTR, competing pages and snippet targets from Search Console | Write |
| `check_serp_position` | The top 20 Google results for one query and where this site ranks | Write |
| `analyze_serp` | Crawl up to ten ranking pages and analyze their shared content patterns and intent | Write |
| `research_competitor` | Compare a competitor with this site: domain metrics, keywords and backlink gaps | Write |
| `find_link_gaps` | Sites that link to competitors but not to this domain | Write |
| `audit_local_seo` | The business profile, map-pack rivals, reviews and service-area pages | Write |
| `write_service_area_pages` | Draft up to ten service-area pages with local structured data | Write |
| `scan_map_grid` | Scan a 5×5 Google Maps grid around a location and save a report | Write |
| `share_workflow_result` | Turn on a public link for a finished workflow result | Write |
| `list_workflows` | The built-in workflow catalog with credit costs | Read |
| `get_workflow` | One workflow's description, result type and credit cost | Read |
| `get_workflow_credits` | Workflow credit balance for the current billing cycle | Read |
| `list_workflow_runs` | Workflow runs, newest first | Read |
| `get_workflow_run` | One workflow run with per-step progress | Read |
| `get_workflow_result` | The finished output of a workflow run | Read |

### Content ideas and actions

| Tool | What it does | Scope |
| --- | --- | --- |
| `list_content_ideas` | Every page idea from the domain's content plans, in one list | Read |
| `set_content_idea_status` | Shortlist or dismiss a content idea | Write |
| `draft_content_idea` | Draft one content idea | Write |
| `list_content_actions` | The actions board for a domain | Read |
| `update_content_action` | Move an action to to_do, doing, done or dismissed | Write |

### Crawl logs

| Tool | What it does | Scope |
| --- | --- | --- |
| `query_crawl_logs` | Recent search and AI crawler visits, with filters | Read |
| `get_crawl_stats` | Top search and AI crawlers, pages crawled and a per-day breakdown | Read |

### Pre-rendering

| Tool | What it does | Scope |
| --- | --- | --- |
| `get_snapshot` | What crawlers get for a page: age, size, SEO analysis and optionally the HTML | Read |
| `list_snapshots` | Prerendered snapshots for a domain | Read |
| `rerender_pages` | Re-render pages now so crawlers get the live version | Write |
| `rerender_site` | Start a site-wide re-render in the background | Write |
| `get_render_job` | Progress of a site re-render | Read |
| `remove_snapshots` | Remove the snapshots of specific pages | Write |
| `remove_stale_snapshots` | Remove snapshots in bulk | Write |
| `get_middleware_setup` | The pre-rendering middleware snippet and install steps for a domain | Read |
| `verify_middleware` | Check the domain as a crawler and confirm the middleware works | Write |

### Client reports

| Tool | What it does | Scope |
| --- | --- | --- |
| `list_reports` | Client reports for a domain, most recently edited first | Read |
| `get_report` | One report with all its blocks and the client share link | Read |
| `create_report` | Compose a new client report | Write |
| `update_report` | Edit a report's title, period, theme or blocks | Write |
| `delete_report` | Delete a report | Write |

### Sites and setup

| Tool | What it does | Scope |
| --- | --- | --- |
| `list_domains` | The domains in this Encited account | Read |
| `get_domain` | One domain's settings | Read |
| `add_domain` | Add a site to the account: your own or a client's | Write |
| `update_domain_settings` | Change a domain's settings | Write |
| `update_domain_sitemap` | Set, clear or re-fetch a domain's sitemap URL | Write |
| `delete_domain` | Remove a domain from the account | Write |
| `read_me` | Usage guidance and playbooks for the other tools | Read |

## Bundled skill

The plugin ships one skill, `encited`, that routes SEO, content, ranking, and AI-search questions to the right tool and explains how to run a workflow end to end. It activates when its description matches your request, so you do not need to invoke it by name.

## Authentication and network

The plugin connects only to `https://encited.com`. Authentication is OAuth 2.1 with PKCE and dynamic client registration.

Endpoints:

- `https://encited.com/api/mcp`: hosted MCP (streamable HTTP)
- `https://encited.com/authorize`, `/oauth/token`, `/oauth/register`: OAuth 2.1 + DCR
- `https://encited.com/.well-known/oauth-authorization-server` and `/.well-known/oauth-protected-resource`: discovery

Credentials: an Encited account. The access token is sent as `Authorization: Bearer` on `/api/mcp`. No API key is stored in the plugin. Tools are scoped to the domains the signed-in user can access.

The plugin runs no local code: no hooks, no commands, no scripts.

## How to develop

```bash
git clone https://github.com/Encited/seo-mcp-plugin
claude --plugin-dir ./seo-mcp-plugin
```

Then run `/mcp` and follow the browser prompts to log into Encited.

`server.json` is the entry published to the official MCP Registry.

## Documentation

- [Encited MCP](https://encited.com/seo-mcp)
- [Encited](https://encited.com)
- Support: team@encited.com

## License

The files in this repository are licensed under the [MIT License](LICENSE). Use of the hosted MCP is governed by the [Encited terms](https://encited.com/terms). The Encited name and logo are trademarks of Encited and are not covered by the MIT grant.
