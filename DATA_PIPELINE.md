# Jobs Data Pipeline

The main product goal is a current, trustworthy board of relevant legal roles. Login is optional and comes later.

## Target flow

```text
Approved sources -> Fetch -> Parse -> Normalize -> Relevance rules -> Deduplicate
    -> Verify posting -> Publish active roles -> Recheck -> Archive expired roles
```

## First version

Start with sources that provide stable, permitted access:

- Official employer career pages
- Greenhouse, Ashby, Workable, and similar public employer feeds
- Government or public job APIs
- User-supplied roles for confidential or hard-to-access positions

Avoid broad scraping until a source's terms, robots rules, rate limits, and access method are understood. Prefer APIs, feeds, or structured career-board endpoints.

## Job record

Each role should have:

- `source` and stable source identifier
- `sourceUrl` and `lastCheckedAt`
- company, title, location, work model, experience, and practice sectors
- description, salary when available, and posted date
- `status`: active, expired, or needs-review
- `firstSeenAt`, `lastSeenAt`, and `expiredAt`
- a relevance decision and reason

## Relevance rules

The first rules should be explicit and reviewable rather than hidden in AI output:

- Legal, compliance, privacy, regulatory, transactions, litigation, or related roles
- Target seniority and experience ranges
- Target geographies and remote eligibility
- Target sectors such as technology, financial services, life sciences, energy, real estate, and consumer
- Exclude duplicates, non-legal roles, closed postings, and low-confidence matches

AI can help classify descriptions, but it should produce a reason and confidence score. A human review queue should handle uncertain matches.

## Expiry rules

A role should be rechecked on a schedule. Mark it `needs-review` after a failed or ambiguous check, and archive it only when the posting is confirmed closed, removed, or repeatedly unavailable. Keep the historical record and show the original source and dates.

## Efficient build order

1. Extract the current records into a structured dataset without changing the visual board. Completed: records now live in `jobs.json`.
2. Add one compliant source adapter and a manual refresh command.
3. Add relevance, duplicate, link-check, and expiry processing.
4. Store the normalized records in a hosted database.
5. Schedule the refresh job and add a small review/admin view.
6. Add login only if private saved searches or restricted roles require it.
