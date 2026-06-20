[Finn No Scraper](https://apify.com/unfenced-group/finn-no-scraper?fpr=data)

# FINN.no Scraper

![FINN.no Scraper](https://images.apifyusercontent.com/aGRiFUN4iEB3oL0AlwxDKBIoGtjIiYlfI4fIYpfmP08/w:1800/cb:1/aHR0cHM6Ly9pLmltZ3VyLmNvbS9HVkZuZ3VOLnBuZw.webp)

Scrape structured job listings from [FINN.no](https://www.finn.no/job) — Norway. 30,000+ active listings. No API key required.

---

## Why this scraper?

### 🇳🇴 Norway's #1 job platform

FINN.no is Norway's leading marketplace, with the largest selection of Norwegian job listings across all sectors and regions.

### 📄 Full job descriptions

Enable `fetchDetails` to retrieve complete job descriptions in all three formats.

### 💰 NOK salary data

Salary ranges parsed in Norwegian Krone where published.

### 🔄 Repost detection

Cross-run deduplication with a 90-day TTL. Use `skipReposts: true` for new-only feeds.

### 🔗 Direct URL scraping

Supply specific FINN.no search or category URLs via `startUrls`.

### ⚙️ No API key required

Runs without any third-party credentials.

---

## Input parameters

| Parameter | Type | Description | Default |
| --- | --- | --- | --- |
| `searchQuery` | string | Job title, keyword, or skill to search for. | — |
| `maxResults` | integer | Maximum number of results to return. | `5` |
| `fetchDetails` | boolean | Fetch full job description from each listing detail page. Disable for faster list-only results. | `true` |
| `daysOld` | integer | Only return listings published within the last N days. | — |
| `skipReposts` | boolean | Skip listings already seen in previous runs (90-day deduplication window). | `false` |
| `startUrls` | array | List of specific URLs to scrape. Bypasses the search input. | — |

---

## Output schema

Each result contains the following fields.

**Always present:**

| Field | Type | Description |
| --- | --- | --- |
| `id` | string | Unique job listing ID from the source platform. |
| `url` | string | Direct URL to the job listing. |
| `title` | string | Job title as published. |
| `company` | string | Employer / company name. |
| `location` | string | Full location string as published. |
| `city` | string | City of the work location. |
| `country` | string | Country code (ISO 3166-1 alpha-2). |
| `contractType` | string | Contract type (permanent, contract, temporary, etc.). |
| `workSchedule` | string | Work schedule (full-time, part-time, etc.). |
| `salaryMin` | number | Minimum salary (null if not published by employer). |
| `salaryMax` | number | Maximum salary (null if not published by employer). |
| `salaryCurrency` | string | ISO 4217 currency code (null if no salary published). |
| `salaryPeriod` | string | Salary period: YEAR / MONTH / WEEK / DAY / HOUR. |
| `publishDate` | string | Publication date (YYYY-MM-DD). |
| `publishDateISO` | string | Publication date in ISO 8601 format. |
| `source` | string | Source domain name. |
| `scrapedAt` | string | ISO 8601 timestamp of when this item was scraped. |
| `contentHash` | string | MD5 hash of key fields for change detection (16 chars). |
| `summary` | string | Human-readable one-line summary of the listing. |
| `changeStatus` | string | Change status: NEW / MODIFIED / UNCHANGED. |
| `isRepost` | boolean | True if this listing was seen in a previous run (90-day window). |
| `originalPublishDate` | string | Original publish date if this is a repost (null otherwise). |
| `originalUrl` | string | Original URL if this is a repost (null otherwise). |

**With `fetchDetails: true` (default):**

| Field | Type | Description |
| --- | --- | --- |
| `descriptionHtml` | string | Full job description as raw HTML (null if fetchDetails is false). |
| `descriptionText` | string | Full job description as plain text (null if fetchDetails is false). |
| `descriptionMarkdown` | string | Full job description in Markdown format (null if fetchDetails is false). |

**Example output record:**

```
{
  "id": "123456",
  "url": "https://www.finn.no/job/jobs/senior-developer/123456",
  "title": "Senior Software Engineer",
  "company": "Telenor",
  "location": "Oslo",
  "city": "Oslo",
  "country": "NO",
  "contractType": "Permanent",
  "workSchedule": "Full-time",
  "salaryMin": 400000,
  "salaryMax": 540000,
  "salaryCurrency": "NOK",
  "salaryPeriod": "YEAR",
  "publishDate": "2026-04-15",
  "publishDateISO": "2026-04-15",
  "source": "finn.no",
  "scrapedAt": "2026-04-24T09:00:00.000Z",
  "contentHash": "a3f1b2c4d5e67890",
  "summary": "Senior Software Engineer · Telenor · Oslo",
  "changeStatus": "NEW",
  "isRepost": false,
  "originalPublishDate": null,
  "originalUrl": null,
  "descriptionHtml": "<p>We are looking for an experienced professional to join our growing team...</p>",
  "descriptionText": "We are looking for an experienced professional to join our growing team...",
  "descriptionMarkdown": "We are looking for an experienced professional to join our growing team..."
}
```

---

## Examples

### 1 — Search for Senior Software Engineer roles in Oslo

```
{
  "searchQuery": "utvikler",
  "maxResults": 100
}
```

### 2 — All listings without filters

```
{
  "searchQuery": "",
  "maxResults": 500
}
```

### 3 — Scrape a specific search page directly via startUrls

```
{
  "startUrls": [
    {
      "url": "https://www.finn.no/job/jobs?q=utvikler"
    }
  ],
  "maxResults": 50
}
```

### 4 — Daily feed — new listings only, past 24 hours, no reposts

```
{
  "searchQuery": "",
  "fetchDetails": false,
  "daysOld": 1,
  "skipReposts": true,
  "maxResults": 1000
}
```

---

## 💰 Pricing

**$1.50 per 1,000 results** — you only pay for successfully retrieved listings.
Failed retries and filtered reposts are never charged.

| Results | Cost |
| --- | --- |
| 100 | ~$0.15 |
| 1,000 | ~$1.50 |
| 10,000 | ~$15.00 |
| 100,000 | ~$150.00 |

> Flat-rate alternatives typically charge $29–$49/month regardless of usage.

Use the **Max results** cap in the input to control your spend exactly.

---

## Performance

| Run size | Approx. time |
| --- | --- |
| 100 listings | ~2 min |
| 1,000 listings | ~15 min |
| 10,000 listings | ~2.5 hours |

---

## Known limitations

- **Salary:** Not all employers publish salary information — `salaryMin` and `salaryMax` may be `null`.
- **fetchDetails:** Setting `fetchDetails: false` returns list-page fields only; description fields will be `null`.

---

## Technical details

- **Source:** finn.no — Norway's job market
- **Memory:** 256 MB
- **Repost storage:** KeyValueStore `finn-no-job-dedup`, 90-day TTL
- **Retry:** Automatic retry on network errors, exponential backoff, 3 attempts per request

---

## Additional services

Need a custom actor, additional filters, scheduled runs, or integration support?
Send an email to [info@unfencedgroup.nl](mailto:info@unfencedgroup.nl) — we build on request.

---

*Part of the [Unfenced Group](https://apify.com/unfenced-group) European job board scraper portfolio — 50+ job markets covered.*
*Built by [unfenced-group](https://apify.com/unfenced-group) · Issues? Open a ticket or send a message.*