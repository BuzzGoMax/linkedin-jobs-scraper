[Linkedin Jobs Scraper](https://apify.com/sovereigntaylor/linkedin-jobs-scraper?fpr=data)

# LinkedIn Jobs Scraper

Scrape public LinkedIn job listings without requiring a LinkedIn account or login. Extract job titles, companies, locations, salaries, descriptions, applicant counts, and application links.

> **Important: Proxy Required** — LinkedIn actively blocks datacenter IPs. This actor requires **residential or premium proxies** to work reliably. Configure `proxyConfiguration` with `"apifyProxyGroups": ["RESIDENTIAL"]` for best results. Without proper proxy configuration, most requests will be blocked with 999 error codes.

## Features

- **No Login Required** -- scrapes LinkedIn's public job search pages
- **Rich Data Extraction** -- titles, companies, locations, salaries, full descriptions, criteria, apply links
- **Flexible Filters** -- keyword, location, time posted, job type, experience level, remote/on-site/hybrid
- **Multiple Parsing Strategies** -- handles LinkedIn's frequent HTML changes with 3 fallback strategies
- **User-Agent Rotation** -- 8 rotating browser User-Agents to reduce detection
- **Respectful Crawling** -- built-in rate limiting and random delays
- **Pagination** -- automatically pages through results (up to 1000 per search)
- **PPE Billing** -- pay-per-event pricing (charges per job scraped)
- **Proxy Support** -- works with Apify residential proxies for reliable results

## Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `keyword` | string | `"software engineer"` | Job title, skill, or company to search for |
| `location` | string | `"United States"` | City, state, country, or "Remote" |
| `timePosted` | enum | `"any"` | `any`, `past24h`, `pastWeek`, `pastMonth` |
| `jobType` | enum | `"any"` | `any`, `fulltime`, `parttime`, `contract`, `internship`, `temporary`, `volunteer` |
| `experienceLevel` | enum | `"any"` | `any`, `internship`, `entry`, `associate`, `mid-senior`, `director`, `executive` |
| `remoteFilter` | enum | `"any"` | `any`, `remote`, `onsite`, `hybrid` |
| `maxResults` | integer | `25` | Max jobs to scrape (0 = unlimited) |
| `scrapeJobDetails` | boolean | `true` | Visit each job's detail page for full description |
| `maxConcurrency` | integer | `2` | Concurrent requests (keep low for LinkedIn) |
| `proxyConfiguration` | object | - | Apify proxy config (recommended: residential) |

### Example Input

```
{
    "keyword": "data scientist",
    "location": "San Francisco, CA",
    "timePosted": "pastWeek",
    "jobType": "fulltime",
    "experienceLevel": "mid-senior",
    "remoteFilter": "remote",
    "maxResults": 50,
    "scrapeJobDetails": true,
    "proxyConfiguration": {
        "useApifyProxy": true,
        "apifyProxyGroups": ["RESIDENTIAL"]
    }
}
```

## Output

Each scraped job listing contains the following fields:

| Field | Type | Description |
| --- | --- | --- |
| `title` | string | Job title |
| `company` | string | Company name |
| `location` | string | Job location |
| `salary` | string | Salary range (if displayed) |
| `jobId` | string | LinkedIn job posting ID |
| `jobUrl` | string | Direct link to job posting |
| `postedDate` | string | Approximate posting date (ISO 8601) |
| `postedDateRaw` | string | Raw date text from LinkedIn |
| `employmentType` | string | Full-time, Part-time, Contract, etc. |
| `experienceLevel` | string | Entry, Mid-Senior, Director, etc. |
| `industry` | string | Industry classification |
| `jobFunction` | string | Job function/department |
| `description` | string | Full job description (plain text) |
| `descriptionHtml` | string | Full description (HTML) |
| `criteria` | object | All job criteria from the detail page |
| `applicantCount` | string | Number of applicants text |
| `companyUrl` | string | Company LinkedIn page URL |
| `companyDetails` | array | Company size, industry, etc. |
| `applyUrl` | string | External application URL (if available) |
| `benefits` | array | Listed benefits/perks |
| `searchKeyword` | string | The keyword used in the search |
| `searchLocation` | string | The location used in the search |
| `scrapedAt` | string | Timestamp when this job was scraped |

### Example Output

```
{
    "title": "Senior Data Scientist",
    "company": "Stripe",
    "location": "San Francisco, CA (Remote)",
    "salary": "$180,000 - $250,000/yr",
    "jobId": "3847291056",
    "jobUrl": "https://www.linkedin.com/jobs/view/3847291056/",
    "postedDate": "2026-02-25T00:00:00.000Z",
    "postedDateRaw": "4 days ago",
    "employmentType": "Full-time",
    "experienceLevel": "Mid-Senior level",
    "industry": "Technology, Information and Internet",
    "jobFunction": "Engineering and Information Technology",
    "description": "We're looking for a Senior Data Scientist to join our Risk team...",
    "descriptionHtml": "<p>We're looking for a Senior Data Scientist...</p>",
    "criteria": {
        "seniority_level": "Mid-Senior level",
        "employment_type": "Full-time",
        "job_function": "Engineering and Information Technology",
        "industries": "Technology, Information and Internet"
    },
    "applicantCount": "127 applicants",
    "companyUrl": "https://www.linkedin.com/company/stripe",
    "companyDetails": ["5,001-10,000 employees", "Financial Services"],
    "applyUrl": "https://stripe.com/jobs/listing/senior-data-scientist/...",
    "benefits": ["Health insurance", "401(k)"],
    "searchKeyword": "data scientist",
    "searchLocation": "San Francisco, CA",
    "scrapedAt": "2026-03-01T12:00:00.000Z"
}
```

## Use Cases

- **Job Market Research** -- analyze hiring trends by role, location, and industry
- **Salary Benchmarking** -- collect salary data across companies and regions
- **Competitive Hiring Analysis** -- track which companies are hiring for specific roles
- **Lead Generation** -- identify companies with open positions for B2B outreach
- **HR & Recruiting** -- monitor competitor job postings and compensation
- **Career Planning** -- track demand for specific skills and technologies
- **Talent Market Intelligence** -- understand which markets have the most openings
- **Academic Research** -- study labor market dynamics and trends

## Tips for Best Results

1. **Use Proxies** -- LinkedIn actively blocks datacenter IPs. Use Apify residential proxies for reliable scraping.
2. **Keep Concurrency Low** -- set `maxConcurrency` to 1-2. LinkedIn is aggressive about rate limiting.
3. **Start Small** -- test with `maxResults: 10` before scaling up.
4. **Specific Keywords** -- more specific keywords yield better results (e.g., "senior react developer" vs "developer").
5. **Off-Peak Hours** -- scraping during off-peak hours (weekends, nights) may reduce blocking.

## Limitations

- LinkedIn may change their public page structure at any time. The scraper uses 3 fallback parsing strategies to handle this.
- Salary data is only available when the employer or LinkedIn chooses to display it (roughly 30-40% of listings).
- LinkedIn caps public search pagination at approximately 1,000 results.
- Some job details may require authentication to access -- the scraper extracts what is publicly available.
- Rate limiting is common. Using residential proxies significantly improves reliability.

## Cost / Pricing

This actor uses Pay-Per-Event (PPE) pricing. You are charged for each job listing successfully scraped. There is no charge for failed requests or blocked pages.

## Technical Details

- Built with **CheerioCrawler** from Crawlee (no browser overhead)
- ESM modules (Node.js 20+)
- Handles LinkedIn's auth walls, CAPTCHAs, and 999 error codes
- Automatic retry with exponential backoff on failures
- Deduplicates results by LinkedIn job ID

## Integration — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("sovereigntaylor/linkedin-jobs-scraper").call(run_input={
    "keyword": "data scientist",
    "location": "San Francisco, CA",
    "timePosted": "pastWeek",
    "maxResults": 50,
    "scrapeJobDetails": True,
    "proxyConfiguration": {
        "useApifyProxy": True,
        "apifyProxyGroups": ["RESIDENTIAL"]
    }
})

