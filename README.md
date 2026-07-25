[Linkedin Jobs Scraper](https://apify.com/mr.data_scientist/linkedin-jobs-scraper?fpr=data)

# LinkedIn Jobs Scraper

Scrape LinkedIn job listings with powerful filtering options. Extract job titles, companies, locations, descriptions, seniority levels, employment types, and more — all without requiring a LinkedIn account.

## Features

- 🔍 **Advanced Search Filters**: Filter by location radius, date posted, experience level, and work type
- 📊 **Comprehensive Data**: Extract full job details including description, seniority, employment type, industries
- 🚀 **Fast & Efficient**: Optimized scraping with smart pagination handling
- 🔒 **No Login Required**: Uses LinkedIn's public job listings
- 📁 **Multiple Export Formats**: JSON, CSV, Excel via Apify datasets
- ⚡ **Proxy Support**: Built-in proxy rotation for reliable scraping

## How to Use

 

## Input Parameters

| Parameter | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `searchQueries` | Array | ✅ Yes | - | List of search queries with title and location |
| `distance` | String | No | "40" | Search radius: "0", "8", "16", "40", "80", "160" km |
| `datePosted` | String | No | "any" | Time filter: "any", "24hr", "week", "month" |
| `experienceLevel` | Array | No | [] | Experience levels: internship, entry, associate, mid-senior, director, executive |
| `workType` | Array | No | [] | Work types: remote, hybrid, onsite |
| `maxJobs` | Number | No | 25 | Maximum jobs per search query (1-1000) |
| `scrapeJobDetails` | Boolean | No | true | Fetch full job descriptions |
| `proxy` | Object | No | No proxy | Proxy configuration (optional) |

### Example Input

```
{
    "searchQueries": [
        {
            "title": "Software Engineer",
            "location": "San Francisco, CA"
        },
        {
            "title": "Software Developer",
            "location": "San Francisco, CA"
        },
        {
            "title": "Backend Engineer",
            "location": "San Francisco, CA"
        },
        {
            "title": "Full Stack Developer",
            "location": "New York, NY"
        }
    ],
    "distance": "40",
    "datePosted": "week",
    "experienceLevel": ["entry", "associate", "mid-senior"],
    "workType": ["remote", "hybrid"],
    "maxJobs": 50,
    "scrapeJobDetails": true
}
```

## Output

Each scraped job contains the following fields:

| Field | Type | Description |
| --- | --- | --- |
| `job_title` | String | Job title |
| `company` | String | Company name |
| `location` | String | Job location |
| `job_link` | String | Direct link to the job posting |
| `posting_date` | String | When the job was posted (MM/DD/YYYY) |
| `description` | String | Full job description (if `scrapeJobDetails` is true) |
| `seniority_level` | String | Seniority level (e.g., "Mid-Senior level") |
| `employment_type` | String | Employment type (e.g., "Full-time") |
| `job_function` | String | Job function/department |
| `industries` | String | Industry sectors |
| `search_query` | String | The search query that found this job |
| `search_location` | String | The location used in the search |
| `scraped_at` | String | Timestamp of when the job was scraped |

### Example Output

```
{
    "job_title": "Senior Software Engineer",
    "company": "TechCorp Inc.",
    "location": "San Francisco, CA",
    "job_link": "https://www.linkedin.com/jobs/view/1234567890",
    "posting_date": "01/03/2026",
    "description": "We are looking for a Senior Software Engineer to join our team...",
    "seniority_level": "Mid-Senior level",
    "employment_type": "Full-time",
    "job_function": "Engineering, Information Technology",
    "industries": "Software Development, Technology",
    "search_query": "Software Engineer",
    "search_location": "San Francisco, CA",
    "scraped_at": "2026-01-05T10:30:00.000Z"
}
```

## Filter Options

### Distance Radius

| Value | Description |
| --- | --- |
| "0" | Exact location only |
| "8" | 8 km (5 miles) |
| "16" | 16 km (10 miles) |
| "40" | 40 km (25 miles) - Default |
| "80" | 80 km (50 miles) |
| "160" | 160 km (100 miles) |

### Date Posted

| Value | Description |
| --- | --- |
| "any" | Any time (no filter) |
| "24hr" | Past 24 hours |
| "week" | Past week |
| "month" | Past month |

### Experience Level

| Value | Description |
| --- | --- |
| "internship" | Internship |
| "entry" | Entry level |
| "associate" | Associate |
| "mid-senior" | Mid-Senior level |
| "director" | Director |
| "executive" | Executive |

### Work Type

| Value | Description |
| --- | --- |
| "remote" | Remote work |
| "hybrid" | Hybrid (office + remote) |
| "onsite" | On-site only |

## Usage Tips

1. **Use Multiple Job Titles**: Search for the same role using different title variations (e.g., "Software Engineer", "Software Developer", "SWE") to maximize results
2. **Start Small**: Begin with a lower `maxJobs` value (25-50) to test your filters
3. **Add Delays**: Increase `requestDelayMs` if you experience rate limiting
4. **Combine Filters**: Use multiple experience levels and work types for broader searches
5. **Specific Locations**: Use city + state/country format for better location matching

## Rate Limiting & Best Practices

- The actor includes built-in delays between requests to avoid rate limiting
- Consider running during off-peak hours for better performance
- Split large searches into multiple smaller runs

## Integrations

Export your data to:

- **Google Sheets**: Via Apify integrations
- **Webhooks**: Send data to your API endpoints
- **Email**: Get notified when new jobs are found
- **Zapier/Make/n8n**: Connect to 1000+ apps

## Changelog

- Full filtering support (distance, date, experience, work type)
- Job detail scraping
- Pagination support
- Proxy integration

## Support

If you have any issues or feature requests:

- Open an issue on GitHub
- Contact support through Apify
- OR email me: [mrali.hassan997@gmail.com](mailto:mrali.hassan997@gmail.com)