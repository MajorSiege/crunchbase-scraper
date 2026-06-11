[Crunchbase Scraper](https://apify.com/magicfingers/crunchbase-scraper?fpr=data)

Scrape Crunchbase company profiles, funding rounds, founders/executives, and investor data without a Crunchbase Pro subscription.

## What data can you extract?

### Organization profiles

- Name, description, founded date, headquarters location
- Employee count range, operating status, website
- Social links (LinkedIn, Twitter, Facebook)
- Industry categories and category groups
- Total funding raised, last funding type and date
- IPO status, stock symbol, revenue range
- Crunchbase rank

### Funding rounds

- Announced date, funding type (Seed, Series A, etc.)
- Money raised (USD), pre-money valuation
- Lead investors with names and Crunchbase links
- All investors for each round
- Number of investors

### People (founders and executives)

- Name, title, current organization
- LinkedIn and Twitter profiles
- Crunchbase profile URL
- Employment history

### Investor profiles

- Name, type, location, description
- Number of investments, exits, and funds
- Lead investments count
- Portfolio companies list
- Website and social links

## How to use

### Search companies by keyword

```
{
    "action": "searchCompanies",
    "searchQuery": "artificial intelligence",
    "maxResults": 50,
    "includeFunding": true,
    "includePeople": true
}
```

### Search with filters

```
{
    "action": "searchCompanies",
    "searchQuery": "fintech",
    "location": "San Francisco",
    "industryFilter": "Financial Services",
    "fundingStage": "series_a",
    "maxResults": 100
}
```

### Scrape specific company profiles

```
{
    "action": "scrapeProfiles",
    "directUrls": [
        "https://www.crunchbase.com/organization/openai",
        "https://www.crunchbase.com/organization/stripe",
        "https://www.crunchbase.com/organization/anthropic"
    ],
    "includeFunding": true,
    "includePeople": true
}
```

### Scrape investor profiles

```
{
    "action": "scrapeInvestors",
    "directUrls": [
        "https://www.crunchbase.com/organization/sequoia-capital",
        "https://www.crunchbase.com/organization/andreessen-horowitz"
    ]
}
```

### Scrape people profiles

```
{
    "action": "scrapePeople",
    "directUrls": [
        "https://www.crunchbase.com/person/sam-altman",
        "https://www.crunchbase.com/person/elon-musk"
    ]
}
```

## Input parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `action` | string | `searchCompanies` | What to scrape: `searchCompanies`, `scrapeProfiles`, `scrapeInvestors`, `scrapePeople` |
| `searchQuery` | string |  | Keyword to search for |
| `location` | string |  | Filter by HQ location |
| `industryFilter` | string |  | Filter by industry category |
| `fundingStage` | string |  | Filter by last funding stage (seed, series_a, etc.) |
| `directUrls` | array | `[]` | Crunchbase URLs to scrape directly |
| `maxResults` | integer | `100` | Max results (0 = unlimited) |
| `includeFunding` | boolean | `true` | Include funding rounds for profiles |
| `includePeople` | boolean | `true` | Include founders/executives for profiles |
| `includeInvestors` | boolean | `false` | Include detailed investor info |
| `maxConcurrency` | integer | `3` | Parallel pages (lower = safer) |
| `requestTimeout` | integer | `90` | Page load timeout in seconds |
| `proxyConfiguration` | object | Residential | Proxy settings (residential recommended) |

## Output format

Each item in the dataset is a JSON object with a `type` field (`organization`, `investor`, `person`, or `searchResult`).

### Organization example

```
{
    "type": "organization",
    "name": "OpenAI",
    "shortDescription": "OpenAI is an AI research and deployment company.",
    "foundedDate": "2015-12-11",
    "headquartersLocation": "San Francisco, California, United States",
    "website": "https://openai.com",
    "employeeCount": "1001-5000",
    "totalFunding": "$11,300.0M",
    "totalFundingUsd": 11300000000,
    "lastFundingType": "Series Unknown",
    "operatingStatus": "Active",
    "industries": ["Artificial Intelligence", "Machine Learning"],
    "linkedin": "https://www.linkedin.com/company/openai",
    "twitter": "https://twitter.com/OpenAI",
    "fundingRounds": [
        {
            "announcedDate": "2023-04-28",
            "fundingType": "Series Unknown",
            "moneyRaised": 10000000000,
            "leadInvestors": [{ "name": "Microsoft" }],
            "numInvestors": 1
        }
    ],
    "people": [
        {
            "name": "Sam Altman",
            "title": "CEO",
            "linkedin": "https://linkedin.com/in/samaltman"
        }
    ],
    "crunchbaseUrl": "https://www.crunchbase.com/organization/openai",
    "scrapedAt": "2024-01-15T10:30:00.000Z"
}
```

## Pricing

This actor uses pay-per-event pricing: **$2.00 per 1,000 results** ($0.002 per result).

Each saved item (organization profile, investor profile, person profile, or search result) counts as one result.

## Tips for best results

1. **Use residential proxies** — Crunchbase has strong anti-bot detection. Residential proxies are strongly recommended.
2. **Keep concurrency low** — 2-3 concurrent pages reduces blocking risk significantly.
3. **Start with direct URLs** — Scraping specific profile URLs is more reliable than search-based scraping.
4. **Use reasonable limits** — Start with smaller `maxResults` to verify output before large runs.

## Technical details

- Built with Apify SDK v3 and Crawlee PlaywrightCrawler
- Uses response interception to capture Crunchbase's internal API data
- Falls back to DOM extraction when API data is not available
- Extracts JSON-LD and **NEXT_DATA** structured data
- Includes stealth measures (navigator overrides, random delays, human-like scrolling)
- Automatic session rotation and retry logic