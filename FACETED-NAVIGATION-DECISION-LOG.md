# Faceted Navigation — Initial Decision Log

## Problem
Location, Job Type, Experience Level and Work Mode filters can generate many query URLs. Most are filtered views of the same category inventory rather than unique landing pages.

## Options
1. Index every combination: can target long-tail demand if content is unique, but risks thin/duplicate pages, index bloat and crawl expansion.
2. Canonical filtered URLs to clean category: consolidates duplicate signals and indicates preferred URL; canonical is a hint, not a directive, and URLs may still be crawled.
3. Noindex filtered URLs: excludes low-value combinations from indexing when honored, but does not prevent crawling and persistent noindex may affect link discovery.

## Initial recommendation
For this practice site, canonicalize query-string filter variants to their clean category URL because they are filtered views of the same inventory. Keep five clean category pages indexable and self-canonical. If a filter combination merits search traffic and unique content, build a dedicated static landing page with its own self-canonical. Verify deployed behavior before reporting completion.
