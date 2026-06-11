[Crunchbase Scraper](https://apify.com/alizarin_refrigerator-owner/crunchbase-scraper?fpr=data)

# Crunchbase Company Scraper

Scrape company profiles from Crunchbase. Extract funding data, investors, employees, founders, and company details. Perfect for investor research, lead generation, and market analysis. Built by John Rippy ([https://www.linkedin.com/in/johnrippy/](https://www.linkedin.com/in/johnrippy/) | [https://johnrippy.link/](https://johnrippy.link/)).

**BYOK (Bring Your Own Key)** -- you provide your own API credentials.

---

## Before You Start

This actor requires your own API credentials to fetch real data.

**Where to get your key:** JSON array of cookies from Cookie-Editor. Helps bypass Crunchbase paywalls and login gates.

You can test with **Demo Mode** first (free, no key needed) to see the output format before committing.

---

## Quick Start

### Test with Demo Mode (free, no API key needed)

```
{
  "demoMode": true,
  "searchQuery": "AI startup"
}
```

### Run with real data

```
{
  "demoMode": false,
  "searchQuery": "AI startup",
  "maxResults": 50,
  "includeFundingRounds": false,
  "sessionCookies": "YOUR_API_KEY_HERE",
  "webhookPlatform": "custom",
  "cookieKvStoreName": "cookie-sessions"
}
```

---

## Input Parameters

| Parameter | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| `demoMode` | boolean | `true` | No | Run with sample data without making API calls. Great for testing the actor. |
| `searchQuery` | string | - | No | Company name or search term (e.g., 'Stripe', 'AI startup', 'SaaS'). |
| `category` | string | - | No | Filter by industry. |
| `location` | string | - | No | Filter by headquarters location (e.g., 'San Francisco', 'New York'). |
| `fundingStage` | string | - | No | Filter by last funding stage. |
| `minFunding` | string | - | No | Minimum total funding (e.g., '$1M', '$10M', '$100M'). |
| `maxResults` | integer | `50` | No | Maximum number of companies to scrape. |
| `includeFundingRounds` | boolean | `false` | No | Include detailed funding round history (slower but more data). |
| `sessionCookies` | string | - | Yes* | JSON array of cookies from Cookie-Editor. Helps bypass Crunchbase paywalls and login gates. |
| `webhookUrl` | string | - | No | URL to POST results when scraping completes (Zapier, Make, n8n, custom endpoint) |
| `webhookPlatform` | string | `"custom"` | No | Platform type for webhook formatting |
| `webhookHeaders` | object | - | No | Custom HTTP headers to send with webhook (JSON object) |
| `cookieStorageKey` | string | - | No | Key name to load cookies from the Cookie Manager KV store. If set and no manual sessionCookies are provided, the actor loads cookies from the named KV store automatically. Use this with the Cookie Manager actor for automated cookie rotation. |
| `cookieKvStoreName` | string | `"cookie-sessions"` | No | Name of the Apify Key-Value store where Cookie Manager saves cookies. Defaults to 'cookie-sessions' if not set. |

*Required when Demo Mode is off.

---

## Pricing

This actor uses **pay-per-event** billing:

| Event | Description | Price |
| --- | --- | --- |
| Company Scraped | Each company profile scraped from Crunchbase | $0.08 |

**Demo mode is free** -- no charges for sample data.

---

## Troubleshooting

### "API key is required"

You have Demo Mode turned **off** but didn't provide an API key. Either:

- Turn Demo Mode **on** to test with sample data
- Add your API key in the input

### "API error 403" or "Unauthorized"

Your API key is invalid, expired, or doesn't have access to this specific API endpoint. Double-check your key and account permissions.

### "API error 429" or "Rate limit"

Too many requests. Wait a minute and try again, or reduce the number of items per run.

### No results or empty dataset

Check the run log for error messages. Common causes:

- Invalid input format (check the examples above)
- API key without proper permissions
- The target data doesn't exist or is too small to track

### How do I test without an API key?

Enable **Demo Mode** in the input. This returns realistic sample data so you can verify the output format works for your workflow.

---

**Built by John Rippy | [Actor Arsenal](https://actorarsenal.com)**