# Tech Trend Keyword Extractor

An end-to-end automation built with **n8n** that scrapes trending topics and content signals from seven different sources developer communities, search engines, and top-ranking web pages and stores the cleaned, deduplicated results in Google Sheets for trend research.

The workflow combines **Hacker News**, **Reddit**, **GitHub**, **Google/Bing/YouTube Autocomplete**, and **SERP scraping (Zenserp)** to build a multi-source dataset of what's trending in tech, with a focus on the AI / vibe-coding tools space.

---

## How It Works

The automation runs on manual trigger and fans out into **7 parallel branches**, each following the same pattern: **fetch → parse → append to sheet → wait → dedupe → clear sheet → rewrite clean data**.

- **Hacker News** Fetches the current top story IDs from HN's Firebase API, retrieves each story's title, score, comment count, and URL.
- **Reddit** Pulls the top 100 posts of the week from r/programming and extracts title, score, comments, and URL.
- **GitHub** Searches for repositories with 500+ stars pushed recently, sorted by stars, extracting name, description, star count, language, and URL.
- **Google Autocomplete** Queries Google's suggestion API against a fixed list of ~25 seed keywords (e.g. "vibe coding," "ai app builder," "cursor ai," "lovable ai") to surface related search demand.
- **Bing Autocomplete** Same seed keywords against Bing's suggestion endpoint.
- **YouTube Autocomplete** Same seed keywords against YouTube's suggestion endpoint to catch video-specific search trends.
- **Top Ranked Websites** Uses Zenserp to pull organic Google search results for the seed keywords, filters out low-signal domains (Reddit, Forbes, LinkedIn, Medium, Twitter, YouTube), fetches the remaining pages, and strips the HTML down to plain text content for analysis.

Each branch re-reads its own sheet after appending, removes duplicate entries (by title or content), and rewrites a clean version back so re-running the workflow never accumulates duplicate rows.

---

## Technologies Used

- n8n
- Hacker News API
- Reddit API
- GitHub REST API
- Google / Bing / YouTube Autocomplete endpoints
- Zenserp (SERP API)
- Google Sheets API
- JavaScript (Code nodes)
- HTML-to-text extraction

---
