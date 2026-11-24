# Free Lead-Enrichment Waterfall for Clay & Make (Zero Runaway Crawl Bills)

> **Note:** Keep this template strictly off-platform (GitHub, n8n community, Clay guides, `quitegoodproject.com`) — never paste external links inside Apify Store listings.

## Workflow 1: Enrich Any Google Maps Export Inside Apify
1. Run Google Maps Scraper (`compass/crawler-google-places`) on your target city + trade.
2. Copy the **Dataset ID** of the finished run.
3. Call `tarquin/flat-cap-contact-scraper` with:
   ```json
   {
     "sourceDatasetId": "YOUR_MAPS_DATASET_ID",
     "maxPagesPerDomain": 4,
     "verifyEmails": true
   }
   ```
4. Export only rows where `verifiedEmails.length > 0`.

## Workflow 2: High-Volume Direct HTTP API Column in Clay (For 50k+ Rows/Month)
Add an **HTTP API** enrichment column in Clay for sub-cent verification & scraping without Apify middleman markup:

### Option A — SMTP/M365 Email Verification (`TokenVerify`)
- **Method:** `POST`
- **Endpoint:** `https://tokenverifyapi.com/v1/verify/email`
- **Headers:**
  ```json
  {
    "Content-Type": "application/json",
    "Authorization": "Bearer {{QGP_TOKENVERIFY_KEY}}"
  }
  ```
- **Body:**
  ```json
  {
    "email": "{{Email}}"
  }
  ```
- **Keep rows where:** `deliverable == true` and `is_catch_all == false`.
- **Get API Key:** `https://tokenverifyapi.com/#pricing` (free sandbox / `$10` 10k non-expiring credit pack)

### Option B — Clean Markdown Website Scrape (`TokenMarkdown`)
- **Method:** `POST`
- **Endpoint:** `https://tokenmarkdown.com/v1/extract`
- **Headers:**
  ```json
  {
    "Content-Type": "application/json",
    "Authorization": "Bearer {{QGP_TOKENMARKDOWN_KEY}}"
  }
  ```
- **Body:**
  ```json
  {
    "url": "{{Website}}",
    "mode": "clean"
  }
  ```
- **Get API Key:** `https://tokenmarkdown.com/#pricing` (`https://quitegoodproject.com/` overview)
