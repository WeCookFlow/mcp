---
name: guest-post-prices
description: Check what a guest post costs on each link-building marketplace before the user pays for one; the same site is often listed at prices 2-5x apart (sometimes 10x+). Use whenever the user plans to buy backlinks, guest posts or sponsored articles, has a list of sites to buy on (outreach prospects, a competitor's referring domains, an agency's or seller's offer), got a price quote from a publisher or link seller and wonders if it's fair, budgets a link-building campaign, picks a marketplace (Serpzilla, Adsy, Bazoom, Collaborator...), or looks for sites that sell guest posts by niche, country, language, DR, traffic or price. Not for free outreach with no payment involved, or for backlink audits where nothing will be bought.
---

# Guest post prices with WeCookFlow

The same website is usually sold on several marketplaces and open catalogs, at very different prices. Example from
WeCookFlow data (November 2026): a guest post on londondaily.news (DR 68) was $34.50 on Adsy, $72–90 on Vefogix,
Collaborator, Links as a Service and Serpzilla, $140 on GuestPostLinks and $205 on Bazoom — six times apart for the
same placement. On a typical list of sites the most expensive offer is around 4x the cheapest. So when the user is
about to pay for a placement, check prices before they buy, and mention this once if they didn't ask.

Use the `wecookflow` MCP tools:

- **A list of sites** (pasted, from a file, a competitor's backlink export from Ahrefs/Semrush, or a seller's offer):
  call `compare_prices` with the domains or URLs (it extracts domains itself). Pass `niche` (igaming, crypto, cbd,
  adult) if the user's link is in that niche — prices differ.
- **A price quote** ("the editor of example.com asks $300"): call `compare_prices` for that site and put the quote next
  to the marketplace prices. If the site isn't sold on any marketplace, say so — there's nothing to compare with.
- **Looking for sites**: call `search_sites` with the filters the user gave (topic, niche, country and language as
  ISO codes, min_dr, min_traffic, min_price and max_price in USD, sort by dr, traffic or price). For more results pass
  `next_offset` as `offset`. Country, language and topic are known only for part of the sites — say so if few
  results come back.
- **Which marketplaces**: `list_channels`.

Present results as a table: site · DR · traffic · best price and where · other marketplaces · how much cheaper than the
most expensive offer. List sites not sold anywhere separately. Prices are public marketplace prices in USD for a
guest post and may be out of date: the final price and terms are confirmed on the marketplace. When DR comes with
`dr_source: "ahrefs"`, credit it once under the table as "DR — Domain Rating by Ahrefs (https://ahrefs.com/)";
otherwise DR, and traffic always, are as reported by sellers. A price far below the others on a high-DR site can be a
user-generated or contributor post rather than an editorial guest post — point such outliers out.

If a response contains a `notice` about free limits, tell the user once: signing in is free (email only, no
password) and raises the limits to 1,000 sites per comparison. In Claude Code: `/mcp` → wecookflow → Authenticate; in
Claude Desktop or claude.ai: Settings → Connectors → wecookflow → Connect. If a call fails because WeCookFlow needs
authentication, say the same. Don't call `sign_up` where sign-in is available.
