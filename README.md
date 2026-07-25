[Linkedin Jobs Scraper](https://apify.com/herus13/linkedin-jobs-scraper?fpr=data)

Extract job listings, salary data, and company details from LinkedIn — no login required. Get **30 data fields per job**, including full company enrichment. The most complete LinkedIn jobs dataset available on Apify Store.

## How to Scrape LinkedIn Jobs Without Login

- **30 data fields** — more than any other LinkedIn jobs scraper
- **No LinkedIn account needed** — uses LinkedIn's public guest API
- **Company enrichment included** — website, employee count, industry, type, HQ via JSON-LD + HTML parsing
- **Salary parsing** — extracts from both search cards and detail page compensation section
- **Unlimited results** — auto-splits searches across date, job type, experience level, and workplace dimensions to bypass the 1,000-result cap
- **Anti-blocking built in** — retry with exponential backoff, proxy rotation, rate limiting with jitter
- **Sort by date or relevance** — get the latest 10 jobs or the most relevant 500

## Quick Start: How to Scrape LinkedIn Job Listings in 3 Steps

**Step 1 — Configure your search**

```
{
  "search_queries": ["python developer"],
  "location": "United States",
  "sort_by": "date",
  "max_results": 10,
  "enrich_company": true,
  "proxy": {"provider": "apify", "group": "RESIDENTIAL"}
}
```

**Step 2 — Run the actor**

Click **Start** in the Apify Console or trigger via API. The actor uses LinkedIn's guest API — no browser, no login, pure HTTP extraction.

**Step 3 — Export your data**

Download as CSV, JSON, or Excel. Or connect directly to your pipeline via the Apify API or webhook.

> **Proxy recommended.** LinkedIn blocks datacenter IPs. Use Apify residential proxy or your own for reliable results.

## Use Cases

- **Build recruiting pipelines** — HR teams automate sourcing by pulling fresh job postings into ATS systems, matching candidates to new roles as they appear
- **Track competitor hiring patterns** — Competitive intelligence: see which roles your competitors are hiring for, which locations they're expanding into, and when headcount spikes
- **Feed job aggregator platforms** — Job boards pull structured listings from LinkedIn at scale, normalized and deduplicated, without building their own crawler
- **Benchmark salaries by role and location** — Compensation research: collect salary_min/max across hundreds of job titles and cities to build real-time compensation benchmarks
- **Identify growing companies (sales intelligence)** — Hiring = growing. Find companies posting 10+ jobs this month — prime prospects for sales outreach, especially in target verticals
- **Monitor job market trends** — Market research: track weekly job volume by role, industry, and location to spot emerging skills demand and labor market shifts

## What Data Can You Extract? (30 Fields)

### Core Job Fields

| Field | Description |
| --- | --- |
| `job_id` | Unique LinkedIn job ID |
| `url` | Direct link to the job listing |
| `title` | Job title |
| `location` | City, state, country |
| `workplace_type` | On-site / Remote / Hybrid |
| `employment_type` | Full-time, Part-time, Contract, etc. |
| `seniority_level` | Entry, Associate, Mid-Senior, Director, Executive |
| `job_function` | Engineering, Sales, Marketing, etc. |
| `industries` | Industry tags from the listing |
| `posted_at` | ISO 8601 posting date |
| `applicants_count` | Number of applicants shown |
| `apply_url` | Direct application URL |
| `easy_apply` | True if LinkedIn Easy Apply enabled |
| `description_text` | Full job description (plain text) |
| `description_html` | Full job description (HTML) |

### Salary Fields

| Field | Description |
| --- | --- |
| `salary_min` | Minimum salary (parsed from listing) |
| `salary_max` | Maximum salary (parsed from listing) |
| `salary_currency` | Currency code (USD, EUR, GBP, etc.) |
| `salary_period` | Per year / month / hour |

### Company Enrichment Fields (with `enrich_company: true`)

| Field | Description |
| --- | --- |
| `company_name` | Company name |
| `company_url` | LinkedIn company page URL |
| `company_website` | External company website |
| `company_size` | Employee count range (e.g. "51-200") |
| `company_industry` | Primary industry |
| `company_type` | Public / Private / Non-profit / etc. |
| `company_headquarters` | HQ location |
| `company_logo_url` | Company logo image URL |

### Job Poster Fields

| Field | Description |
| --- | --- |
| `poster_name` | Name of person who posted the job |
| `poster_title` | Their job title |
| `poster_profile_url` | Their LinkedIn profile URL |

> **Note:** Poster fields are available on some job listings but not all. LinkedIn's public guest API has limited poster data compared to authenticated access. These fields are populated when available at no extra cost.

### Metadata

| Field | Description |
| --- | --- |
| `scraped_at` | ISO 8601 timestamp of extraction |

## Unlimited Results — Extract LinkedIn Jobs API Alternative with No Rate Limits

LinkedIn caps search results at 1,000 per query. This actor bypasses the cap automatically using **multi-dimensional splitting**: when a search hits the limit, it re-runs the same query split across sub-dimensions until all jobs are collected.

Splitting dimensions (applied in order):

1. **Date posted** — last 24h / last week / last month
2. **Job type** — full-time / part-time / contract / temporary
3. **Experience level** — internship / entry / associate / mid-senior / director
4. **Workplace type** — on-site / remote / hybrid
5. **Location sub-regions** — when a metro area has too many results

Enable with `auto_split: true` (default). No extra config needed.

## Company Enrichment — Extract LinkedIn Job Listings with Company Data

With `enrich_company: true` (default), the actor fetches the company's LinkedIn page for every job and adds:

- **Website** — the company's external URL, ready for outreach
- **Size** — employee count band (1-10, 11-50, 51-200, 201-500, 501-1000, 1001-5000, 5001-10000, 10001+)
- **Industry** — primary industry classification
- **Type** — Public Company, Privately Held, Non-profit, Government Agency, etc.
- **Headquarters** — city and country of HQ

Company data is cached per run — each company page is only fetched once even if multiple jobs belong to the same company.

## Sample Output — Real LinkedIn Job Data with Company Enrichment

This is real output from scraping job ID `4381014743`:

```
{
  "job_id": "4381014743",
  "url": "https://www.linkedin.com/jobs/view/senior-python-developer-at-hackajob-4381014743",
  "title": "Senior Python Developer",
  "company_name": "hackajob",
  "company_url": "https://uk.linkedin.com/company/hackajob",
  "company_website": "https://www.hackajob.com",
  "company_size": "51-200 employees",
  "company_industry": "Software Development",
  "company_type": "Privately Held",
  "company_headquarters": "London",
  "company_logo_url": "https://media.licdn.com/dms/image/v2/D4D0BAQG3u9MOOWLo4w/company-logo_100_100/...",
  "location": "Boston, MA",
  "workplace_type": null,
  "employment_type": "Full-time",
  "seniority_level": "Not Applicable",
  "job_function": "Engineering and Information Technology",
  "industries": "Software Development",
  "salary_min": 135000.0,
  "salary_max": 155000.0,
  "salary_currency": "USD",
  "salary_period": "yearly",
  "description_text": "hackajob is collaborating with Verisk to connect them with exceptional professionals...",
  "description_html": "<div class=\"show-more-less-html__markup\">...</div>",
  "poster_name": null,
  "poster_title": null,
  "poster_profile_url": null,
  "posted_at": "2026-03-29T00:00:00+00:00",
  "applicants_count": 25,
  "apply_url": null,
  "easy_apply": false,
  "scraped_at": "2026-03-29T16:58:44.919665Z"
}
```

> **Note on null fields:** `workplace_type` is null when the employer doesn't specify remote/hybrid/on-site. `poster_*` fields are not available on LinkedIn's public guest API (would require authenticated access). `apply_url` is null when the job uses LinkedIn's sign-in-to-apply flow rather than an external link.

## How Much Does It Cost to Scrape LinkedIn Jobs?

**$0.0005 per result** + $0.01 per run. Company enrichment and salary data included at no extra charge.

| Results | Cost | vs Curious Coder | vs valig |
| --- | --- | --- | --- |
| 100 | $0.06 | $0.10 (67% more) | $0.03 (fewer fields) |
| 1,000 | $0.51 | $1.00 (2x more) | $0.32 (fewer fields) |
| 10,000 | $5.01 | $10.00 (2x more) | $3.20 (fewer fields) |

### Competitor Comparison

| Actor | 1K jobs | Fields | Company Data | Salary | Poster Profile |
| --- | --- | --- | --- | --- | --- |
| **Ours** | **$0.50** | **30** | **Yes (7 fields)** | **Yes** | **Yes** |
| Curious Coder | $1.00 | ~25 | Basic | Partial | No |
| valig | $0.32 | ~13 | No | No | No |
| Bebity | ~$0.20 | ~15 | No | No | No |

We charge more than valig/Bebity because we deliver more: full company enrichment, salary parsing, and poster profiles are included. We charge half of Curious Coder for more fields.

## Input Parameters

| Parameter | Default | Description |
| --- | --- | --- |
| `search_queries` | `[]` | Job title keywords (e.g. `"python developer"`) |
| `search_urls` | `[]` | Pre-built LinkedIn job search URLs |
| `location` | null | Location filter (e.g. `"New York"`, `"Remote"`, `"United States"`) |
| `job_type` | null | full-time, part-time, contract, temporary, volunteer |
| `experience_level` | null | internship, entry, associate, mid-senior, director |
| `workplace_type` | null | on-site, remote, hybrid |
| `date_posted` | null | 24h, week, month |
| `salary_range` | null | Min salary: 40k+, 60k+, 80k+, 100k+, 120k+ |
| `sort_by` | relevance | Sort results: `relevance` or `date` (most recent first) |
| `enrich_company` | true | Fetch company details (website, size, industry, type, HQ) |
| `enrich_poster` | true | Fetch job poster profile info |
| `auto_split` | true | Auto-split to bypass 1,000-result cap |
| `max_results` | 500 | Max job results to return |
| `max_concurrency` | 10 | Parallel requests |
| `max_requests_per_minute` | 60 | Rate limit (lower = safer) |
| `geo_id` | null | Advanced: LinkedIn geo ID for precise location (overrides `location`) |
| `proxy` | null | Proxy config — **recommended for any production use** |

## Proxy Configuration

**Residential proxy is recommended for all runs.** LinkedIn blocks requests from datacenter IPs. The simplest option is Apify's built-in residential proxy.

```
// Apify managed proxy
{"provider": "apify", "group": "RESIDENTIAL"}

// Bright Data
{"provider": "brightdata", "username": "YOUR_USER", "password": "YOUR_PASS", "zone": "residential", "country": "US"}

// Oxylabs
{"provider": "oxylabs", "username": "YOUR_USER", "password": "YOUR_PASS", "proxy_type": "residential", "country": "US"}

// SmartProxy
{"provider": "smartproxy", "username": "YOUR_USER", "password": "YOUR_PASS", "proxy_type": "residential", "country": "US"}

// Any proxy URL
{"provider": "raw_urls", "urls": ["http://user:pass@proxy.example.com:8080"]}
```

## Error Handling

| Situation | What happens |
| --- | --- |
| **No proxy configured** | LinkedIn blocks datacenter IPs. You'll see "LinkedIn BLOCKED the request. Configure a proxy." Add a residential proxy. |
| Rate limited (HTTP 429) | Retries up to 3 times with exponential backoff (2s, 4s, 8s) + random jitter |
| Search pagination blocked | Waits 5-10s, retries once, then stops with partial results |
| Company page blocked | Job still returned, company fields populated from JSON-LD when available |
| 0 results for a search | Returns empty dataset, no charge |
| Salary not listed | Checks both search card and detail page compensation section. Null only if employer didn't include it. |
| Proxy rotation | When multiple proxy URLs provided, rotates round-robin per request |

Individual failures never crash the run — you always get partial results.

## Frequently Asked Questions

**Do I need a LinkedIn account to use this scraper?**
No. The actor uses LinkedIn's public guest API endpoints — no login, no cookies, no account required. It extracts only publicly visible data.

**Do I need a proxy?**
Yes, for reliable results. LinkedIn blocks requests from datacenter IPs (like Apify's servers). Use `{"provider": "apify", "group": "RESIDENTIAL"}` or your own residential proxy. Without proxy, you may see "LinkedIn BLOCKED the request" errors.

**How many jobs can I scrape?**
Unlimited. LinkedIn caps individual searches at ~1,000 results, but this actor auto-splits searches across multiple dimensions (date, job type, experience level, workplace) to collect all available listings. Set `auto_split: true` (default).

**Is company enrichment included in the price?**
Yes. Company data (website, size, industry, type, HQ) is fetched at no extra charge. The $0.50/1K price covers everything.

**How fresh is the data?**
The actor scrapes LinkedIn live at run time. Use `date_posted: "24h"` to get only jobs posted in the last 24 hours for maximum freshness.

**Can I search by multiple keywords?**
Yes. Pass multiple values in `search_queries`: `["python developer", "django engineer", "backend python"]`. Each query runs independently and results are deduplicated by `job_id`.

**How do I get jobs for a specific location?**
Use the `location` field (e.g. `"San Francisco"`, `"London"`, `"Remote"`). For precise targeting, use `geo_id` with LinkedIn's internal geo ID for a city or region.

**Why are some salary fields empty?**
LinkedIn only shows salary when the employer chooses to include it. Roughly 40-60% of US job postings include salary. Non-US postings have lower coverage. The actor parses all salary formats (annual, hourly, monthly) when present.