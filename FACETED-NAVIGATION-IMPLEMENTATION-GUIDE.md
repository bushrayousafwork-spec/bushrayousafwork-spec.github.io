TalentHub Careers — Faceted Navigation Implementation Guide

Core rule: Allow users to filter jobs through URL parameters, but keep every filtered URL canonicalized to its single clean category URL so filters never become separate indexable pages.

1. How Filtering Works and Which URLs Are Crawlable

The job board provides four filters across five job categories:

- Location ("location")
- Job Type ("type")
- Experience Level ("level")
- Work Mode ("workmode")

The shared JavaScript file "/assets/js/filters.js" reads the selected values, filters matching job cards, updates the result count, and updates the browser URL using query parameters.

Example filtered URL:

"/categories/technology/?location=Remote"

Multiple filters can be combined:

"/categories/technology/?location=Remote&type=Contract"

The implementation supports filter persistence after refresh, Reset functionality, and browser Back/Forward navigation.

Each category includes eight selected filtered links for controlled crawl testing. The five clean category URLs are the crawlable indexable category pages. Filtered variations are accessible to users and can be crawled, but should not be indexed as separate pages. Filtered URLs are excluded from the XML sitemap.
These eight filtered links per category are deliberate test links used to expose representative query-string URLs to Screaming Frog during controlled crawl testing. Once testing is complete, remove these standalone test links from production HTML, or retain filtering as user-only navigation through the filter controls. Do not expand the test links into a large crawlable set of filter combinations.

2. Canonical Rule and Duplicate Content Prevention

Each category has one clean, self-referencing canonical URL. All filtered variations must retain that category's clean canonical target.

For example:

Filtered URL:

"/categories/technology/?location=Remote"

Canonical:

<link rel="canonical" href="https://bushrayousafwork-spec.github.io/categories/technology/">

The canonical tag is included directly in the static HTML "<head>" of each category page, not injected by JavaScript.

Canonical targets:

- Technology: "/categories/technology/"
- Design: "/categories/design/"
- Marketing: "/categories/marketing/"
- Customer Support: "/categories/customer-support/"
- Finance: "/categories/finance/"
Verification: Open a filtered category URL (e.g., /categories/technology/?location=Remote), view the page source, and confirm that the canonical tag points to https://bushrayousafwork-spec.github.io/categories/technology/.

Important: Filter combinations must never receive their own canonical URLs. All filtered versions of a category point to that category's single clean URL. This consolidates duplicate URL variations and keeps the preferred category URL clear to search engines.

Future rule: Any new filter added to the category pages must follow the same canonical rule. It must not create its own canonical URL or a separate indexable URL. All filtered combinations must remain canonicalized to the clean category URL.

Screaming Frog Verification Results:
The controlled crawl confirmed the canonical implementation:
Total canonical URLs: 65
Self-referencing URLs: 25
Incorrect filtered canonical targets: 0 
All 40 filtered URLs were canonicalised to their respective clean category URLs. No incorrect filtered canonical targets were found .
Crawl date : 20 Nov,2026 

3. Hosting Limitation, Redirect Chain and Noindex

Two test pages were created to demonstrate an intended redirect chain:

/old-job/ -- 301-->/temporary-job/ --301--> /jobs/seo-executive/
                                

The intended rules are documented in the repository's "_redirects" configuration. However, the project is hosted on GitHub Pages, which does not natively process Netlify-style "_redirects" rules or "netlify.toml". Therefore, these redirects are not live. Both test URLs currently return their own HTML pages with HTTP 200 responses.

To prevent these test pages from being indexed, both contain:

<meta name="robots" content="noindex,follow">

Both URLs are excluded from the XML sitemap, and the noindex directives have been verified in their live HTML source.

While the site remains hosted on GitHub Pages, keep the noindex directives on both test pages because the platform does not serve the configured HTTP 301 redirects. Only replace the noindex directives with the redirect chain when the site is hosted on a platform that supports and serves real HTTP 301 redirects.
