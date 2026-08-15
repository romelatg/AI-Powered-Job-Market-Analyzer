# Job Market Analyzer — CDMX Data Analyst Roles

## Overview
An AI-powered pipeline that automatically extracts and analyzes 
structured insights from job postings using the Claude API. 
Analyzes required skills, seniority levels, and language 
requirements for data analyst roles in Mexico City.

## Tools Used
- Python / pandas
- Claude API (Anthropic)
- Power BI

## How It Works
1. Raw job posting text collected from LinkedIn and OCC Mundial
2. Each posting sent to Claude API for structured data extraction
3. Claude automatically standardizes skill names during extraction
   (e.g. "Excel Avanzado" → "Excel", "DAX" → "Power BI")
4. Claude uses its own judgment to group any skills not explicitly
   listed — making the pipeline scalable without manual updates
5. Results stored in pandas DataFrame with a unique job_id per posting
6. Skills exploded into individual rows for granular analysis
7. Both tables linked in Power BI via job_id for cross-filtering

## Design Decisions
- **Prompt-based standardization over manual mapping**: Initially
  used a hardcoded skill_mapping dictionary to clean skill names.
  Replaced this with Claude's own judgment inside the prompt —
  meaning any new job postings added in the future are automatically
  standardized without touching the code.
- **job_id as a bridge**: Added a unique job_id to both tables so
  Power BI visuals filter each other when clicking on any data point.


## Dashboard Preview
![Dashboard](dashboard_screenshot.png)

## Files
- `job_market_analyzer.ipynb` — full pipeline notebook
- `jobs_analysis.csv` — one row per job posting
- `skills_analysis.csv` — one row per skill mention

## How to Run
1. Clone this repository
2. Install dependencies: `pip install requests pandas`
3. Get a Claude API key from console.anthropic.com
4. Replace `YOUR_API_KEY_HERE` in the notebook with your key
5. Add job posting texts to the `job_postings` list
6. Run all cells in order
7. Load the exported CSVs into Power BI
