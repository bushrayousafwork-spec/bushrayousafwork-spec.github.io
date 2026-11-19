Faceted Navigation — Architecture Decision Log

Project: TalentHub Careers
Decision ID: ADR-01
Date: 19 November 2026
Decision Status: Implemented and Verified

1. Problem and Context

TalentHub Careers has five category pages with filters for Location, Job Type, Experience Level, and Work Mode.

These filters generate query-parameter URLs. Most filtered URLs represent variations of the same category inventory rather than unique search landing pages.

Allowing every filter combination to become independently indexable could create thin or duplicate pages, increase index bloat, and expand unnecessary crawling.

However, some combinations may represent valuable long-tail search opportunities, such as "remote junior technology jobs".

The architectural decision must balance technical SEO health against potential organic search visibility.

2. Options Considered

Option A — Index Every Filter Combination

Allow all parameter-based filter URLs to be independently indexed.

Advantages:

- Potential to target specific long-tail search queries.
- Could capture search demand for combinations of location, job type, level, and work mode.

Disadvantages:

- Risks thin or duplicate content.
- Can increase index bloat and crawl expansion.
- Requires unique, useful content and ongoing management for individual combinations.

Option B — Canonicalise Filtered URLs to Clean Category URLs

Add a canonical link on each filtered URL pointing to its corresponding clean parent category URL.

Advantages:

- Consolidates canonical signals toward preferred category URLs.
- Reduces the risk of duplicate indexable filter combinations.
- Keeps the five main category pages as preferred organic landing pages.
- Preserves filter functionality for website visitors.

Disadvantages:

- Canonical is a search-engine hint, not an absolute directive.
- Filtered URLs may still be crawled.
- Parameter URLs are not intended to rank independently.
- The site sacrifices the immediate opportunity for those filtered URLs to rank separately for long-tail searches.

Option C — Apply Noindex, Follow

Apply a noindex directive to filtered combinations.

Advantages:

- Prevents filtered URLs from appearing in search results when the directive is respected.
- Can be appropriate for low-value filtered pages.

Disadvantages:

- Does not consolidate canonical signals to the clean parent category in the same way.
- Does not prevent crawling.
- Requires monitoring to ensure the directive remains accessible to search engines.

Option D — Block Filter URLs in robots.txt

Prevent search engines from crawling parameter-based URLs.

Advantages:

- Can reduce crawling of blocked URL patterns.

Disadvantages:

- Search engines may not be able to crawl the blocked page and see its canonical directive.
- Blocking URLs does not guarantee that their URLs will never appear in search results.
- It is not suitable as the primary duplicate-consolidation solution for this implementation.

3. Architectural Decision

Choice Made: Canonicalise all parameter-based filter URLs combining "type", "location", "level", and "workmode" back to their respective clean parent category URLs.

Why This Was Chosen:

The five category pages contain filter combinations representing variations of the same job inventory. Canonicalisation consolidates canonical signals toward the preferred clean category URLs and reduces the risk of index bloat caused by thin, duplicate, or low-value filter permutations.

4. Trade-offs and Business Impact

Advantages:

- Reduces the risk of duplicate indexation.
- Consolidates canonical signals toward the five clean category pages.
- Avoids treating every filter combination as an independent organic landing page.
- Preserves the filter experience for users.

Disadvantages and SEO Opportunity Cost:

- We intentionally sacrifice the opportunity for parameter-based filtered URLs to rank independently for high-intent long-tail queries.
- For example, searches such as "remote junior technology jobs" may have specific organic search demand.
- Search engines are signalled to prefer the broader Technology category URL instead of the filtered parameter URL.
- As a result, the broad category page may not satisfy every specific long-tail search intent as effectively as a dedicated landing page could.

Future Opportunity:

If a filter combination demonstrates meaningful search demand and can support unique, useful content, it can be developed into a dedicated static landing page with its own self-referencing canonical.

This would allow the website to target valuable long-tail searches without indexing every possible filter combination.

5. Why Canonicalisation Was Preferred Over Noindex

Noindex can exclude filtered pages from search results when respected, but it does not consolidate canonical signals toward the clean parent category URL.

Canonicalisation better matches the current website architecture because filtered URLs represent variations of the same category inventory.

The objective is to retain the clean category pages as preferred indexable URLs while preserving user-facing filter functionality.

6. Implementation and Verification

The selected approach was implemented and checked using Screaming Frog and page-source inspection.

Latest post-fix crawl: 19 November 2026

- Total URLs containing canonical elements: 65
- Self-referencing canonical URLs: 25
- Canonicalised URLs: 40
- Incorrect filtered canonical targets found in the supplied verification: 0

The 40 filtered URLs were distributed across five category pages:

Category| Filtered URLs verified
Design| 8
Technology| 8
Customer Support| 8
Marketing| 8
Finance| 8
Total| 40

All 40 filtered URLs correctly canonicalise to their respective clean parent category URLs.

The five clean category pages remain the preferred indexable versions.

7. Final Decision and Review Conditions

Final Decision: Canonicalisation of parameter-based filtered URLs.

Status: Implemented and verified.

The decision prioritises canonical consolidation and controlled indexation over independently indexing every filter combination.

This decision should be reviewed if search-demand research identifies valuable long-tail combinations that can support dedicated, unique landing-page content.

Canonical targets should also be rechecked whenever the category filter architecture changes.

8. Evidence

Evidence source: Screaming Frog post-fix crawl and source inspection, 19 November 2026.

Supporting evidence:

- Canonical Audit CSV
- Post-fix Internal HTML CSV
- Category filter URL verification
- Page-source canonical inspection
