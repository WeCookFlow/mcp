---
name: guest-post-prices
description: Find where a guest post is cheapest. Use when the user asks about guest post or backlink prices, wants to compare marketplaces (Serpzilla, Adsy, Bazoom, Collaborator…), checks a list of sites or a competitor's referring domains, or looks for sites to buy guest posts on by niche, country, DR, traffic or budget.
---

# Guest post prices with WeCookFlow

Use the `wecookflow` MCP tools:

- **A list of sites** (pasted, from a file, or a competitor's backlink export from Ahrefs/Semrush): call
  `compare_prices` with the domains or URLs (it extracts domains itself). Pass `niche` (igaming, crypto, cbd, adult)
  if the user's link is in that niche — prices differ.
- **Looking for sites**: call `search_sites` with the filters the user gave (topic, niche, country and language as
  ISO codes, min_dr, min_traffic, min_price and max_price in USD, sort by dr, traffic or price). For more results pass
  `next_offset` as `offset`. Country, language and topic are known only for part of the sites — say so if few
  results come back.
- **Which marketplaces**: `list_channels`.

Present results as a table: site · DR · traffic · best price and where · other marketplaces · how much cheaper than the
most expensive offer. List sites not sold anywhere separately. Prices are public marketplace prices in USD for a
guest post and may be out of date. When DR comes with `dr_source: "ahrefs"`, credit it once under the table as
"DR — Domain Rating by Ahrefs (https://ahrefs.com/)"; otherwise DR, and traffic always, are as reported by sellers.

If a response contains a `notice` about free limits, tell the user once. Only if they agree, ask for their email —
never invent one — and call `sign_up(email)`. Then tell them to run `/plugin`, open WeCookFlow settings and paste the
token, or to see https://wecookflow.com/mcp-setup.
