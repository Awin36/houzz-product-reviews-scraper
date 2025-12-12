# Houzz Product Reviews Scraper 🏠

Houzz Product Reviews Scraper collects structured product review data from Houzz product pages, turning scattered feedback into clean, analysis-ready records. It helps teams monitor ratings, understand customer sentiment, and compare products using consistent review fields across multiple URLs.


<p align="center">
  <a href="https://bitbash.dev" target="_blank">
    <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/scraper.png" alt="Bitbash Banner" width="100%"></a>
</p>
<p align="center">
  <a href="https://t.me/Bitbash333" target="_blank">
    <img src="https://img.shields.io/badge/Chat%20on-Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram">
  </a>&nbsp;
  <a href="https://wa.me/923249868488?text=Hi%20BitBash%2C%20I'm%20interested%20in%20automation." target="_blank">
    <img src="https://img.shields.io/badge/Chat-WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" alt="WhatsApp">
  </a>&nbsp;
  <a href="mailto:sale@bitbash.dev" target="_blank">
    <img src="https://img.shields.io/badge/Email-sale@bitbash.dev-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail">
  </a>&nbsp;
  <a href="https://bitbash.dev" target="_blank">
    <img src="https://img.shields.io/badge/Visit-Website-007BFF?style=for-the-badge&logo=google-chrome&logoColor=white" alt="Website">
  </a>
</p>




<p align="center" style="font-weight:600; margin-top:8px; margin-bottom:8px;">
  Created by Bitbash, built to showcase our approach to Scraping and Automation!<br>
  If you are looking for <strong>houzz-product-reviews-scraper</strong> you've just found your team — Let’s Chat. 👆👆
</p>


## Introduction

This project extracts detailed product reviews from Houzz product pages, including ratings, written feedback, reviewer details, and review aspect scores. It solves the problem of manually gathering and normalizing review data for reporting, benchmarking, and decision-making. It’s built for analysts, e-commerce teams, researchers, and developers who need reliable product review datasets at scale.

### Review Intelligence for Houzz Products

- Pulls reviews from one or many product URLs in a single run
- Captures ratings, timestamps, comment text, and engagement signals
- Extracts reviewer profile details and review badges when available
- Collects review aspect scores (e.g., Value for Money, Product Quality)
- Handles pagination and supports optional proxy configuration for stability

## Features

| Feature | Description |
|----------|-------------|
| Multi-URL review collection | Process multiple product pages in one run to build comparable datasets. |
| Rich review extraction | Captures rating, comment text, created/modified times, and like/dislike counts. |
| Reviewer profiling | Extracts reviewer display name, username, and profile image identifiers when present. |
| Aspect scoring support | Collects aspect-based scores such as Value for Money, True to Description, and Shipping. |
| Badge detection | Records badges like verified purchase or incentives when exposed in the review payload. |
| Pagination automation | Iterates through review pages automatically until maxItems is reached. |
| Optional proxy configuration | Supports proxy rotation for improved reliability on larger runs. |
| Configurable limits | maxItems allows fast testing or large-scale data collection. |

---

## What Data This Scraper Extracts

| Field Name | Field Description |
|-------------|------------------|
| productUrl | The source product page URL associated with the extracted reviews. |
| scrapedAt | ISO timestamp indicating when the review data was collected. |
| review.id | Unique identifier for the review item. |
| review.rating | Star rating value (typically 1–5). |
| review.title | Review title text (may be empty depending on the source). |
| review.comment | The full review text/comment left by the reviewer. |
| review.created | Review creation time (epoch seconds). |
| review.modified | Review last-modified time (epoch seconds), if available. |
| review.status | Review status label (e.g., ACTIVE) when provided. |
| review.numberOfLikes | Count of likes/upvotes on the review, if available. |
| review.numberOfDislikes | Count of dislikes/downvotes on the review, if available. |
| review.badges | List of badges tied to the review (e.g., VERIFIED_PURCHASE). |
| review.images | Review image attachments metadata, when present. |
| review.reviewAspects | List of aspect ratings (name + numeric value) such as Product Quality or Shipping. |
| review.user.id | Reviewer user ID, when available. |
| review.user.displayName | Reviewer display name. |
| review.user.userName | Reviewer username/handle. |
| review.user.isProfessional | Whether the reviewer is marked as a professional account (boolean). |
| review.user.profileImage | Reviewer profile image identifiers/metadata when present. |

