# Sitemap Audit + Planning - BoatsForSale.com - 9/15/25

**Category:** SEO, BFS, Growth  
**Created by:** Shane O'Malley Firek  
**By:** Shane Firek – Head of Digital Growth – shane.firek@twinvee.com  
**Date:** 9/15/2025

---

## Summary

We are addressing Google's poor indexation of BoatsForSale.com pages. Right now, Google is overwhelmed with soft-404s, thin/duplicate location pages and noisy sitemap signals.

The plan is structured in two phases of work, each with its own supporting doc:

### Phase 0 – Indexing Fix Plan
Immediate stabilization.
- Fix status codes (404/410).
- - Clean robots.txt and sitemap index.
  - - Submit a test sitemap (1–2k URLs) and monitor GSC results.
   
    - ### Competitor Sitemap Playbook
    - Long-term architecture modeled on Boat Trader / YachtWorld.
    - - Sharded sitemaps by type (listings, hubs, dealers).
      - - Current vs archive rotation.
        - - Inventory thresholds for hubs.
          - - Compressed .xml.gz files with stable lastmod.
           
            - ---

            ## Why This Matters

            - Google is currently treating many BFS pages as low quality, which suppresses indexation and impressions.
            - - Sitemap churn and canonical mismatches reduce "Indexed from sitemap" credit.
              - - Competitors use a clean, gated, and stable structure — BFS must match this to scale.
               
                - ---

                ## Deliverables This Sprint

                - Phase 0 implementation (404/410 fixes, robots.txt update, clean sitemap index).
                - - Small test sitemap submitted to the correct GSC property.
                  - - Validation via curl commands + GSC reporting.
                    - - Evidence-backed roadmap toward competitor-style sitemap architecture.
                     
                      - ---

                      ## Linked Docs

                      - Sitemap Phase 0 Research + Implementation - 9/15/25
                      - - Competitor Sitemap Playbook (Boat Trader–Style)
