[Linkedin Jobs Scraper](https://apify.com/kaix/linkedin-jobs-scraper?fpr=data)

# LinkedIn Jobs Scraper

Scrape LinkedIn job listings via the public guest API. Search by keyword, browse by company, or fetch specific job IDs. No login required, no proxy needed.

## Why use this scraper?

- Uses LinkedIn's public guest API, no authentication or cookies needed
- 3 input modes: keyword search, company jobs, direct job ID lookup
- 16 fields per job from search results alone (fast, lightweight)
- 43+ fields with detail mode: full description, employer-provided salary, featured benefits, recruiter contact
- Fetch similar jobs per listing via LinkedIn's similar jobs API
- All LinkedIn search filters: job type, experience level, remote/hybrid/on-site, salary range, date posted, Easy Apply
- Structured output ready for analysis pipelines

## Use cases

- Monitor job postings for specific roles, companies, or locations
- Build salary benchmarks from employer-provided compensation data
- Track hiring trends across industries and regions
- Feed structured job data into AI/NLP pipelines
- Aggregate recruiter contact info for outreach
- Discover related roles and salary ranges from similar jobs

## How to use

### Basic search

```
{
  "keywords": "software engineer",
  "location": "San Francisco"
}
```

### Search with filters

```
{
  "keywords": "data scientist",
  "location": "United States",
  "maxJobs": 100,
  "jobType": ["full_time"],
  "experienceLevel": ["mid_senior", "director"],
  "workType": ["remote"],
  "datePosted": "past_week",
  "sortBy": "recent"
}
```

### Browse jobs by company

```
{
  "companyId": "30898036",
  "maxJobs": 50
}
```

Find company IDs from the typeahead API (`/jobs-guest/api/typeaheadHits?typeaheadType=COMPANY&query=Notion`) or from job detail pages (`companyId` field).

### Fetch specific jobs by ID

```
{
  "jobIds": ["4406118990", "4407050560", "4370317193"]
}
```

Always fetches full details. No extra charge for detail fetching in this mode.

### Fetch full job details

```
{
  "keywords": "marketing director",
  "location": "New York",
  "maxJobs": 10,
  "fetchDetails": true
}
```

### Include similar jobs

```
{
  "keywords": "nurse practitioner",
  "location": "Texas",
  "maxJobs": 5,
  "includeSimilar": true,
  "maxSimilarJobs": 50
}
```

### Filter by salary and Easy Apply

```
{
  "keywords": "nurse practitioner",
  "location": "Texas",
  "salary": "100000",
  "easyApplyOnly": true,
  "maxJobs": 50
}
```

## Input

### Search

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| **keywords** | string |  | Job search keywords. Required unless using `companyId` or `jobIds`. |
| **location** | string |  | Job location |
| **maxJobs** | number | 25 | Max listings to scrape (LinkedIn caps at 1000) |
| **sortBy** | select | relevant | `relevant` or `recent` |

### Alternative modes

| Parameter | Type | Description |
| --- | --- | --- |
| **companyId** | string | LinkedIn company ID to list all jobs from that company |
| **jobIds** | string[] | Fetch specific jobs by ID. Always fetches full details. |

### Filters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| **jobType** | string[] |  | `full_time`, `part_time`, `contract`, `temporary`, `volunteer`, `internship`, `other` |
| **experienceLevel** | string[] |  | `internship`, `entry_level`, `associate`, `mid_senior`, `director`, `executive` |
| **workType** | string[] |  | `on_site`, `remote`, `hybrid` |
| **datePosted** | select |  | `past_24h`, `past_week`, `past_month` |
| **salary** | select |  | Minimum salary: `40000` through `200000` |
| **easyApplyOnly** | boolean | false | Only Easy Apply jobs |

### Output options

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| **fetchDetails** | boolean | false | Fetch full job page per listing (~300KB each) |

### Similar jobs

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| **includeSimilar** | boolean | false | Fetch similar jobs per listing |
| **maxSimilarJobs** | number | 25 | Max similar jobs per listing. 0 = unlimited (up to 1000). |

## Pricing

| Event | When charged | Unit |
| --- | --- | --- |
| **job-detail** | Each successful detail fetch in search/company mode | Per job |
| **similar-job** | Each similar job fetched | Per similar job |

Job ID mode (`jobIds`) always fetches details at no extra charge. Search-only mode (no `fetchDetails`) incurs no per-item charges.

## Output

### Search-only fields (16 fields, fast)

```
{
  "jobId": "4406118990",
  "jobSlug": "software-engineer-new-grad-at-notion-4406118990",
  "title": "Software Engineer, New Grad",
  "company": "Notion",
  "companySlug": "notionhq",
  "companyUrl": "https://www.linkedin.com/company/notionhq",
  "companyLogoUrl": "https://media.licdn.com/dms/image/v2/D4E0BAQGwvcv_1tHZ4w/company-logo_100_100/B4EZW25gE2GgAQ-/0/1742530282185/notionhq_logo?e=2147483647&v=beta&t=h_sgZm5R2TgP9Fpbo95m2wmxnSDoEz06eupofZwpSXs",
  "location": "San Francisco, CA",
  "jobUrl": "https://www.linkedin.com/jobs/view/software-engineer-new-grad-at-notion-4406118990",
  "position": 1,
  "postedDate": "2026-04-24",
  "postedTimeAgo": "1 week ago",
  "isNew": false,
  "salary": null,
  "badge": "Actively Hiring",
  "benefitsCount": null,
  "scrapedAt": "2026-05-01T05:06:50.232Z"
}
```

### Detail fields (with `fetchDetails: true` or `jobIds`)

```
{
  "description": "About UsNotion helps you build beautiful tools for your life's work...",
  "descriptionHtml": "<strong>About Us<br><br></strong>Notion helps you build...",
  "experienceLevel": "Entry level",
  "employmentType": "Full-time",
  "jobFunction": "Engineering and Information Technology",
  "industries": "Software Development",
  "applicants": "Over 200 applicants",
  "applicantsStatus": "high",
  "companyId": "30898036",
  "industryIds": "4",
  "titleId": "9",
  "ogTitle": "Notion hiring Software Engineer, New Grad in San Francisco, CA | LinkedIn",
  "referralMultiplier": "2x",
  "geoId": "105638634",
  "hasDirectApply": false,
  "compensationSalary": null,
  "compensationProvider": null,
  "compensationDescription": null,
  "featuredBenefits": [],
  "recruiter": null
}
```

### Compensation and benefits (when available, ~20% of jobs)

From a Financial Planning & Analysis Analyst listing at Jersey Mike's Subs:

```
{
  "compensationSalary": "$102,200.00/yr - $143,100.00/yr",
  "compensationProvider": "Jersey Mike's Subs provided pay range",
  "compensationDescription": "This range is provided by Jersey Mike's Subs. Your actual pay will be based on your skills and experience — talk with your recruiter to learn more.",
  "featuredBenefits": ["Medical insurance", "Vision insurance", "Dental insurance", "401(k)"],
  "hasDirectApply": true
}
```

### Recruiter info (when available, ~5% of jobs)

From a Director, Partner Marketing listing at Pinterest:

```
{
  "recruiter": {
    "name": "Aisling Seaver (Keogh)",
    "title": "Recruiting at Pinterest",
    "profileUrl": "https://ie.linkedin.com/in/aisling-seaver-keogh-017b2253",
    "photoUrl": "https://media.licdn.com/dms/image/v2/D4D03AQG4RJmq4TjpJg/profile-displayphoto-shrink_400_400/..."
  }
}
```

### Similar jobs (with `includeSimilar: true`)

Fetched via LinkedIn's similar jobs API, paginated at 10 per page:

```
{
  "similarJobs": [
    {
      "jobId": "4370317193",
      "title": "Software Engineer (New Grads)",
      "company": "Giga",
      "companyUrl": "https://www.linkedin.com/company/gigaml",
      "companyLogoUrl": "https://media.licdn.com/dms/image/v2/D560BAQGuz5OVE8IcRg/company-logo_100_100/...",
      "location": "San Francisco, CA",
      "salary": "$160,000.00 - $250,000.00",
      "jobUrl": "https://www.linkedin.com/jobs/view/software-engineer-new-grads-at-giga-4370317193",
      "postedDate": "2026-04-14",
      "postedTimeAgo": "2 weeks ago",
      "isNew": false
    }
  ]
}
```

### Detail page related content (with `fetchDetails: true`)

The full job page also includes these related sections (different from the similar jobs API):

```
{
  "peopleAlsoViewed": [
    {
      "jobId": "4318502728",
      "title": "Software Engineer",
      "company": "Imprint",
      "salary": "$140,000.00 - $180,000.00"
    }
  ],
  "similarSearches": [
    { "title": "Technology Intern jobs", "url": "https://www.linkedin.com/jobs/technology-intern-jobs", "openJobsCount": "5,338 open jobs" }
  ],
  "relatedSearches": [
    { "title": "Ascent Aviation Services jobs", "url": "https://www.linkedin.com/jobs/ascent-aviation-services-jobs" }
  ]
}
```

## Limitations

- LinkedIn caps search results at 1000 per query. Use narrower filters to access more listings.