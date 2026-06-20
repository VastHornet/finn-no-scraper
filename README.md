[Finn No Scraper](https://apify.com/santamaria-automations/finn-no-scraper?fpr=data)

# Finn.no Scraper

Scrape listings from [finn.no](https://www.finn.no), Norway's largest classifieds platform and job board (Schibsted group). Supports marketplace, jobs, real estate, cars, and mobility.

## How it works

1. Go to [finn.no](https://www.finn.no) and set up your search with all desired filters (category, price, location, make, model, etc.)
2. Copy the URL from your browser
3. Paste it into the **Search URLs** input
4. Run the actor

The actor extracts all listings matching your search, with automatic pagination.

## Use with AI Agents (MCP)

Connect this actor to any MCP-compatible AI client — Claude Desktop, Claude.ai, Cursor, VS Code, LangChain, LlamaIndex, or custom agents.

**Apify MCP server URL:**

```
https://mcp.apify.com?tools=santamaria-automations/finn-no-scraper
```

**Example prompt once connected:**

> "Use `finn-no-scraper` to scrape company data from finn no. Return results as a table."

Clients that support dynamic tool discovery (Claude.ai, VS Code) will receive the full input schema automatically via `add-actor`.

## Features

- **Any filter combination** -- Whatever you can filter on finn.no, the actor can scrape
- **Multiple searches** -- Paste multiple URLs to run several searches in one run
- **Detail enrichment** -- Optionally get full description, company URL, employment type (jobs)
- **All verticals** -- Marketplace (Torget), Jobs (Jobb), Real Estate (Eiendom), Cars (Bil), Mobility
- **Fast & cheap** -- HTTP-only, 128 MB, pay-per-result

## Output

| Field | Description | Source |
| --- | --- | --- |
| `title` | Listing title | Search |
| `price` / `currency` | Price in NOK | Search |
| `location` | City or address | Search |
| `category` | Detected vertical (marketplace/jobs/cars/realestate) | Search |
| `company_name` | Employer (jobs) or seller | Search |
| `company_url` | Employer website | Detail |
| `employment_type` | FULL_TIME, PART_TIME, etc. (jobs) | Detail |
| `image_url` | Primary image URL | Search |
| `description` | Full listing description | Detail |
| `posted_at` / `expires_at` | Publication and expiry dates | Both |
| `source_url` | Direct link on finn.no | Both |

## Pricing

No start fee -- pay only for results:

| Event | Cost |
| --- | --- |
| Listing (basic) | $0.003 |
| Listing (with details) | $0.005 |

**100 listings = $0.30** (basic) or **$0.50** (with details)

## Examples

### Cars under 200K NOK

```
{
  "searchUrls": ["https://www.finn.no/mobility/search/car?price_to=200000&registration_class=1&variant=0.801"],
  "maxResults": 50
}
```

### Multiple searches in one run

```
{
  "searchUrls": [
    "https://www.finn.no/bap/forsale/search.html?q=iphone",
    "https://www.finn.no/job/search?q=utvikler",
    "https://www.finn.no/realestate/homes/search.html?q=leilighet"
  ],
  "maxResults": 200,
  "maxResultsPerQuery": 80
}
```

### Quick SERP-only scan (fast, less data)

```
{
  "searchUrls": ["https://www.finn.no/bap/forsale/search.html?q=macbook"],
  "maxResults": 200,
  "includeDetails": false
}
```

## Related Actors

**European Classifieds**

- [Blocket.se Scraper — Sweden](https://apify.com/santamaria-automations/blocket-se-scraper)
- [DBA.dk Scraper — Denmark](https://apify.com/santamaria-automations/dba-dk-scraper)
- [Tori.fi Scraper — Finland](https://apify.com/santamaria-automations/tori-fi-scraper)
- [Marktplaats.nl Scraper — Netherlands](https://apify.com/santamaria-automations/marktplaats-nl-scraper)
- [Kleinanzeigen.de Scraper — Germany](https://apify.com/santamaria-automations/kleinanzeigen-de-scraper)

**Real Estate**

- [Homegate.ch Scraper — Swiss real estate](https://apify.com/santamaria-automations/homegate-scraper)
- [Immowelt.de Scraper — German real estate](https://apify.com/santamaria-automations/immowelt-de-scraper)

**Enrich your data**

- [Website Email & Phone Scraper](https://apify.com/santamaria-automations/website-email-scraper)
- [Google Maps Scraper](https://apify.com/santamaria-automations/google-maps-scraper)
- [Website Contact Extractor](https://apify.com/santamaria-automations/website-contact-extractor)

## Issues & Feedback

Missing something or not working as expected? [Open an issue](https://console.apify.com/actors/It8xIqTEZKIadyNNr/issues) and we'll fix it.