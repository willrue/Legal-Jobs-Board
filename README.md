# Legal Jobs Board

This repository currently contains a working dashboard prototype in [index.html](index.html), with its records stored separately in [jobs.json](jobs.json).

## Preview locally

From the project folder, run:

```bash
python3 -m http.server 8000
```

Then open [http://localhost:8000](http://localhost:8000) in a browser.

The current prototype includes:

- Active, further-opportunity, and archived role views
- Search, sector, location, work-model, experience, and sort filters
- Role details dialogs
- Links to the original job postings
- Embedded job data from the September 1, 2026 baseline

The page now loads the records from `jobs.json`, so future refreshes can update the dataset without editing the interface.

The Admin tab is currently a local prototype: added roles, removals, and tab moves are stored in this browser only. URL submission infers basic details from the URL and requires approval before adding the record. A backend and server-side extractor are required before changes can be shared with other users or arbitrary pages can be scraped reliably.

## Planned build stages

1. Clean the single-file prototype and move the embedded job data into a separate data file.
2. Add a real backend and database so jobs are no longer stored in the page.
3. Add secure login and saved searches.
4. Add scheduled updates from approved APIs, feeds, or permitted employer career pages.
5. Deploy the application with backups, monitoring, and a clear source-attribution policy.

Automatic scraping should respect each source's terms of service, robots rules, rate limits, and access controls. Official APIs and feeds are preferred.

## Important

This is not a production system yet. The HTML contains the complete job dataset and should not contain passwords, API keys, or other secrets.