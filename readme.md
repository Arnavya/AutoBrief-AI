# AI-Powered Trend Intelligence & Startup Opportunity Discovery System

## Overview

This project is an agentic workflow built using n8n that automatically collects, analyzes, and summarizes trending content from YouTube and the web to generate actionable business insights and startup opportunities.

The workflow was inspired by a personal productivity problem. I often spent significant time browsing YouTube, Reddit, Twitter, blogs, and other online sources to stay updated on topics such as C++, low-latency systems, quantitative finance, algorithmic trading, and AI automation. Although I started with productive content, I frequently drifted into unrelated entertainment content, wasting time searching for information rather than consuming valuable insights.

To solve this problem, I designed an AI-powered intelligence system that automatically gathers relevant information, identifies trends, summarizes key developments, and generates potential startup and business opportunities based on emerging patterns.

The final output is a professionally formatted daily intelligence report delivered directly to the user's inbox.

---

# Problem Statement

### Target User

Developers, founders, researchers, students, and professionals who need to stay informed about rapidly evolving industries without spending hours manually searching for information.

### Pain Point

Staying up to date with industry trends requires monitoring multiple platforms and sources. This process is time-consuming, repetitive, and often leads to information overload.

### Proposed Solution

An automated AI workflow that:

* Collects information from YouTube and the web
* Identifies relevant trends
* Summarizes important content
* Detects emerging patterns
* Generates startup and business opportunities
* Delivers a concise report directly to the user

### Expected Output

A daily trend intelligence report containing:

* Executive summary
* Trending topics
* Video summaries
* Industry news
* Emerging patterns
* Business opportunities
* Startup ideas

---

# Workflow Architecture

## Step 1: Data Collection

### YouTube Content Discovery

The workflow searches YouTube for recently published videos related to selected niches.

Current niche examples:

* C++
* Low Latency Systems
* Quantitative Finance
* High Frequency Trading
* Algorithmic Trading
* AI Automation

The system retrieves the top videos matching these topics.

### Web Intelligence Collection

The workflow uses Tavily Search to gather recent developments and news from across the web.

This provides broader context beyond YouTube content.

---

## Step 2: Deterministic Filtering

### Short Video Removal

A validation step removes YouTube Shorts and very short videos.

Criteria:

* Video duration must exceed 210 seconds

Purpose:

* Improve information quality
* Reduce noise
* Focus on educational and in-depth content

---

## Step 3: Video Intelligence Processing

### Video Intelligence Builder

This component extracts and organizes metadata including:

* Video title
* Description
* Tags
* Timestamps
* Channel information
* Duration
* Topics

The output is converted into a structured format suitable for AI processing.

### Context Builder

This stage prepares clean context for the language model.

Responsibilities:

* Content organization
* Metadata consolidation
* Topic extraction
* Intent detection
* Quality scoring

---

## Step 4: AI Content Analysis Agent

### Transcript Analysis Agent

Role:
Content Analyst Agent

Responsibilities:

* Understand video content
* Identify main thesis
* Extract key arguments
* Generate concise summaries
* Produce detailed insights

Output:

```json
{
  "Title": "...",
  "Link": "...",
  "Quick Summary": "...",
  "Deep Dive Summary": "..."
}
```

A structured output parser validates all generated responses before continuing.

---

# Step 5: News Intelligence Agent

### Web Content Analyzer

Role:
News Intelligence Agent

Responsibilities:

* Analyze web search results
* Extract top stories
* Remove citations and noise
* Create structured news entries

Output:

```json
{
  "stories": [
    {
      "headline": "...",
      "content": "..."
    }
  ]
}
```

---

# Step 6: Data Persistence

## Airtable Storage

The workflow stores processed information inside Airtable.

Stored Data:

### YouTube Table

* Title
* Channel
* Views
* Thumbnail
* Quick Summary
* Deep Dive Summary

### News Table

* Headline
* Summary

Purpose:

* Historical trend tracking
* Data persistence
* Future analysis

---

# Step 7: Aggregation and Synchronization

## Aggregate Node