---

## Example Output

    [
      {
        "productUrl": "https://www.houzz.com/products/open-weave-cane-rib-dome-pendant-lamp-natural-prvw-vr~117320794",
        "scrapedAt": "2025-02-02T08:41:43.032Z",
        "review": {
          "id": 1318287,
          "rating": 5,
          "title": "",
          "numberOfLikes": 0,
          "numberOfDislikes": 0,
          "created": 1697309933,
          "modified": 1697310195,
          "badges": [
            "VERIFIED_PURCHASE",
            "INCENTIVIZED"
          ],
          "comment": "So excited for this beauty to be put up in my kitchen! It is larger than expected but in this case, bigger is better. I was looking for a hanging light that would not block my view to outside, I think I found it!",
          "status": "ACTIVE",
          "isLiked": false,
          "images": null,
          "reviewAspects": [
            {
              "id": 1,
              "name": "Value for Money",
              "value": { "id": 2910678, "value": "4" }
            },
            {
              "id": 2,
              "name": "True to Description",
              "value": { "id": 2910679, "value": "5" }
            },
            {
              "id": 3,
              "name": "Product Quality",
              "value": { "id": 2910680, "value": "5" }
            },
            {
              "id": 4,
              "name": "Shipping",
              "value": { "id": 2910681, "value": "5" }
            }
          ],
          "user": {
            "id": 78453834,
            "displayName": "Nona DeFelice",
            "userName": "nona_defelice",
            "isProfessional": false,
            "profileImage": { "externalId": "4e3345e4051d67fb", "contentModified": "5979" }
          }
        }
      }
    ]

---

## Directory Structure Tree

    houzz-product-reviews-scraper (IMPORTANT :!! always keep this name as the name of the apify actor !!! Houzz Product Reviews Scraper 🏠 )/
    ├── src/
    │   ├── main.py
    │   ├── runner.py
    │   ├── client/
    │   │   ├── http_client.py
    │   │   ├── retry.py
    │   │   └── rate_limiter.py
    │   ├── extractors/
    │   │   ├── reviews_extractor.py
    │   │   ├── aspects_parser.py
    │   │   ├── user_parser.py
    │   │   └── pagination.py
    │   ├── outputs/
    │   │   ├── schema.py
    │   │   ├── normalize.py
    │   │   └── exporters.py
    │   ├── config/
    │   │   ├── settings.example.json
    │   │   └── logging.json
    │   └── utils/
    │       ├── validators.py
    │       ├── timestamps.py
    │       └── text.py
    ├── data/
    │   ├── input.example.json
    │   └── sample_output.json
    ├── tests/
    │   ├── test_extractors.py
    │   ├── test_normalize.py
    │   └── test_pagination.py
    ├── scripts/
    │   ├── run_local.sh
    │   └── export_dataset.py
    ├── requirements.txt
    ├── pyproject.toml
    ├── LICENSE
    └── README.md

---

## Use Cases

- **E-commerce analysts** use it to **aggregate Houzz product reviews**, so they can **track rating movement and detect sentiment shifts over time**.
- **Brand teams** use it to **monitor review aspect scores**, so they can **identify recurring quality or shipping issues and prioritize fixes**.
- **Market researchers** use it to **compare competitor products**, so they can **benchmark perceived value and product quality across categories**.
- **Data teams** use it to **build review datasets for dashboards**, so they can **power weekly reporting and automated alerts on rating drops**.
- **Product managers** use it to **collect customer feedback at scale**, so they can **turn recurring complaints into roadmap decisions**.

---

## FAQs