for job in client.dataset(run["defaultDatasetId"]).iterate_items():
    salary = job.get("salary", "Not listed")
    print(f"{job['title']} at {job['company']} — {salary}")
```

## Integration — JavaScript

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('sovereigntaylor/linkedin-jobs-scraper').call({
    keyword: 'data scientist',
    location: 'San Francisco, CA',
    timePosted: 'pastWeek',
    maxResults: 50,
    scrapeJobDetails: true,
    proxyConfiguration: {
        useApifyProxy: true,
        apifyProxyGroups: ['RESIDENTIAL']
    }
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(job => {
    console.log(`${job.title} at ${job.company} — ${job.salary || 'Not listed'}`);
});
```

## Related Actors

- [LinkedIn Company Scraper](https://apify.com/sovereigntaylor/linkedin-company-scraper) — Scrape LinkedIn company profiles
- [LinkedIn Profile Scraper](https://apify.com/sovereigntaylor/linkedin-profile-scraper) — Extract LinkedIn profile data
- [Indeed Scraper](https://apify.com/sovereigntaylor/indeed-scraper) — Compare with Indeed job listings
- [Indeed Salary Scraper](https://apify.com/sovereigntaylor/indeed-salary-scraper) — Salary data and compensation benchmarks
- [Glassdoor Scraper](https://apify.com/sovereigntaylor/glassdoor-scraper) — Company reviews and salary data