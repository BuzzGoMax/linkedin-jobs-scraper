[Linkedin Jobs Scraper](https://apify.com/vulnv/linkedin-jobs-scraper?fpr=data)

# 💼 LinkedIn Jobs Scraper ⚡ No Login Required

## Overview

The **LinkedIn Jobs Scraper** is an Apify Actor that extracts comprehensive job data from **LinkedIn Jobs** at scale. Perfect for job market analysis, recruitment research, salary benchmarking, and competitive intelligence — with **no LinkedIn login, cookies, or browser automation required**.

✅ No LinkedIn login required | ✅ Advanced search filters | ✅ Automated pagination | ✅ Structured JSON output | ✅ High success rate

---

### **Complete Job Data**

- **Job Information** — Title, description, job type, experience level, remote options
- **Company Details** — Company name, size, industry, location
- **Salary Information** — Salary ranges and compensation details (when available)
- **Location Data** — Job location, remote/hybrid options, location radius
- **Application Details** — Application URLs, posting date, job status
- **Requirements** — Skills, qualifications, experience requirements
- **Benefits** — Company benefits and perks (when available)
- **Metadata** — Job ID, posting timestamp, extraction timestamp

### **Advanced Search Filters**

- **Location-based** — Search by city, country, and radius
- **Keyword Search** — Job titles, skills, company names
- **Experience Level** — Internship to Executive positions
- **Job Type** — Full-time, Part-time, Contract, Temporary
- **Work Arrangement** — On-site, Remote, Hybrid
- **Time Range** — Past 24 hours to any time
- **Company Filter** — Target specific companies

---

## 🧾 Input Configuration

The scraper uses a simple, intuitive input format for single job searches:

```
{
  "location": "New York",
  "keyword": "python developer",
  "country": "US",
  "time_range": "Past month",
  "job_type": "Full-time",
  "experience_level": "Mid-Senior level",
  "remote": "Remote",
  "max_jobs": 25
}
```

### **Input Parameters**

| Field | Required | Description | Example |
| --- | --- | --- | --- |
| `location` | ✅ | Job location | "New York", "London", "Berlin" |
| `keyword` | ❌ | Job title/keywords | "python developer", "marketing manager" |
| `max_jobs` | ❌ | Max jobs to collect (1-100) | 25 |
| `country` | ❌ | Country code (2 letters) | "US", "GB" (for UK), "FR", "DE", "CA" |
| `time_range` | ❌ | Posting timeframe | "Past 24 hours", "Past week", "Past month", "Any time" |
| `job_type` | ❌ | Employment type | "Full-time", "Part-time", "Contract", "Temporary", "Volunteer" |
| `experience_level` | ❌ | Experience required | "Internship", "Entry level", "Associate", "Mid-Senior level", "Director", "Executive" |
| `remote` | ❌ | Work arrangement | "On-site", "Remote", "Hybrid" |
| `company` | ❌ | Company name | "Google", "Microsoft", "Apple" |
| `selective_search` | ❌ | Strict keyword matching | `true`, `false` |
| `location_radius` | ❌ | Search radius | "Exact location", "5 miles (8 km)", "25 miles (40 km)" |

---

## 📤 Output Format

Each job will return comprehensive structured data such as:

```
{
  "job_posting_id": "3472834729",
  "job_title": "Senior Python Developer",
  "company_name": "TechCorp Inc",
  "company_url": "https://www.linkedin.com/company/techcorp",
  "location": "San Francisco, CA",
  "remote_allowed": true,
  "job_type": "Full-time",
  "experience_level": "Mid-Senior level",
  "posted_date": "2024-01-15T10:30:00Z",
  "application_url": "https://www.linkedin.com/jobs/view/3472834729",
  "job_description": "We are seeking a Senior Python Developer to join our growing engineering team...",
  "requirements": [
    "5+ years of Python experience",
    "Experience with Django/Flask",
    "Knowledge of cloud platforms (AWS/GCP)",
    "Strong problem-solving skills"
  ],
  "benefits": [
    "Competitive salary",
    "Health insurance",
    "Remote work options",
    "Professional development budget"
  ],
  "salary_range": {
    "min": 120000,
    "max": 180000,
    "currency": "USD",
    "period": "annual"
  },
  "company_info": {
    "industry": "Technology",
    "company_size": "201-500 employees",
    "headquarters": "San Francisco, CA"
  },
  "applicants_count": 47,
  "timestamp": "2024-01-16T14:25:30.965Z"
}
```

---

## ⚙️ Smart Pagination

When you request more than 5 jobs (`max_jobs > 5`), the scraper automatically handles pagination:

- **Splits requests** into multiple API calls (max 5 jobs per call)
- **Prevents duplicates** using job ID tracking
- **Continues until target** is reached or no more jobs available

**Example:** `max_jobs: 15` results in 3 API calls collecting 5 jobs each.

---

## ✅ Usage Examples

### Basic Job Search

```
{
  "location": "Chicago",
  "keyword": "marketing manager",
  "max_jobs": 10
}
```

### Advanced Filtered Search

```
{
  "location": "Remote",
  "keyword": "frontend developer",
  "time_range": "Past week",
  "job_type": "Contract",
  "remote": "Remote",
  "experience_level": "Mid-Senior level",
  "selective_search": true,
  "max_jobs": 30
}
```

### Company-Specific Search

```
{
  "location": "Seattle",
  "company": "Amazon",
  "country": "US",
  "job_type": "Full-time",
  "location_radius": "25 miles (40 km)",
  "max_jobs": 50
}
```

### International Search

```
{
  "location": "Berlin",
  "keyword": "data scientist",
  "country": "DE",
  "remote": "Hybrid",
  "experience_level": "Entry level",
  "max_jobs": 20
}
```

---

## 📊 Output & Export

### **Dataset Storage**

- All extracted job data is stored in your Apify dataset
- Each job becomes one dataset item
- Failed extractions are logged with error details

### **Export Formats**

- **JSON** — Raw structured data for API integration
- **CSV** — Spreadsheet-compatible format for analysis
- **Excel** — Formatted spreadsheet for reporting

---

## 💼 Common Use Cases

### **Recruitment & Talent Acquisition**

- Source candidates by analyzing job requirements and qualifications
- Track competitor hiring patterns and salary benchmarks
- Identify in-demand skills and experience levels in specific markets

### **Market Research & Analysis**

- Analyze job market trends by location, industry, and role
- Monitor salary ranges and compensation trends over time
- Research company hiring activity and growth patterns

### **Career Planning & Development**

- Discover skill requirements for target positions
- Compare salaries across different companies and locations
- Track job availability and market demand in specific fields

### **Business Intelligence & Strategy**

- Monitor competitor workforce expansion and hiring priorities
- Analyze industry talent demands and skill gaps
- Research market entry opportunities in different geographic regions

---

## 🚀 Getting Started

### **Using the Apify Console**

1. **Set your search criteria** — Enter location, keywords, and filters
2. **Choose job limit** — Set how many jobs to collect (1-100)
3. **Run the scraper** — Click "Start" and monitor progress
4. **Download results** — Export in JSON, CSV, or Excel format

### **Using the API**

```
curl -X POST https://api.apify.com/v2/acts/YOUR_ACTOR_ID/runs \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "location": "New York",
    "keyword": "data analyst",
    "country": "US",
    "experience_level": "Entry level",
    "max_jobs": 25
  }'
```

### **Command Line Testing**

```
# Quick test
apify run -p --input-file=test-small.json

# Pagination test
apify run -p --input-file=test-pagination.json

# Standard test
apify run -p --input-file=test.json
```

---

## 🎯 Key Features

✅ **Simple Input** — Just location and optional filters, no complex arrays
✅ **Smart Pagination** — Automatically handles large job requests
✅ **Duplicate Prevention** — Built-in job ID tracking prevents duplicates
✅ **Rich Filters** — All LinkedIn search options supported
✅ **Structured Output** — Clean, consistent JSON data format
✅ **Error Handling** — Robust retry mechanisms and detailed logging
✅ **No Authentication** — Works without LinkedIn login or cookies

Ready to start scraping LinkedIn jobs? Simply enter your search criteria and let the scraper handle the rest! 🎉