[Crunchbase Scraper](https://apify.com/sovereigntaylor/crunchbase-scraper?fpr=data)

# Crunchbase Company & Funding Scraper

Extract comprehensive company data from Crunchbase — funding rounds, investors, valuations, key people, acquisitions, tech stack, and more. Built for investors, VCs, analysts, and growth teams who need structured startup intelligence at scale.

## Features

- **Full company profiles** — name, description, founded date, HQ, industry, categories, operating status
- **Funding data** — total raised, funding rounds, last round type/amount, investor names, lead investors
- **Key people** — founders, CEO, CTO, board members with titles and LinkedIn URLs
- **Acquisitions** — acquired companies with dates, prices, and types
- **Financial signals** — revenue range, employee count, IPO status, stock exchange/symbol
- **Social links** — website, LinkedIn, Twitter, Facebook, contact email, phone
- **Tech stack** — technologies used by the company
- **Multiple discovery modes** — direct URLs, keyword search, category browse, funding stage filter
- **5 extraction strategies** — **NEXT_DATA** JSON, LD+JSON, inline scripts, meta tags, DOM parsing
- **Anti-bot protection** — 12+ rotating user agents, random delays, Cloudflare detection, rate limit handling
- **Google fallback** — discovers Crunchbase profiles via Google when direct search is blocked
- **Pay-per-event** — charged per company profile scraped ($0.008/company)
- **Proxy support** — residential proxies recommended for large-scale scraping

## Use Cases

### Investor Research & Deal Flow

Monitor startups in specific categories and funding stages. Track Series A companies in AI, fintech, or climate tech. Build a pipeline of investment opportunities with complete funding history and investor networks.

### Competitive Intelligence

Map competitors in your industry with detailed funding, employee count, revenue range, and key hires. Understand who's gaining traction and who's raising capital.

### Market Mapping & Analysis

Build comprehensive market maps by category — how many companies exist in a space, total funding deployed, average round sizes, most active investors. Export structured data for analysis in Excel, Airtable, or any BI tool.

### Lead Generation for B2B Sales

Find companies by category, size, and funding stage for targeted outreach. Extract decision-maker names (CEO, CTO, VP Engineering) with titles for personalized sales campaigns.

### Recruitment Intelligence

Identify fast-growing companies (recent large funding rounds) that are likely hiring. Find key people and their backgrounds. Track executive movements across companies.

### VC Portfolio Analysis

Analyze a VC firm's portfolio by scraping their investments. Compare portfolio companies by funding, growth stage, and category. Identify co-investment patterns.

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `companyUrls` | Array | `[]` | Direct Crunchbase organization URLs to scrape |
| `searchQuery` | String | *(empty)* | Search for companies by name or keyword |
| `category` | String | *(empty)* | Filter by Crunchbase category (e.g., `artificial-intelligence`) |
| `fundingStage` | String | `any` | Filter by funding stage: `seed`, `series_a`, `series_b`, `series_c`, `ipo` |
| `maxResults` | Integer | `200` | Maximum company profiles to scrape (1-5,000) |
| `proxyConfiguration` | Object | *(none)* | Apify proxy settings (residential recommended) |

### Input Examples

#### Scrape specific companies by URL

```
{
    "companyUrls": [
        "https://www.crunchbase.com/organization/openai",
        "https://www.crunchbase.com/organization/stripe",
        "https://www.crunchbase.com/organization/anthropic",
        "https://www.crunchbase.com/organization/figma"
    ],
    "maxResults": 10
}
```

#### Find AI startups at Series A

```
{
    "searchQuery": "artificial intelligence",
    "fundingStage": "series_a",
    "maxResults": 100
}
```

#### Browse fintech companies

```
{
    "searchQuery": "fintech payments",
    "category": "fintech",
    "maxResults": 200
}
```

#### Climate tech companies that went public

```
{
    "searchQuery": "climate technology renewable energy",
    "fundingStage": "ipo",
    "maxResults": 50
}
```

#### Seed-stage cybersecurity startups

```
{
    "searchQuery": "cybersecurity",
    "category": "cybersecurity",
    "fundingStage": "seed",
    "maxResults": 150
}
```

### Common Categories

| Category Slug | Description |
| --- | --- |
| `artificial-intelligence` | AI and machine learning companies |
| `fintech` | Financial technology |
| `health-care` | Healthcare and medtech |
| `e-commerce` | Online retail and marketplaces |
| `saas` | Software as a Service |
| `biotechnology` | Biotech and life sciences |
| `cybersecurity` | Security technology |
| `clean-technology` | Clean energy and sustainability |
| `blockchain` | Blockchain and crypto |
| `edtech` | Education technology |
| `real-estate` | PropTech and real estate |
| `developer-tools` | Developer infrastructure |
| `enterprise-software` | B2B enterprise solutions |
| `robotics` | Robotics and automation |

## Output

Each company profile is saved to the default dataset with comprehensive fields:

```
{
    "name": "OpenAI",
    "legalName": "OpenAI, Inc.",
    "description": "OpenAI is an AI research and deployment company.",
    "longDescription": "OpenAI is an AI research and deployment company dedicated to ensuring that general-purpose artificial intelligence benefits all of humanity...",
    "founded": "2015-12-11",
    "foundedYear": 2015,
    "headquarters": "San Francisco, California, United States",
    "city": "San Francisco",
    "region": "California",
    "country": "US",
    "industry": "Artificial Intelligence",
    "categories": ["Artificial Intelligence", "Machine Learning", "SaaS"],
    "categoryGroups": ["Artificial Intelligence", "Data and Analytics", "Software"],
    "website": "https://openai.com",
    "linkedinUrl": "https://www.linkedin.com/company/openai",
    "twitterUrl": "https://twitter.com/OpenAI",
    "facebookUrl": null,
    "contactEmail": "info@openai.com",
    "fundingTotal": "$11.3B",
    "fundingTotalUsd": 11300000000,
    "fundingRounds": 7,
    "lastFundingRound": "Series Unknown",
    "lastFundingDate": "2024-02-01",
    "lastFundingAmount": 6600000000,
    "investors": ["Microsoft", "Sequoia Capital", "Andreessen Horowitz", "Thrive Capital", "Khosla Ventures"],
    "leadInvestors": ["Microsoft", "Thrive Capital"],
    "numInvestors": 12,
    "employeeCount": "c_01001_05000",
    "employeeCountRange": "1,001-5,000",
    "revenueRange": "$100M+",
    "operatingStatus": "active",
    "ipoStatus": "private",
    "stockExchange": null,
    "stockSymbol": null,
    "acquisitions": [
        {
            "acquireeName": "Global Illumination",
            "announcedDate": "2023-08-16",
            "price": null,
            "type": "acquisition"
        }
    ],
    "keyPeople": [
        { "name": "Sam Altman", "title": "CEO", "linkedinUrl": null },
        { "name": "Greg Brockman", "title": "President", "linkedinUrl": null },
        { "name": "Mira Murati", "title": "CTO", "linkedinUrl": null }
    ],
    "techStack": [],
    "crunchbaseUrl": "https://www.crunchbase.com/organization/openai",
    "crunchbaseSlug": "openai",
    "crunchbaseRank": 15,
    "imageUrl": "https://images.crunchbase.com/image/upload/...",
    "extractionStrategies": ["nextData", "metaTags"],
    "scrapedAt": "2026-03-02T12:00:00.000Z"
}
```

### Output Fields Reference

| Field | Type | Description |
| --- | --- | --- |
| `name` | String | Company name |
| `legalName` | String | Legal entity name |
| `description` | String | Short company description |
| `longDescription` | String | Full company description |
| `founded` | String | Founded date (ISO format) |
| `foundedYear` | Integer | Year founded |
| `headquarters` | String | Full HQ location string |
| `city` / `region` / `country` | String | Location components |
| `industry` | String | Primary industry |
| `categories` | Array | All Crunchbase categories |
| `website` | String | Company website URL |
| `linkedinUrl` / `twitterUrl` / `facebookUrl` | String | Social media links |
| `fundingTotal` | String | Formatted total funding (e.g., "$11.3B") |
| `fundingTotalUsd` | Number | Total funding in USD |
| `fundingRounds` | Integer | Number of funding rounds |
| `lastFundingRound` | String | Latest round type (e.g., "Series B") |
| `lastFundingDate` | String | Date of last funding round |
| `lastFundingAmount` | Number | Amount raised in last round (USD) |
| `investors` | Array | All investor names |
| `leadInvestors` | Array | Lead investor names |
| `employeeCount` | String | Employee count enum or range |
| `revenueRange` | String | Estimated revenue range |
| `ipoStatus` | String | IPO status (private/public) |
| `acquisitions` | Array | Companies acquired (name, date, price) |
| `keyPeople` | Array | Founders, executives, board (name, title) |
| `techStack` | Array | Technologies used |
| `crunchbaseUrl` | String | Crunchbase profile URL |
| `crunchbaseRank` | Integer | Crunchbase rank score |
| `extractionStrategies` | Array | Which parsing strategies yielded data |

## Performance Tips

1. **Use residential proxies** — Crunchbase has aggressive anti-bot protection. Residential proxies are strongly recommended for anything beyond a few companies.
2. **Start with direct URLs** — Providing specific company URLs is the most reliable mode. Search/discovery depends on Google availability.
3. **Keep maxResults reasonable** — Start with 10-50 companies to test, then scale up.
4. **Category + keyword** — Combining a category filter with a search query gives the most targeted results.
5. **Expect partial data** — Crunchbase paywalls some data behind their Pro plan. The scraper extracts everything publicly available.

## Anti-Bot Handling

Crunchbase uses Cloudflare and their own rate limiting. This actor handles it by:

- Rotating through 12+ realistic browser user agents
- Adding random delays (1.5-4 seconds) between requests
- Limiting to 15 requests/minute by default
- Detecting Cloudflare challenges, CAPTCHAs, and rate limit pages
- Falling back to Google search for company discovery
- Using 5 independent extraction strategies (redundancy)
- Retrying blocked requests with exponential backoff

For best results at scale, use Apify **residential proxies** with automatic rotation.

## Pricing (Pay Per Event)

This actor uses Apify's pay-per-event pricing model. You are charged **$0.008 per company profile** successfully scraped and saved to the dataset. No charge for failed extractions or filtered-out companies.

## Legal Notice

This actor is provided as a technical tool for research and analysis. Users are responsible for ensuring their use complies with Crunchbase's Terms of Service and all applicable laws. Crunchbase data is subject to their own licensing terms.

## Integration — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("sovereigntaylor/crunchbase-scraper").call(run_input={
    "searchTerm": "crunchbase",
    "maxResults": 50
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item.get('title', item.get('name', 'N/A'))}")
```

## Integration — JavaScript

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('sovereigntaylor/crunchbase-scraper').call({
    searchTerm: 'crunchbase',
    maxResults: 50
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => console.log(item.title || item.name || 'N/A'));
```