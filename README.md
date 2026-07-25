[Linkedin Jobs Scraper](https://apify.com/thirdwatch/linkedin-jobs-scraper?fpr=data)

# LinkedIn Jobs Scraper

> Hiring-intent and buying-signal data at scale: scrape public LinkedIn jobs for titles, companies, parsed salary, skills, descriptions, and apply links across 20+ countries — no LinkedIn account, no API key.

## What you get

LinkedIn hosts 20M+ active job postings across 200+ countries — every one of them is a buying signal. A company hiring a "Salesforce Admin" is a Salesforce customer; a company posting 10 backend roles in 30 days is in growth mode and buying tooling. This scraper returns titles, companies, locations, parsed salary ranges (min/max/currency/period), skills, experience levels, job type, full descriptions, applicant counts, and direct apply links. No LinkedIn account needed, no API key.

## LinkedIn Jobs API alternative for hiring intelligence

LinkedIn does not publish a public Jobs API. B2B sellers and RevOps teams use this actor as the structured-data alternative for tracking hiring intent: which companies are hiring for your ICP's tech stack, which competitors are scaling specific functions, and which accounts just opened 5+ new headcount in your target segment. The `skills`, `description`, and `company_name` fields are the load-bearing ones for buying-signal pipelines — they let you match job posts to product categories (e.g. "hiring SDR" → outbound tooling buyer; "hiring Snowflake engineer" → data-stack buyer).

## Map company hiring trends from job postings

Filter by `companyName` to track competitor or target-account hiring velocity over time: how many roles, which functions, what locations, what experience levels. Combine with the LinkedIn Company Employees Scraper to size the team, then use this actor to size the *delta* — net new headcount as a leading indicator for funding rounds, market expansion, and buying intent. Recruiters use the same data as a sourcing-intelligence layer (where talent is flowing to/from) and investors use it as a portfolio-monitoring signal.

## Output fields

| Field | Description |
| --- | --- |
| `title` | Job title |
| `company_name` | Hiring company |
| `location` | Job location |
| `salary_raw` | Salary as displayed |
| `salary_min` | Parsed minimum salary |
| `salary_max` | Parsed maximum salary |
| `salary_currency` | Currency code |
| `salary_period` | Pay period (yearly, monthly, hourly) |
| `experience_level` | Required experience level |
| `job_type` | Full-time, Part-time, Contract, etc. |
| `industry` | Company industry |
| `skills` | Required skills (Standard and Full modes) |
| `description` | Full job description (Standard and Full modes) |
| `applicant_count` | Number of applicants |
| `is_easy_apply` | Whether Easy Apply is available |
| `posted_at` | Posting date |
| `apply_url` | LinkedIn job URL |

## Example output

```
{
    "title": "Software Engineer",
    "company_name": "Google",
    "location": "San Francisco, CA",
    "salary_raw": "$150,000 - $200,000/yr",
    "salary_min": 150000,
    "salary_max": 200000,
    "salary_currency": "USD",
    "salary_period": "yearly",
    "experience_level": "Mid-Senior level",
    "job_type": "Full-time",
    "industry": "Technology, Information and Internet",
    "skills": ["Python", "Java", "AWS"],
    "description": "We are looking for a talented Software Engineer to join...",
    "applicant_count": "200+ applicants",
    "is_easy_apply": true,
    "posted_at": "2026-04-05",
    "apply_url": "https://www.linkedin.com/jobs/view/123456/"
}
```

## Input parameters

| Parameter | Required | Description |
| --- | --- | --- |
| `queries` | Yes | Job search keywords (e.g., `["software engineer", "data scientist"]`). Each query runs a separate LinkedIn search. |
| `location` | No | City or country (e.g., `"San Francisco"`, `"London"`, `"Bangalore"`, `"India"`). Leave empty for worldwide. |
| `country` | No | Country filter: United States, United Kingdom, India, Canada, Australia, Germany, France, Netherlands, Singapore, UAE, Japan, Brazil, Ireland, Sweden, Switzerland, Spain, Italy, Israel, South Korea, Mexico. Leave empty to use the `location` field instead. |
| `companyName` | No | Limit results to a specific company (e.g., `"Google"`, `"Netflix"`). |
| `maxResultsPerQuery` | No | Max jobs per query. Default `5` (start small to preview cost; raise for larger runs). LinkedIn shows ~25 per page. |
| `maxPages` | No | Number of search result pages per query. Default `1`. Each page has ~25 jobs. |
| `scrapeMode` | No | `standard` (default — fastest, gets all fields), `full` (alternative extraction with fallback), or `fast` (search cards only, no descriptions). |
| `datePosted` | No | Filter: Any time, Past 24 hours, Past week, Past month. |
| `jobType` | No | Filter: Full-time, Part-time, Contract, Temporary, Internship. |
| `experienceLevel` | No | Filter: Internship, Entry level, Associate, Mid-Senior level, Director, Executive. |
| `proxyConfiguration` | No | Proxy settings. Leave default for best results. |

## Scrape modes

- **Standard (recommended)**: Fastest and most affordable. Gets all fields including descriptions, salary, and skills.
- **Full**: Alternative extraction method with fallback. Use if Standard returns incomplete data for your queries.
- **Fast**: Extracts data from search result cards only — title, company, location, posted date, apply URL. Best for bulk collection when descriptions aren't needed.

## Use cases

- **B2B sales / RevOps (buying signals)**: Filter for `skills: ["Salesforce"]` to find Salesforce customers; filter for `skills: ["Snowflake"]` to find data-stack buyers. Hiring posts are the cleanest public proxy for tech-stack adoption.
- **ABM teams**: Track hiring velocity at your 200 named accounts — companies posting 10+ roles in 30 days are in expansion mode and primed for outreach.
- **Competitive intelligence**: Pull every job your top 5 competitors posted last month — see which functions they're scaling, which markets they're entering, and what their salary bands signal about funding.
- **Recruiters / talent-sourcing**: Power sourcing workflows with fresh public listings, parsed salary, and apply URLs.
- **Investors / market analysts**: Use net hiring as a portfolio-monitoring leading indicator — growth, contraction, and pivots show up in job posts before press releases.
- **Job aggregators**: Build global job boards with LinkedIn as the flagship feed.
- **Salary analytics**: Benchmark parsed salary ranges across roles, levels, and geographies.
- **Labor-market research**: Study demand by skill, industry, and geography over time.

 

## Use cases & recipes

Step-by-step guides on [thirdwatch.dev/blog](https://thirdwatch.dev/blog):

- [Build a LinkedIn Jobs Aggregator with Apify (2026 Guide)](https://thirdwatch.dev/blog/build-linkedin-jobs-aggregator-with-apify)
- [Filter LinkedIn Jobs by Skill and Location (2026 Guide)](https://thirdwatch.dev/blog/filter-linkedin-jobs-by-skill-and-location)
- [Scrape LinkedIn Jobs Without Login at Scale (2026 Guide)](https://thirdwatch.dev/blog/scrape-linkedin-jobs-without-login)
- [Track LinkedIn Hiring Velocity by Company (2026)](https://thirdwatch.dev/blog/track-linkedin-hiring-velocity-by-company)

 -end

## Limitations

- Salary fields are populated for roughly 40-60% of listings — LinkedIn shows salary only when the employer opts in.
- `skills` and `description` require Standard or Full mode; Fast mode reads only the search cards.
- Easy Apply jobs have an `apply_url` pointing back to LinkedIn; direct-apply jobs link to the employer's site.
- No login means no personalized recommendations — only public listings.
- **Per-query result ceiling: ~1000 jobs.** LinkedIn's public guest endpoint stops paginating around the 1000th result. To pull more, split by location, role, `job_type`, or `date_posted` and run several queries.
- **Match precision is good, not exact.** Public guest search is broader than logged-in search — e.g. `"account manager"` may surface adjacent sales roles. Use specific titles and the `job_type` / `experience_level` filters to tighten results. Boolean operators (AND / OR / NOT) are not supported on the public endpoint.
- Very high volumes may hit LinkedIn rate limits; split large pulls across multiple runs.

## Compared to alternatives

- **vs. LinkedIn's public API**: LinkedIn does not offer an open job-search API for third parties. This actor is the structured-data alternative.
- **vs. hiring-intent platforms (LinkedIn Talent Insights, Lightcast, Revelio)**: Those tools cost $20K–$100K/year for enterprise seats. This actor returns the underlying job-post data — title, company, skills, salary, posted_at — at a flat per-result rate, so you can build the same hiring-intent signals in-house.
- **vs. curious_coder/linkedin-jobs-scraper** ($0.001/result, 45K users): Cheaper per result with a much larger installed base, but returns fewer fields and does not parse salary. Use this actor when you need structured salary, skills, and descriptions with a free trial.
- **vs. bebity/linkedin-jobs-scraper** (~$0.005/result): Comparable fields, but no tiered volume discounts.

Pairs well with [Indeed Scraper](https://apify.com/thirdwatch/indeed-jobs-scraper) and [Naukri Scraper](https://apify.com/thirdwatch/naukri-jobs-scraper) for multi-source hiring datasets.

## FAQ

**Do I need a LinkedIn account?**
No. The scraper accesses only publicly visible job listing pages.

**Why are some fields empty in Fast mode?**
Fast mode reads only the search cards. Salary, skills, and description require Standard or Full mode.

**What if I get blocked?**
The actor has built-in rate limiting. If you see failures, lower `maxPages`, shrink queries, or spread runs across the day.

Last verified: 2026-05

More scrapers at [thirdwatch.dev](https://thirdwatch.dev).