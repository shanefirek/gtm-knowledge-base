# PostHog Tracking & SEO Implementation

**Category:** SEO, Growth, BFS  
**Created by:** Shane O'Malley Firek  
**Owner:** Shane Firek (Head of Growth)  
**Developer Assigned:** Amrit  
**Date:** September 4th, 2025

---

## Part 1. Conversion Event Tracking (PostHog)

**Goal:** Capture critical buyer → seller actions (form submissions, phone clicks) and seller listing journey events for conversion attribution & funnel analysis.

### 1. Buyer → Seller Conversion Events

#### A. Contact Form Submissions

- **Event Name:** `contact_seller_boat`
- - **Trigger:** On submit of contact form on a boat listing.
  - - **Payload:**
   
    - ```javascript
      posthog.capture('contact_seller_boat', {
        boat_id: boat.id,
        boat_make: boat.make,
        boat_model: boat.model,
        price: boat.price,
        seller_type: boat.seller_type
      });
      ```

      #### B. Phone Number Clicks

      - **Event Name:** `call_click_seller`
      - - **Trigger:** On click/tap of seller phone number.
        - - **Payload:**
         
          - ```javascript
            posthog.capture('call_click_seller', {
              boat_id: boat.id,
              phone_number: seller.phone
            });
            ```

            ### 2. Seller Journey Events (Revenue Funnel)

            #### A. Listing Started

            - **Event Name:** `listing_started`
            - - **Trigger:** Seller begins listing process.
              - - **Payload:**
               
                - ```javascript
                  posthog.capture('listing_started', {
                    step: 'basic_info'
                  });
                  ```

                  #### B. Photo Upload Step

                  - **Event Name:** `listing_photo_upload`
                  - - **Trigger:** Seller uploads one or more photos.
                    - - **Payload:**
                     
                      - ```javascript
                        posthog.capture('listing_photo_upload', {
                          step: 'photos',
                          photos_uploaded: count
                        });
                        ```

                        #### C. Listing Published

                        - **Event Name:** `listing_published`
                        - - **Trigger:** Seller completes process and listing goes live.
                          - - **Payload:**
                           
                            - ```javascript
                              posthog.capture('listing_published', {
                                boat_make: make,
                                boat_model: model,
                                price: price
                              });
                              ```

                              ### Implementation Notes (PostHog)

                              - Use `snake_case` for event names.
                              - - Payloads should only include serializable values.
                                - - Include `distinct_id` = user ID/session ID if available for attribution.
                                  - - Validate events in PostHog Live View on staging before prod.
                                    - - Growth team will configure funnels:
                                      -   - **Buyer Funnel:** `contact_seller_boat` + `call_click_seller`
                                          -   - **Seller Funnel:** `listing_started` → `listing_photo_upload` → `listing_published`
                                           
                                              - ---

                                              ## Part 2. Breadcrumb Schema Fix (SEO)

                                              **Goal:** Resolve Google Search Console error "Either name or item.name should be specified" to restore breadcrumb rich results in SERPs.

                                              ### Current Issue

                                              Breadcrumb JSON-LD is missing the `name` property in `itemListElement`. Example of broken markup:

                                              ```json
                                              {
                                                "@type": "ListItem",
                                                "position": 2,
                                                "item": {
                                                  "@id": "https://www.boatsforsale.com/buy/state-FL"
                                                }
                                              }
                                              ```

                                              ### Correct Format Example (Florida State Page)

                                              ```html
                                              <script type="application/ld+json">
                                              {
                                                "@context": "https://schema.org",
                                                "@type": "BreadcrumbList",
                                                "itemListElement": [
                                                  {
                                                    "@type": "ListItem",
                                                    "position": 1,
                                                    "name": "Home",
                                                    "item": "https://www.boatsforsale.com/"
                                                  },
                                                  {
                                                    "@type": "ListItem",
                                                    "position": 2,
                                                    "name": "Buy",
                                                    "item": "https://www.boatsforsale.com/buy"
                                                  },
                                                  {
                                                    "@type": "ListItem",
                                                    "position": 3,
                                                    "name": "Florida",
                                                    "item": "https://www.boatsforsale.com/buy/state-FL"
                                                  }
                                                ]
                                              }
                                              </script>
                                              ```

                                              ### Dynamic Rules

                                              - Always include `name` for each ListItem.
                                              - - `item` should match the canonical URL.
                                                - - Use human-readable names (e.g., "Florida," "Miami," "Center Console").
                                                  - - Include one BreadcrumbList per page.
                                                   
                                                    - ### Example Variants
                                                   
                                                    - - **City Page:** `/buy/state-FL/city-miami` → add `"name": "Miami"`.
                                                      - - **Type Page:** `/buy/state-FL/type-center-console` → add `"name": "Center Console"`.
                                                       
                                                        - ### Next Steps (SEO)
                                                       
                                                        - 1. Update schema generator to inject `name` dynamically.
                                                          2. 2. Test with Google Rich Results tool.
                                                             3. 3. Re-deploy & validate fix in GSC.
                                                               
                                                                4. ---
                                                               
                                                                5. ## Deliverables
                                                               
                                                                6. - [ ] Implement PostHog events (contact, call, seller funnel).
                                                                   - [ ] - [ ] Update breadcrumb schema across `/buy/state-*` and nested pages.
                                                                   - [ ] - [ ] QA in staging (PostHog debugger + Rich Results test).
                                                                   - [ ] - [ ] Push to production.
                                                                   - [ ] - [ ] Growth team validates GSC & PostHog reporting.
                                                                  
                                                                   - [ ] ✅ With this doc, Amrit has the full blueprint to fix **conversions + breadcrumbs** in one sprint.
