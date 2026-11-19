# WeCookFlow MCP — guest post prices for AI agents

**WeCookFlow** compares guest post prices for the same websites across link-building marketplaces and open catalogs —
Serpzilla, Adsy, Bazoom, Collaborator, GPosting, Vefogix, GuestPostLinks, Links as a Service — and finds sites by
niche, country, language, DR, traffic and budget. The same site often costs 2–5× more in one place than in another.

This repository holds the public listing of the **remote MCP server** — there is nothing to install or run:

```
https://wecookflow.com/mcp
```

Transport: Streamable HTTP. Works right away with free limits; sign in with your email (OAuth, free, no password)
to raise them — your client opens the WeCookFlow sign-in page.

Step-by-step setup for every client: **https://wecookflow.com/mcp-setup**

## Connect

**Claude Code** — as a plugin (MCP server + a skill with usage hints):

```
/plugin marketplace add WeCookFlow/mcp
/plugin install wecookflow@wecookflow
```

or just the server:

```bash
claude mcp add --transport http --scope user wecookflow https://wecookflow.com/mcp
```

To sign in: `/mcp` → wecookflow → Authenticate (offered once a request goes over the free limits).

**Claude (claude.ai, Desktop)** — Settings → Connectors → Add → Add custom connector → URL
`https://wecookflow.com/mcp`, authentication: **Sign in now** (Claude may detect “No sign-in” — change it) → Add →
enter your email on the WeCookFlow page.

**ChatGPT** — Plugins → + → Add custom MCP server → Server URL, authentication: OAuth.

**Cursor, VS Code, Windsurf, Gemini CLI, Codex** — one-click links and configs on
[wecookflow.com/mcp-setup](https://wecookflow.com/mcp-setup). A generic JSON config:

```json
{ "mcpServers": { "wecookflow": { "type": "http", "url": "https://wecookflow.com/mcp" } } }
```

### Sign-in

Standard MCP OAuth: when a request goes over the free limits, the server answers `401` and your client offers to sign
in — the WeCookFlow page asks only for your email (no password, no confirmation email). The same email as on the
website or in the Chrome extension — the same account and limits.

Client can't sign in? Get a personal token by email at [wecookflow.com/mcp-setup](https://wecookflow.com/mcp-setup)
(“Client can't sign in?”) or let the agent call `sign_up`, then use the URL `https://wecookflow.com/mcp?token=ss_…`
or send `Authorization: Bearer ss_…`.

## Tools

| Tool | What it does |
|---|---|
| `compare_prices(domains, niche?)` | Prices for a list of sites or URLs (e.g. a competitor's backlinks) on every marketplace: best price and where, spread between the cheapest and the most expensive offer, DR and traffic. Sites not sold anywhere are listed separately. |
| `search_sites(niche?, topic?, country?, language?, min_dr?, min_traffic?, min_price?, max_price?, sort?, offset?, limit?)` | Sites that sell guest posts, with the best public price, by filters; sort by DR × traffic (default), DR, traffic or price; page with `offset`. Large brands, universities, government sites and suspiciously cheap high-DR listings (user-generated posts) are left out. |
| `list_channels()` | Marketplaces and catalogs whose prices are compared. |
| `sign_up(email)` | A free personal token by email — for clients that can't sign in. |

`niche`: `general` (default), `igaming`, `crypto`, `cbd`, `adult`. `compare_prices`, `search_sites` and
`list_channels` are read-only.

Try asking:

- “Where is a guest post cheapest for techbullion.com, hackernoon.com and dzone.com?”
- “Here are my competitor's referring domains — which sell guest posts and where is it cheapest?”
- “Find 20 English tech blogs with DR 50+ and a guest post under $150.”

## Limits

| | Not signed in | Signed in (free) |
|---|---|---|
| `compare_prices` | 50 sites per call | 1,000 sites per call |
| `search_sites` | the first 10 sites of a search | 50 per call, 1,000 a day |

## Data

Prices are public marketplace prices in USD for a guest post (article) and may be out of date — check the
final price before you buy. In search results `link_type` is `dofollow` when the marketplace says so, otherwise
`unknown`; placement format and terms are confirmed with the seller. DR is Domain Rating by
[Ahrefs](https://ahrefs.com/) (`dr_source: "ahrefs"`; where a site has none — as reported by sellers); traffic is as
reported by sellers and catalogs, not verified.

## Privacy

The server receives the sites you compare, your search filters and, if you sign in, your email (the token is stored
only as a hash). No ads, no selling data. Full policy: [wecookflow.com/privacy](https://wecookflow.com/privacy).

## Also

- Compare a list of sites in the browser, with CSV upload: [wecookflow.com](https://wecookflow.com)
- SeoSoup Chrome extension — prices of the site you're on: [wecookflow.com/plugin](https://wecookflow.com/plugin)
- Feedback and feature requests: [wecookflow.com/feedback](https://wecookflow.com/feedback) · hi@wecookflow.com

---

[WeCookFlow](https://wecookflow.com). The server code is not open source; this repository contains the
listing, the Claude Code plugin and the MCP registry metadata. MIT license applies to the files in this repository.
