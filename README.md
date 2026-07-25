[Linkedin Jobs Scraper](https://apify.com/logical_scrapers/linkedin-jobs-scraper?fpr=data)

# LinkedIn Jobs Scraper - Apify Actor

A powerful LinkedIn job listings scraper that extracts detailed job information using Apify's robust infrastructure. Perfect for recruiters, job seekers, and market researchers looking to gather comprehensive job market data.

## Features

- **Comprehensive Job Data**: Extract detailed job listings including titles, descriptions, salaries, and requirements
- **Scalable Performance**: Handle large-scale scraping with built-in proxy rotation and rate limiting
- **Rich Metadata**: Collect company information, job locations, posting dates, and more
- **Clean Output**: Structured JSON data ready for analysis or integration
- **Configurable**: Customize search parameters and output size

## Use Cases

1. **Recruitment & HR**

- Track competitor job postings
- Monitor industry hiring trends
- Analyze salary ranges and benefits
2. **Market Research**

- Study job market demands
- Track industry growth patterns
- Analyze skill requirements
3. **Job Seekers**

- Bulk export job opportunities
- Track salary trends
- Monitor new positions in target companies
4. **Data Analysis**

- Generate market insights
- Create salary benchmarks
- Study regional job distribution

## Input Parameters

The actor accepts the following input parameters:

```
{
    "keywords": "software engineer",  // Job search keywords
    "location": "San Francisco, CA",  // Location for job search
    "maxRows": 100                   // Maximum number of jobs to scrape (default: 100)
}
```

## Output Format

The actor outputs detailed job information in JSON format:

```
[
    {
        "@context": "http://schema.org",
        "@type": "JobPosting",
        "datePosted": "2024-11-14T17:04:59.000Z",
        "employmentType": "FULL_TIME",
        "hiringOrganization": {
            "@type": "Organization",
            "name": "Patreon",
            "sameAs": "https://www.linkedin.com/company/patreon",
            "logo": "https://media.licdn.com/dms/image/..."
        },
        "identifier": {
            "@type": "PropertyValue",
            "name": "Patreon",
            "value": "a2a4d103e4dd42439c0a52f3d3abd273"
        },
        "image": "https://media.licdn.com/dms/image/...",
        "industry": "Technology, Information and Internet",
        "jobLocation": {
            "@type": "Place",
            "address": {
                "@type": "PostalAddress",
                "addressCountry": "US",
                "addressLocality": "San Francisco",
                "addressRegion": "CA",
                "streetAddress": null
            },
            "latitude": 37.78008,
            "longitude": -122.42016
        },
        "skills": "",
        "title": "Fullstack Software Engineer, Payments",
        "validThrough": "2025-03-05T23:04:45.000Z",
        "educationRequirements": {
            "@type": "EducationalOccupationalCredential",
            "credentialCategory": "bachelor degree"
        },
        "experienceRequirements": {
            "@type": "OccupationalExperienceRequirements",
            "monthsOfExperience": 36
        },
        "jobDescription": [
            "You'll help scale and expand capabilities of Patreon's payment platform that helps creators get paid effectively and on time, every time.",
            "Collaborate with product managers, designers, and other engineers to build new functionality, while maintaining a delightful user experience, motivated by passion for our shared mission.",
            "Work with a focus on frontend frameworks and technologies including React, Javascript, Typescript, etc.",
            "Work with Python, Java, and MySQL on the backend, introducing other technologies when it makes sense.",
            "Build a strong product-minded, engineering culture by mentoring and guiding engineers inside and outside the team"
        ]
    }
]
```

## Key Features

1. **Smart Scraping**

- Automatic proxy rotation
- Rate limiting protection
- Concurrent request handling
- Efficient memory usage
2. **Data Quality**

- Structured JSON output
- Clean, parsed descriptions
- Normalized salary data
- Verified company information
3. **Performance**

- Batch processing
- Async operations
- Error recovery
- Progress tracking

## Performance

- Processes up to 1000 job listings per run
- Average processing time: 2-3 minutes per 100 jobs
- Success rate: >95% for accessible listings
- Automatic retry on rate limits

## Keywords

`linkedin-scraper`, `job-scraping`, `recruitment-tool`, `market-research`, `job-data`, `salary-data`, `employment-insights`, `hiring-trends`, `job-market-analysis`, `python-scraper`, `apify-actor`, `web-scraping`, `data-extraction`, `job-search`, `career-research`