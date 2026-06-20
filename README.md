[Finn No Scraper](https://apify.com/logiover/finn-no-scraper?fpr=data)

# 🇳🇴 Finn.no Scraper — Real Estate, Cars, Jobs & Marketplace Norway

Extract listings from **[Finn.no](https://www.finn.no)** — Norway's largest classified ads platform, used by **4 million Norwegians every month** (75% of the population). Scrape real estate for sale, used cars, job postings, and marketplace items across all Norwegian regions — with prices, GPS coordinates, photos, agent details and more.

Finn.no publishes **35,000+ new listings every day** across 10+ categories. This scraper taps directly into Finn.no's internal JSON APIs to deliver fast, structured, complete data — no HTML parsing, no proxies required for standard use.

---

## 🔍 What can you scrape?

| Category | Input value | Description |
| --- | --- | --- |
| 🏠 Real Estate | `realestate/homes` | Homes, apartments, cabins for sale |
| 🚗 Used Cars | `car/used` | All used vehicles across Norway |
| 💼 Jobs | `job/fulltime` | Full-time job postings |
| 🛋️ Marketplace | `bap/forsale` | Second-hand goods for sale |

---

## 💡 Use cases

**Real Estate**

- Track property prices across Oslo, Bergen, Trondheim and all 356 Norwegian municipalities
- Monitor price-per-m², total price (Totalpris) and monthly fees (Felleskostnader) to calculate rental yield
- Build automated property alerts for specific areas, price ranges and property types
- Aggregate agent and broker contact data for lead generation
- Feed property data into valuation models and investment analysis tools

**Cars**

- Build Norwegian used car valuation tools with real market data
- Monitor price trends for specific makes, models and years
- Track dealer inventory and private listings simultaneously
- Compare EV vs combustion pricing, range and dealer segments
- Competitive intelligence for car dealerships

**Jobs**

- Analyse Norwegian labour market trends and hiring patterns
- Track which companies are actively recruiting and in which regions
- Monitor demand for specific skills and roles over time
- Build job alert tools for recruiters and candidates
- Generate datasets for salary benchmarking and market research

**Marketplace**

- Price monitoring for second-hand consumer goods
- Brand presence analysis (who sells what and at what price)
- Build recommendation engines for resale platforms
- AI training data with Norwegian-language product descriptions

---

## 📦 Output fields

### 🏠 Real Estate

| Field | Description | Example |
| --- | --- | --- |
| `finnkode` | Unique listing ID | `"455772354"` |
| `url` | Full listing URL | `"https://www.finn.no/realestate/..."` |
| `adType` | Listing subtype | `"realestate"` / `"realestate_project"` |
| `title` | Full listing headline | `"Lys 3-roms med balkong og heis"` |
| `location` | Full address | `"Smedstuvegen 3, Nannestad"` |
| `localAreaName` | Neighbourhood name | `"Majorstuen"` |
| `price` | Asking price (NOK) | `"4 200 000 kr"` |
| `totalPrice` | Total price incl. shared debt | `"4 658 367 kr"` |
| `monthlyFee` | Monthly shared costs | `"5 506 kr"` |
| `size` | Floor area | `"61 m²"` |
| `plotSize` | Land/plot size | `"6 987 m²"` |
| `ownershipType` | Eier / Andel / Aksje | `"Eier (Selveier)"` |
| `propertyType` | Property category | `"Leilighet"` / `"Enebolig"` |
| `bedrooms` | Number of bedrooms | `"2"` |
| `viewingDate` | Open house schedule | `"22. mars 2026, 12:00"` |
| `agent` | Broker/agency name | `"DNB Eiendom AS"` |
| `agentLogoUrl` | Agent logo image URL | `"https://images.finncdn.no/..."` |
| `imageUrl` | Cover photo URL | `"https://images.finncdn.no/..."` |
| `imageUrls` | All photos (comma-separated) | `"url1, url2, url3"` |
| `lat` / `lng` | GPS coordinates | `"59.92119"` / `"10.815"` |

### 🚗 Cars

| Field | Description | Example |
| --- | --- | --- |
| `title` | Make and model | `"BMW i4"` |
| `price` | Asking price | `"509 000 kr"` |
| `make` | Car brand | `"BMW"` |
| `model` | Model name | `"i4"` |
| `modelSpec` | Full specification string | `"M50 Supercharged, H/K, Soltak, Laser"` |
| `year` | Model year | `"2023"` |
| `mileage` | Odometer reading | `"63 000 km"` |
| `fuelType` | Fuel/powertrain type | `"El"` / `"Diesel"` / `"Plug-in Bensin"` |
| `gearbox` | Transmission type | `"Automat"` / `"Manuell"` |
| `drivingRange` | Electric range | `"510 km"` |
| `dealerSegment` | Seller type | `"Merkeforhandler"` / `"Privat"` |
| `dealer` | Dealer name | `"Bilia Skøyen"` |
| `warranty` | Remaining warranty | `"24 mnd"` |
| `lat` / `lng` | GPS coordinates | `"59.91825"` / `"10.66111"` |

### 💼 Jobs

| Field | Description | Example |
| --- | --- | --- |
| `title` | Job title | `"Senior Backend utvikler"` |
| `heading` | Full ad headline | `"Vil du jobbe hos oss?"` |
| `company` | Employer name | `"Telenor Norge"` |
| `location` | City | `"Trondheim"` |
| `locations` | Full breadcrumb | `"Norge, Trøndelag, Trondheim"` |
| `noOfPositions` | Open positions | `"3"` |
| `publishedAt` | Publication timestamp | `"2026-03-05T13:50:05.000Z"` |
| `deadline` | Application deadline | `"2026-04-06T21:59:59.999Z"` |
| `lat` / `lng` | GPS coordinates | `"63.42207"` / `"10.43776"` |

### 🛋️ Marketplace (BAP)

| Field | Description | Example |
| --- | --- | --- |
| `title` | Item name | `"Smedstorp sofa fra IKEA"` |
| `price` | Asking price | `"4 500 kr"` |
| `brand` | Product brand | `"IKEA"` / `"Skeidar"` |
| `tradeType` | Sale type | `"Til salgs"` / `"Gis bort"` |
| `sellerType` | Seller type | `"Privat"` |
| `publishedAt` | Listing timestamp | `"2026-03-16T15:32:49.000Z"` |
| `imageUrls` | All photos | `"url1, url2, url3"` |
| `lat` / `lng` | GPS coordinates | `"59.9218"` / `"10.7757"` |

---

## ⚙️ Input options

### Basic — scrape by category

```
{
  "category": "realestate/homes",
  "maxResults": 100,
  "proxyConfiguration": { "useApifyProxy": true }
}
```

### With keyword search

```
{
  "category": "realestate/homes",
  "searchQuery": "3 soverom balkong",
  "maxResults": 50,
  "proxyConfiguration": { "useApifyProxy": true }
}
```

### Filter by city (Oslo)

```
{
  "category": "car/used",
  "searchQuery": "BMW",
  "location": "0.20061",
  "maxResults": 200,
  "proxyConfiguration": { "useApifyProxy": true }
}
```

### Jobs search

```
{
  "category": "job/fulltime",
  "searchQuery": "developer",
  "location": "0.20061",
  "maxResults": 100,
  "proxyConfiguration": { "useApifyProxy": true }
}
```

### Marketplace search

```
{
  "category": "bap/forsale",
  "searchQuery": "sofa",
  "maxResults": 50,
  "proxyConfiguration": { "useApifyProxy": true }
}
```

---

## 🏙️ Location IDs

Use these in the `location` field to filter by city:

| City | Location ID |
| --- | --- |
| Oslo | `0.20061` |
| Bergen | `0.20007` |
| Trondheim | `0.20012` |
| Stavanger | `0.20011` |
| Tromsø | `0.20019` |
| Kristiansand | `0.20009` |
| Drammen | `0.20032` |
| Fredrikstad | `0.20001` |

For any other location, open Finn.no, search with the city filter applied, and copy the `location=` value from the URL.

---

## 📊 Sample output — Real Estate

```
{
  "finnkode": "455808561",
  "url": "https://www.finn.no/realestate/homes/ad.html?finnkode=455808561",
  "adType": "realestate",
  "title": "Lys og gjennomgående 3-roms med solrik balkong",
  "location": "Jacob Aalls gate 3C, Oslo",
  "localAreaName": "Majorstuen",
  "price": "9 450 000 kr",
  "totalPrice": "9 744 733 kr",
  "monthlyFee": "5 580 kr",
  "size": "76 m²",
  "plotSize": "951 m²",
  "ownershipType": "Eier (Selveier)",
  "propertyType": "Leilighet",
  "bedrooms": "2",
  "viewingDate": "22. mars 2026, 12:00, 23. mars 2026, 16:00",
  "agent": "PrivatMegleren Dyve & Partnere",
  "imageUrl": "https://images.finncdn.no/dynamic/default/2026/3/...",
  "imageUrls": "https://images.finncdn.no/..., https://images.finncdn.no/...",
  "lat": "59.92552",
  "lng": "10.71305",
  "scrapedAt": "2026-03-16T15:43:06.025Z"
}
```

## 📊 Sample output — Car

```
{
  "finnkode": "455806676",
  "url": "https://www.finn.no/mobility/item/455806676",
  "adType": "car/used",
  "title": "BMW i5",
  "location": "Fredrikstad",
  "price": "728 500 kr",
  "make": "BMW",
  "model": "i5",
  "modelSpec": "xDrive40, Fully Ch, M-Sport Pro, Pano, Bower & W",
  "year": "2025",
  "mileage": "9 900 km",
  "fuelType": "El",
  "gearbox": "Automat",
  "drivingRange": "513 km",
  "dealerSegment": "Merkeforhandler",
  "dealer": "Sulland Fredrikstad BMW",
  "warranty": "56 mnd",
  "lat": "59.24063",
  "lng": "10.98364",
  "scrapedAt": "2026-03-16T15:43:41.399Z"
}
```

---

## 💰 Pricing

| Volume | Estimated cost |
| --- | --- |
| 100 listings | ~$0.50 |
| 500 listings | ~$2.50 |
| 1,000 listings | ~$5.00 |
| 10,000 listings | ~$50.00 |
| 100,000 listings | ~$500.00 |

| Tier | Price per result |
| --- | --- |
| Default | $0.005 |
| Bronze | $0.0045 |
| Silver | $0.004 |
| Gold | $0.0035 |

---

## ⚡ Performance

- **JSON API** — direct structured data, no browser, no HTML parsing
- **~200–400 listings/minute** depending on category and proxy
- **Automatic pagination** — follows all result pages up to `maxResults`
- **Deduplication** — each listing saved once across pages
- **400ms delay** between pages — polite, stable, avoids rate limiting

---

## 🔒 Proxy usage

Finn.no is accessible without proxies for light use. For scraping thousands of listings, Apify's built-in proxy pool is recommended to maintain consistent access. Keep `"useApifyProxy": true` in the proxy configuration (default setting).

---

## ❓ FAQ

**How large is Finn.no?**

Finn.no is Norway's largest marketplace, with over 1.5 million active listings at any time, 35,000+ new listings added daily, and 4 million unique monthly users — roughly 75% of the Norwegian population.

**Does this work for all Norwegian regions?**

Yes. Leave `location` blank to scrape all of Norway, or add a location ID to target a specific city or region.

**What is Totalpris?**

Total price including any shared debt (fellesgjeld) in co-operative housing. This is the true cost to the buyer and is mandatory in Norwegian property listings.

**What is Felleskostnader / Monthly Fee?**

Monthly shared building costs for co-operative (Andel) or share (Aksje) apartments — covering maintenance, insurance, and sometimes heating. Critical for calculating total ownership cost.

**What do Eier / Andel / Aksje mean?**

Norwegian property ownership types. Eier (Selveier) = freehold — you own the property outright. Andel = co-operative share (Borettslag). Aksje = share in a housing company (Aksjeleilighet). Andel and Aksje properties carry shared debt and monthly fees.

**What does dealerSegment mean for cars?**

Merkeforhandler = authorised brand dealer. Forhandler = used car dealer. Privat = private seller.

**What is drivingRange for electric cars?**

The official WLTP-rated range in kilometres for electric and plug-in hybrid vehicles.

**Can I scrape jobs in a specific industry?**

Yes — use `searchQuery` with keywords like `"developer"`, `"sykepleier"` (nurse), `"leder"` (manager), etc. Combine with `location` to target specific cities.

**Is scraping Finn.no legal?**

This scraper collects publicly available listing data visible to any website visitor without login. Always use the data responsibly and in compliance with applicable laws in your jurisdiction.