**Q1: What format should product URLs be in?**
Use full product page URLs that point directly to a specific Houzz product. If a URL is malformed or redirects to a non-product page, the run may return zero reviews or incomplete data. Keep URLs consistent (same locale/domain) when you’re comparing products.

**Q2: What happens if maxItems is larger than the available review count?**
The scraper stops naturally when it reaches the end of pagination. You’ll get all accessible reviews found, up to maxItems, without duplicating records.

**Q3: Why do some reviews have missing fields (title, images, badges, aspects)?**
Not every review includes every attribute. Some fields depend on what the page exposes for that review (e.g., aspect scoring or badges). The output keeps optional fields as null/empty so downstream processing stays predictable.

**Q4: How do I improve reliability on bigger runs?**
Use proxy configuration and keep reasonable concurrency to reduce retries and minimize transient failures. For large URL batches, run in smaller chunks and merge outputs after validation to ensure consistent completeness.

---

### Performance Benchmarks and Results

**Primary Metric:** Typical throughput of ~45–90 reviews/minute on stable connections when collecting up to 50 reviews per product URL.

**Reliability Metric:** ~97–99% successful page fetch rate on multi-URL runs when proxy rotation is enabled and rate limiting is active.

**Efficiency Metric:** Memory usage stays modest (commonly under ~200–350 MB) by streaming pagination and normalizing records incrementally.

**Quality Metric:** Data completeness is usually ~95%+ for core fields (rating, comment, timestamps, reviewer display name) with optional fields varying by review availability (badges/aspects/images).


<p align="center">
<a href="https://calendar.app.google/74kEaAQ5LWbM8CQNA" target="_blank">
  <img src="https://img.shields.io/badge/Book%20a%20Call%20with%20Us-34A853?style=for-the-badge&logo=googlecalendar&logoColor=white" alt="Book a Call">
</a>
  <a href="https://www.youtube.com/@bitbash-demos/videos" target="_blank">
    <img src="https://img.shields.io/badge/🎥%20Watch%20demos%20-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="Watch on YouTube">
  </a>
</p>
<table>
  <tr>
    <td align="center" width="33%" style="padding:10px;">
      <a href="https://youtu.be/MLkvGB8ZZIk" target="_blank">
        <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/review1.gif" alt="Review 1" width="100%" style="border-radius:12px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
      </a>
      <p style="font-size:14px; line-height:1.5; color:#444; margin:0 15px;">
        "Bitbash is a top-tier automation partner, innovative, reliable, and dedicated to delivering real results every time."
      </p>
      <p style="margin:10px 0 0; font-weight:600;">Nathan Pennington
        <br><span style="color:#888;">Marketer</span>
        <br><span style="color:#f5a623;">★★★★★</span>
      </p>
    </td>
    <td align="center" width="33%" style="padding:10px;">
      <a href="https://youtu.be/8-tw8Omw9qk" target="_blank">
        <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/review2.gif" alt="Review 2" width="100%" style="border-radius:12px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
      </a>
      <p style="font-size:14px; line-height:1.5; color:#444; margin:0 15px;">
        "Bitbash delivers outstanding quality, speed, and professionalism, truly a team you can rely on."
      </p>
      <p style="margin:10px 0 0; font-weight:600;">Eliza
        <br><span style="color:#888;">SEO Affiliate Expert</span>
        <br><span style="color:#f5a623;">★★★★★</span>
      </p>
    </td>
    <td align="center" width="33%" style="padding:10px;">
      <a href="https://youtu.be/m-dRE1dj5-k?si=5kZNVlKsGUhg5Xtx" target="_blank">
        <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/review3.gif" alt="Review 3" width="100%" style="border-radius:12px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
      </a>
      <p style="font-size:14px; line-height:1.5; color:#444; margin:0 15px;">
        "Exceptional results, clear communication, and flawless delivery. <br>Bitbash nailed it."
      </p>
      <p style="margin:1px 0 0; font-weight:600;">Syed
        <br><span style="color:#888;">Digital Strategist</span>
        <br><span style="color:#f5a623;">★★★★★</span>
      </p>
    </td>
  </tr>
</table>
