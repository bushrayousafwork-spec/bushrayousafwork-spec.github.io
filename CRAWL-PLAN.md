# Screaming Frog Crawl Plan

Crawl the deployed Github homepage in Spider mode. Export Internal > HTML, Response Codes > Client Error (4xx), Redirection (3xx), Page Titles, Meta Description, H1, Canonicals and Directives; export Redirect Chains if available. Preserve raw CSV exports. Validate JobPosting structured data separately with Rich Results Test or Schema Markup Validator.

## Faceted URL cap
Each of five category pages links to eight filtered variants: 2 location-only (Remote, Lahore), 2 job-type-only (Full-time, Contract), 1 experience-only (Junior), 1 work-mode-only (Hybrid), 2 combinations (Remote + Full-time; Lahore + Mid-level). Total = 40 filtered variants + 5 clean category URLs = 45 category URLs. The form supports four dimensions, but only the selected combinations are linked for crawling to remain below Screaming Frog's free 500-URL limit.

Sitemap is intentionally incomplete in the baseline. Pages should also be discoverable through internal links.
