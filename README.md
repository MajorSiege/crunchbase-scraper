[Crunchbase Scraper](https://apify.com/apivault_labs/crunchbase-scraper?fpr=data)

# 🏢 Crunchbase Company Scraper

Extract **email, phone, website, industry, location, and funding data** from public Crunchbase company profiles — in real time.

No API key, no login, no cookies. Just paste Crunchbase URLs and get structured B2B data.

## Why This Scraper?

- **Contact data** — email + phone extracted directly from Crunchbase profiles
- **Real-time** — scrapes live pages, not a stale database
- **Configurable** — toggle exactly which fields you need
- **Bulk ready** — process hundreds of companies in parallel
- **Cheap** — $4 per 1,000 companies ($0.004 each)

## Output Fields

| Field | Example |
| --- | --- |
| Company Name | OpenAI |
| Description | AI research and deployment company... |
| Location | San Francisco, California, United States |
| Industry | Artificial Intelligence, SaaS, Machine Learning |
| Email | [support@openai.com](mailto:support@openai.com) |
| Phone | +1 800-242-8478 |
| Website | [https://www.openai.com](https://www.openai.com) |
| Crunchbase URL | [https://www.crunchbase.com/organization/openai](https://www.crunchbase.com/organization/openai) |
| Extra Metadata | Growth Score, Heat Score, Employees, Founders, Stock |

## Use Cases

- **B2B Lead Generation** — find company emails and phones at scale
- **Market Research** — map industries, locations, company sizes
- **Sales Prospecting** — enrich CRM with Crunchbase data
- **Competitive Analysis** — track competitors' funding and growth
- **Investor Research** — analyze startup ecosystems

## Input Example

```
{
  "profileUrls": [
    "https://www.crunchbase.com/organization/openai",
    "https://www.crunchbase.com/organization/stripe",
    "https://www.crunchbase.com/organization/airbnb"
  ],
  "maxConcurrency": 5,
  "timeout": 120
}
```

## Output Example

```
{
  "success": true,
  "inputUrl": "https://www.crunchbase.com/organization/openai",
  "companyName": "OpenAI",
  "description": "OpenAI is an AI research and deployment company...",
  "location": "San Francisco, California, United States",
  "industry": "Agentic AI, Artificial Intelligence, SaaS, Machine Learning",
  "email": "support@openai.com",
  "phoneNumber": "+1 800-242-8478",
  "website": "https://www.openai.com",
  "crunchbaseUrl": "https://www.crunchbase.com/organization/openai",
  "otherMetadata": "Growth Score: 94, Heat Score: 85, Employees: 1001-5000"
}
```

## Pricing

- **$4 per 1,000 results** ($0.004 per company)
- Platform fee: $0.00005 per start

## Field Selection

All fields enabled by default. Disable any you don't need:

- Company Name, Description, Location
- Industry / Categories
- Email, Phone Number, Website
- Crunchbase URL
- Extra Metadata (funding, employees, founders, scores)