Purpose:

Collect all processed content into a single package.

Reason:

The report generation agent must analyze patterns across multiple data sources simultaneously.

Without aggregation, the AI would only see one item at a time.

## Merge Node

Purpose:

Ensure all workflow branches complete successfully before report generation begins.

Benefits:

* Synchronization
* Data consistency
* Reliable report generation

---

# Step 8: Strategic Intelligence Agent

## Report Generator Agent

Role:
Strategic Intelligence Agent

Responsibilities:

* Analyze all collected data
* Identify emerging patterns
* Generate executive summaries
* Highlight trends
* Create business opportunities
* Generate startup ideas

Output Sections:

### TLDR

Quick overview of the most important developments.

### YouTube Insights

Top trending content and summaries.

### Web Intelligence

Important industry news and updates.

### Business Opportunities

Potential products, services, and startup ideas derived from detected trends.

### Revenue Opportunities

Potential monetization paths based on current market activity.

---

# Agentic Design Principles Demonstrated

This project incorporates several agentic workflow concepts.

## Role Specialization

Different agents perform different responsibilities:

### Content Analysis Agent

Analyzes and summarizes videos.

### News Intelligence Agent

Processes web search results.

### Strategic Intelligence Agent

Identifies patterns and generates opportunities.

---

## Structured Outputs

All AI-generated responses are validated through predefined schemas.

Benefits:

* Reliability
* Consistency
* Easier downstream processing

---

## Tool Usage

The workflow integrates multiple tools:

* YouTube API
* Tavily Search
* Google Gemini
* Groq
* Airtable
* Gmail

---

## AI vs Deterministic Control

### AI Responsibilities

* Summarization
* Trend analysis
* Pattern recognition
* Opportunity generation
* Report creation

### Deterministic Responsibilities

* Filtering
* Validation
* Aggregation
* Routing
* Synchronization
* Storage

---

## Workflow Diagram

```text
Manual Trigger
      |
      v
YouTube Search ------------ Tavily Search
      |                           |
      v                           v
Metadata Collection        News Processing
      |                           |
      v                           v
Content Analysis Agent     News Agent
      |                           |
      +------------+--------------+
                   |
                   v
             Aggregate
                   |
                   v
                Merge
                   |
                   v
        Strategic Intelligence Agent
                   |
                   v
             HTML Report
                   |
                   v
             Gmail Delivery
```

---

# Sample Output

The generated report contains:

* Daily trend summary
* Top YouTube insights
* Industry news
* Key takeaways
* Startup opportunities
* Revenue ideas

The report is automatically delivered via email and can be reviewed in under five minutes.

---

# Challenges Faced

## Transcript API Limitations

Initially, the workflow used YouTube transcript extraction.

However, the transcript API reached its free-tier limits.

To overcome this limitation, I built a metadata intelligence layer that uses:

* Video titles
* Descriptions
* Tags
* Timestamps
* Channel metadata

This still provides enough context for meaningful AI analysis.

## Social Media API Restrictions

The original vision included:

* Reddit
* Twitter/X

However:

* Reddit introduced API restrictions
* Twitter/X APIs were costly

For the current version, Tavily Search was used as a cost-effective alternative.

---

# Future Improvements

Planned enhancements include:

* Reddit integration
* Twitter/X integration
* Trend scoring system
* Sentiment analysis
* Startup opportunity ranking
* Personalized niche profiles
* Weekly and monthly reports
* Market demand forecasting

---

# Technologies Used

* n8n
* Google Gemini
* Groq LLM
* YouTube Data API
* Tavily Search
* Airtable
* Gmail

---

# Repository Contents

* README.md
* n8n Workflow JSON
* Workflow Screenshots
* Sample Output Report
* Assignment Video Demonstration

---

# Conclusion

This project demonstrates how agentic workflows can transform large volumes of online content into actionable intelligence.

By combining AI reasoning with deterministic workflow control, the system automates trend discovery, content analysis, and opportunity generation while significantly reducing the manual effort required to stay informed about rapidly evolving industries.
