# Amrit's SEO Sprint – Metadata, Static Copy, Blog Linking

**Category:** BFS, SEO, Growth  
**Created by:** Shane O'Malley Firek

---

## Sprint Details

- **Dates:** July 23–30, 2025
- - **Owner:** Amrit
  - - **Supports:** Shane, Michelle
    - - **CMS:** WordPress
      - - **Dev Access:** Azure DevOps (read + push)
       
        - ---

        ## Overview

        This sprint focuses on refreshing key metadata and improving static copy across top /buy/ pages — targeting both type- and geo-based slugs. You'll also connect high-value blog content with relevant category pages via internal links to boost authority and crawl depth.

        ---

        ## Sprint Tracks

        ### 1. Edit FAQ for buy/state-FL

        **Florida Boat Buying & Selling FAQ Section**

        Sample FAQ items include:

        **Q: What makes BoatsForSale.com different from other boat marketplaces?**
        A: BoatsForSale.com offers a cleaner, faster, and more transparent way to buy and sell boats—especially in Florida. Listings include verified specs, mobile-friendly design, and smart pricing features powered by our upcoming AI valuation engine.

        **Q: Is BoatsForSale.com focused on Florida?**
        A: Yes. We're relaunching with a Florida-first strategy. That means more verified listings, geo-specific filters, and partnerships with marinas, dealers, and boat sellers throughout the state.

        **Q: How does the AI valuation work?**
        A: Our upcoming AI-powered valuation tool will let you upload photos and specs to get an instant, image-based price range. It's built to bring speed and trust to the selling process. You can list your boat now and be among the first to access it once live.

        **Q: Can I list my boat now?**
        A: Yes. Listing is fast, easy, and optimized for mobile. During our relaunch period, early sellers may qualify for promo pricing and enhanced exposure.

        **Q: What types of boats are listed in Florida?**
        A: You'll find thousands of center consoles, pontoons, fishing boats, yachts, and more—new and used. We work with both individual sellers and trusted dealers across Florida.

        ---

        ## Technical Implementation

        ### FAQ Schema Markup (JSON-LD)

        The sprint includes implementing FAQPage schema markup to enhance search visibility. Example structure:

        ```json
        {
          "@context": "https://schema.org",
          "@type": "FAQPage",
          "mainEntity": [
            {
              "@type": "Question",
              "name": "What makes BoatsForSale.com different from other boat marketplaces?",
              "acceptedAnswer": {
                "@type": "Answer",
                "text": "BoatsForSale.com offers a cleaner, faster, and more transparent way to buy and sell boats—especially in Florida. Listings include verified specs, mobile-friendly design, and smart pricing features powered by our upcoming AI valuation engine."
              }
            },
            {
              "@type": "Question",
              "name": "Is BoatsForSale.com focused on Florida?",
              "acceptedAnswer": {
                "@type": "Answer",
                "text": "Yes. We're relaunching with a Florida-first strategy. That means more verified listings, geo-specific filters, and partnerships with marinas, dealers, and boat sellers throughout the state."
              }
            }
          ]
        }
        ```

        ---

        ## Deliverables

        1. Updated FAQ content for Florida state pages
        2. 2. JSON-LD FAQ schema implementation
           3. 3. Internal linking from blog content to category pages
              4. 4. Metadata optimization for top /buy/ pages
                 5. 5. Static copy improvements for geo-based slugs
