[Linkedin Jobs Scraper](https://apify.com/parseforge/linkedin-jobs-scraper?fpr=data)

![ParseForge Banner](https://images.apifyusercontent.com/wTxwbnRh8X878EoDysptDr1AzClsoPHSsuMaYGmWENw/w:1800/cb:1/aHR0cHM6Ly9naXRodWIuY29tL1BhcnNlRm9yZ2UvYXBpZnktYXNzZXRzL2Jsb2IvYWQzNWNjYzEzZGRkMDY4YjlkNmNiYTMzZjMyMzk2MmUzOWFlZDViMi9iYW5uZXIuanBnP3Jhdz10cnVl.webp)

# 💼 LinkedIn Jobs Scraper

> 🚀 **Collect job listings from LinkedIn in minutes.** Search by keyword, location, job type, experience level, and salary. Export titles, companies, parsed salary ranges, extracted skills, and full descriptions. No coding, no LinkedIn login.

> 🕒 **Last updated:** 2026-04-16 · **📊 30+ fields** per job · **💰 Parsed salary ranges** · **🛠️ Skill extraction** · **🚫 No login** required

The **LinkedIn Jobs Scraper** collects job listing data from LinkedIn, returning **30+ fields per job**: title, company, location, parsed salary (min/max with currency), extracted skills, experience level, workplace type, applicant count, posting date, full description, and Easy Apply flag. Runs support up to 1,000,000 listings on a paid plan.

The Actor supports keyword search with 10+ filters: location, date posted, job type (full-time, part-time, contract, internship), experience level, workplace type (remote, hybrid, on-site), salary minimum, Easy Apply toggle, and sort order. Optional detail-page fetching adds full descriptions, parsed skills, and company info.

| 🎯 Target Audience | 💡 Primary Use Cases |
| --- | --- |
| Recruiters, HR teams, job aggregators, workforce analysts, salary benchmarking firms, competitive intelligence teams | Job market research, salary benchmarking, recruitment intelligence, skill-demand tracking, competitor hiring analysis |

---

## 📋 What the LinkedIn Jobs Scraper does

Keyword search with 10+ filters:

- 🔍 **Keyword search.** Job title, skills, or company name.
- 📍 **Location filter.** City, state, country, or "Remote".
- 📅 **Date posted filter.** Past 24 hours, week, or month.
- 🏷️ **Job type filter.** Full-time, part-time, contract, temporary, internship, volunteer.
- 📊 **Experience level filter.** Entry, associate, mid-senior, director, executive.
- 🏠 **Workplace type filter.** On-site, remote, hybrid.
- 💰 **Salary filter.** Minimum salary threshold in USD.
- ✅ **Easy Apply toggle.** Return only LinkedIn Easy Apply jobs.
- 📝 **Detail fetching.** Optional full descriptions with parsed skills and company data.

Each job record includes title, company, location, parsed salary range (min, max, currency, period), extracted skills array, experience level, workplace type, applicant count, posting date, job URL, Easy Apply flag, and (when details enabled) full description and company details.

> 💡 **Why it matters:** manually browsing LinkedIn for job market intelligence means scrolling through pages and copying data by hand. This Actor exports structured job data at scale, with parsed salary ranges and extracted skills ready for your dashboards, salary benchmarks, or ATS integrations.

---

## 🎬 Full Demo

*🚧 Coming soon: a 3-minute walkthrough showing how to go from sign-up to a downloaded dataset.*

---

## ⚙️ Input

| Input | Type | Default | Behavior |
| --- | --- | --- | --- |
| `searchQuery` | string | `""` | Job title, keywords, or company name. |
| `location` | string | `""` | City, state, country, or "Remote". |
| `maxItems` | integer | `10` | Max jobs. Free: up to 10. Paid: up to 1,000,000. |
| `datePosted` | string | `""` | Past 24 hours, week, or month. |
| `jobType` | array | `[]` | Full-time, part-time, contract, temporary, internship. |
| `experienceLevel` | array | `[]` | Entry, associate, mid-senior, director, executive. |
| `workplaceType` | array | `[]` | On-site, remote, hybrid. |
| `salary` | string | `""` | Minimum salary in USD. |
| `easyApplyOnly` | boolean | `false` | Only LinkedIn Easy Apply jobs. |
| `scrapeJobDetails` | boolean | `false` | Fetch full descriptions, skills, and company data. |
| `extractSkills` | boolean | `false` | Parse skills from descriptions. |

**Example: remote software engineer jobs posted this week, $100K+.**

```
{
    "searchQuery": "software engineer",
    "location": "Remote",
    "datePosted": "past-week",
    "workplaceType": ["remote"],
    "salary": "100000",
    "scrapeJobDetails": true,
    "extractSkills": true,
    "maxItems": 50
}
```

**Example: entry-level data analyst jobs in New York.**

```
{
    "searchQuery": "data analyst",
    "location": "New York, NY",
    "experienceLevel": ["entry"],
    "maxItems": 100
}
```

> ⚠️ **Good to Know:** residential proxies are recommended for large runs. LinkedIn rate-limits datacenter IPs aggressively. The proxy configuration is pre-filled with recommended settings. Enabling `scrapeJobDetails` is slower (1-2s per job) but returns much richer data.

---

## 📊 Output

Each job record contains **30+ fields** (with details enabled). Download the dataset as CSV, Excel, JSON, or XML.

### 🧾 Schema

| Field | Type | Example |
| --- | --- | --- |
| 📝 `title` | string | `"Senior Software Engineer"` |
| 🏢 `company` | string | `"Google"` |
| 📍 `location` | string | `"Mountain View, CA"` |
| 💰 `salary` | string | `"$150,000 - $200,000/yr"` |
| 💵 `salaryMin` | number | null | `150000` |
| 💵 `salaryMax` | number | null | `200000` |
| 💱 `salaryCurrency` | string | null | `"USD"` |
| 📊 `salaryPeriod` | string | null | `"yearly"` |
| 🏷️ `jobType` | string | `"Full-time"` |
| 📊 `experienceLevel` | string | `"Mid-Senior level"` |
| 🏠 `workplaceType` | string | `"Remote"` |
| 👥 `applicantCount` | string | `"200+ applicants"` |
| 📅 `postedDate` | string | `"2 days ago"` |
| ✅ `easyApply` | boolean | `true` |
| 🛠️ `skills` | array | `["Python", "AWS", "Kubernetes"]` |
| 📝 `description` | string | null | `"We are looking for..."` |
| 🔗 `jobUrl` | string | `"https://www.linkedin.com/jobs/view/..."` |
| 🏢 `companyUrl` | string | null | `"https://www.linkedin.com/company/google"` |
| 🕒 `scrapedAt` | ISO 8601 | `"2026-04-16T00:00:00.000Z"` |

### 📦 Sample records

 
 
 

---

## ✨ Why choose this Actor

|  | Capability |
| --- | --- |
| 💰 | **Parsed salary ranges.** Min, max, currency, and period extracted from salary strings. |
| 🛠️ | **Skill extraction.** Technical and soft skills parsed from job descriptions. |
| 🔍 | **10+ search filters.** Keyword, location, date, type, experience, workplace, salary, Easy Apply. |
| 📊 | **30+ fields per job.** Title, company, salary, skills, applicants, and full description. |
| 📝 | **Optional detail fetching.** Full descriptions, company data, and parsed skills. |
| ⚡ | **Scalable.** From quick 10-job samples to full market sweeps. |
| 🚫 | **No login.** No LinkedIn account or API key needed. |

> 📊 LinkedIn lists millions of active job openings worldwide. Structured access to this data, with parsed salary ranges and extracted skills, powers every recruitment, benchmarking, and workforce-intelligence workflow.

---

## 📈 How it compares to alternatives

| Approach | Cost | Coverage | Refresh | Salary parsing | Setup |
| --- | --- | --- | --- | --- | --- |
| **⭐ LinkedIn Jobs Scraper** *(this Actor)* | $5 free credit, then pay-per-use | Any LinkedIn search | **Live per run** | Yes (min/max/currency) | ⚡ 2 min |
| LinkedIn Recruiter | $8,000+/year | Full platform | Real-time | No parsing | 🐢 Weeks |
| Paid job intelligence platforms | $200-1,000/month | Multi-board | Varies | Some | ⏳ Days |
| Manual LinkedIn browsing | Free | Manual | Manual | No | 🕒 Hours per search |

Pick this Actor when you want LinkedIn job data with parsed salaries and extracted skills, without a Recruiter license.

---

## 🚀 How to use

1. 📝 **Sign up.** [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=vmoqkp) (takes 2 minutes).
2. 🌐 **Open the Actor.** Go to the LinkedIn Jobs Scraper page on the Apify Store.
3. 🎯 **Set input.** Enter a search query and location. Set job type, experience level, and `maxItems`.
4. 🚀 **Run it.** Click **Start** and let the Actor collect your data.
5. 📥 **Download.** Grab your results in the **Dataset** tab as CSV, Excel, JSON, or XML.

> ⏱️ Total time from signup to downloaded dataset: **3-5 minutes.** No coding required.

---

## 💼 Business use cases

| ### 🏢 Recruiters & Staffing Agencies     - Monitor competitor hiring in real time - Track which skills employers demand most - Build candidate-sourcing intelligence - Benchmark offer packages by market | ### 📊 HR & Workforce Planning     - Benchmark salaries against LinkedIn market data - Analyze job posting volume by location and role - Track skill-demand trends over time - Build workforce supply-demand models |
| --- | --- |
| ### 💻 Job Aggregators & Career Platforms     - Feed job boards with fresh LinkedIn listings - Enrich recommendations with salary and skill data - Build salary comparison tools - Power job-alert features | ### 🎓 Job Seekers & Career Advisors     - Research salary ranges before negotiations - Track new postings matching your profile daily - Compare skill requirements across similar roles - Identify high-demand skills in your field |

---

---

## 🌟 Beyond business use cases

Data like this powers more than commercial workflows. The same structured records support research, education, civic projects, and personal initiatives.

| ### 🎓 Research and academia     - Empirical datasets for papers, thesis work, and coursework - Longitudinal studies tracking changes across snapshots - Reproducible research with cited, versioned data pulls - Classroom exercises on data analysis and ethical scraping | ### 🎨 Personal and creative     - Side projects, portfolio demos, and indie app launches - Data visualizations, dashboards, and infographics - Content research for bloggers, YouTubers, and podcasters - Hobbyist collections and personal trackers |
| --- | --- |
| ### 🤝 Non-profit and civic     - Transparency reporting and accountability projects - Advocacy campaigns backed by public-interest data - Community-run databases for local issues - Investigative journalism on public records | ### 🧪 Experimentation     - Prototype AI and machine-learning pipelines with real data - Validate product-market hypotheses before engineering spend - Train small domain-specific models on niche corpora - Test dashboard concepts with live input |

## 🤖 Ask an AI assistant about this scraper

Open a ready-to-send prompt about this ParseForge actor in the AI of your choice:

- 💬 [**ChatGPT**](https://chat.openai.com/?q=How%20do%20I%20use%20the%20%F0%9F%92%BC%20LinkedIn%20Jobs%20Scraper%20%F0%9F%94%93%20No%20Cookie%2FLogin%20Needed%20%F0%9F%93%84%20%2BRaw%20HTML%20by%20ParseForge%20on%20Apify%3F%20Show%20me%20input%20examples%2C%20output%20fields%2C%20common%20use%20cases%2C%20and%20how%20to%20integrate%20it%20into%20a%20workflow.)
- 🧠 [**Claude**](https://claude.ai/new?q=How%20do%20I%20use%20the%20%F0%9F%92%BC%20LinkedIn%20Jobs%20Scraper%20%F0%9F%94%93%20No%20Cookie%2FLogin%20Needed%20%F0%9F%93%84%20%2BRaw%20HTML%20by%20ParseForge%20on%20Apify%3F%20Show%20me%20input%20examples%2C%20output%20fields%2C%20common%20use%20cases%2C%20and%20how%20to%20integrate%20it%20into%20a%20workflow.)
- 🔍 [**Perplexity**](https://perplexity.ai/search?q=How%20do%20I%20use%20the%20%F0%9F%92%BC%20LinkedIn%20Jobs%20Scraper%20%F0%9F%94%93%20No%20Cookie%2FLogin%20Needed%20%F0%9F%93%84%20%2BRaw%20HTML%20by%20ParseForge%20on%20Apify%3F%20Show%20me%20input%20examples%2C%20output%20fields%2C%20common%20use%20cases%2C%20and%20how%20to%20integrate%20it%20into%20a%20workflow.)
- 🅒 [**Copilot**](https://copilot.microsoft.com/?q=How%20do%20I%20use%20the%20%F0%9F%92%BC%20LinkedIn%20Jobs%20Scraper%20%F0%9F%94%93%20No%20Cookie%2FLogin%20Needed%20%F0%9F%93%84%20%2BRaw%20HTML%20by%20ParseForge%20on%20Apify%3F%20Show%20me%20input%20examples%2C%20output%20fields%2C%20common%20use%20cases%2C%20and%20how%20to%20integrate%20it%20into%20a%20workflow.)

## ❓ Frequently Asked Questions

### 💳 Do I need a paid Apify plan to run this actor?

No. You can start right now on the free Apify plan, which includes **$5 in free monthly credit**. That is enough to run this actor several times and explore the output before committing to anything. Paid plans unlock higher limits, more concurrent runs, and larger datasets. [Create a free Apify account here](https://console.apify.com/sign-up?fpr=vmoqkp) to get started.

### 🚨 What happens if my run fails or returns no results?

Failed runs are not charged. If the source site changes, proxies get rate-limited, or a specific input matches nothing, re-run the actor or open our [contact form](https://tally.so/r/BzdKgA) and we will investigate. You can also check the run log in the Apify console to see why the run stopped.

### 📏 How many items can I scrape per run?

Free users are limited to **10 items per run** so you can preview the output and confirm the actor works for your use case. Paid users can raise `maxItems` up to **1,000,000** per run. [Upgrade here](https://console.apify.com/sign-up?fpr=vmoqkp) if you need full scale.

### 🕒 How fresh is the data?

Every run fetches live data at the moment of execution. There is no cache or delay: the records you get reflect what the source returned at that moment. Schedule the actor to maintain a rolling snapshot of the data you need.

### 🧑‍💻 Can I call this actor from my own code?

Yes. Apify exposes every actor as a REST endpoint and ships first-class SDKs for [Node.js](https://docs.apify.com/sdk/js) and [Python](https://docs.apify.com/sdk/python). You can start a run, read the dataset, and handle webhooks from your own app in a few lines. All you need is your Apify API token.

### 📤 How do I export the data?

Every Apify dataset can be downloaded in one click from the console as CSV, JSON, JSONL, Excel, HTML, XML, or RSS. You can also pull results programmatically via the [Apify API](https://docs.apify.com/api/v2) or stream them into BigQuery, S3, and other destinations through built-in integrations.

### 📅 Can I schedule the actor to run automatically?

Yes. Use the Apify scheduler to run the actor on any cadence, from hourly to monthly. Results are saved to your dataset and can be delivered to webhooks, email, Slack, cloud storage, or automation tools such as Zapier and Make.

---

## 🔌 Automating LinkedIn Jobs Scraper

Control the scraper programmatically for scheduled runs and pipeline integrations:

- 🟢 **Node.js.** Install the `apify-client` NPM package.
- 🐍 **Python.** Use the `apify-client` PyPI package.
- 📚 See the [Apify API documentation](https://docs.apify.com/api/v2) for full details.

The [Apify Schedules feature](https://docs.apify.com/platform/schedules) lets you trigger this Actor on any cron interval. Daily pulls keep your recruitment intelligence fresh.

## 🔌 Integrate with any app

LinkedIn Jobs Scraper connects to any cloud service via [Apify integrations](https://apify.com/integrations):

- [**Make**](https://docs.apify.com/platform/integrations/make) - Automate multi-step workflows
- [**Zapier**](https://docs.apify.com/platform/integrations/zapier) - Connect with 5,000+ apps
- [**Slack**](https://docs.apify.com/platform/integrations/slack) - Get alerts on new matching jobs
- [**Airbyte**](https://docs.apify.com/platform/integrations/airbyte) - Pipe job data into your warehouse
- [**GitHub**](https://docs.apify.com/platform/integrations/github) - Trigger runs from commits and releases
- [**Google Drive**](https://docs.apify.com/platform/integrations/drive) - Export datasets straight to Sheets

---

## 🔗 Recommended Actors

- [**🔍 SEEK Job Scraper**](https://apify.com/parseforge/seek-scraper) - Job listings from Australia's largest job board
- [**🔐 ClearedJobs Scraper**](https://apify.com/parseforge/clearedjobs-scraper) - Security-cleared job listings
- [**📊 Glassdoor Jobs Scraper**](https://apify.com/parseforge/glassdoor-scraper-jobs) - Jobs with salary and company data
- [**📸 Instagram Posts Scraper**](https://apify.com/parseforge/instagram-posts-scraper) - Posts and engagement from public profiles
- [**💼 PitchBook Investors Scraper**](https://apify.com/parseforge/pitchbook-investors-scraper) - Investor profiles with AUM and contact data

> 💡 **Pro Tip:** browse the complete [ParseForge collection](https://apify.com/parseforge) for more job and recruitment scrapers.

---

**🆘 Need Help?** [**Open our contact form**](https://tally.so/r/BzdKgA) to request a new scraper, propose a custom data project, or report an issue.

---

> **⚠️ Disclaimer:** this Actor is an independent tool and is not affiliated with, endorsed by, or sponsored by LinkedIn Corporation or Microsoft. All trademarks mentioned are the property of their respective owners. Only publicly available job listing data is collected.