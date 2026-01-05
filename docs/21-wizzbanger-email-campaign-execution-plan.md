# WizzBanger Email Campaign Execution Plan

**Category:** Marketing, BFS, Growth  
**Created by:** Shane O'Malley Firek  
**Prepared by:** Shane Firek | Head of Digital Growth | shane.firek@twinvee.com  
**Date:** September 11, 2025

---

## Objective

Launch a branded email campaign to introduce WizValue as the authoritative valuation tool and drive seller and dealer traffic into BoatsForSale.com. The campaign must balance speed of execution with deliverability safeguards, given the size and condition of existing contact lists.

---

## Campaign Framework

### Structure

Three-touch sequence for each audience segment:
1. Announcement
2. 2. Reminder
   3. 3. Urgency
     
      4. **Timeline:** 5–7 days per campaign wave.
      5. **Daily send volume:** 500–1,000 per inbox/day, scaled gradually.
     
      6. ### Audience Segments
     
      7. - Private Sellers (FSBO, Craigslist, Marketplace)
         - - Dealers & Brokers
           - - General Announcement (newsletter and brand contacts)
            
             - ---

             ## Domains and Sending Lanes

             ### BoatsForSale.com (existing, semi-warm):
             - **selling@boatsforsale.com** – FSBO campaigns.
             - - **dealers@boatsforsale.com** – Dealer and broker campaigns.
               - - **newsletter@boatsforsale.com** – Branded Mailchimp blasts.
                
                 - ### WizzBanger.com (warming over the next week):
                 - - **newsletter@wizzbanger.com** – Primary branded blast address.
                   - - **info@wizzbanger.com** – Neutral/general sends.
                     - - **sales@wizzbanger.com** or **outreach@wizzbanger.com** – Dealer-specific campaigns (optional).
                      
                       - ---

                       ## Tools and Roles

                       - **Mailchimp** – Branded, minimal-design announcement campaigns (logo, color, single CTA).
                       - - **List Verification (NeverBounce/ZeroBounce)** – To clean ~20,000 emails before upload.
                         - - **Google Admin & DNS (Tom/Amrit)** – For inbox creation and SPF/DKIM/DMARC setup.
                           - - **Instantly** - Inbox warming, domain future-proofing
                            
                             - ---

                             ## Deliverability Safeguards

                             - Warm wizzbanger.com inboxes over the next 7 days before any large-scale sends via Instantly.
                             - - Configure SPF, DKIM, and DMARC for both wizzbanger.com and boatsforsale.com.
                               - - Verify all lists before upload; suppress invalid and disposable addresses.
                                 - - Limit design elements in Mailchimp templates to maintain inbox placement.
                                   - - Monitor deliverability using Google Postmaster Tools.
                                    
                                     - ---

                                     ## Access Requirements

                                     - **Google Admin Access** for wizzbanger.com and wizz-banger.com.
                                     -   - Required for inbox creation and/or sender authentication via Instantly.
                                         - - **DNS/Registrar Access** (GoDaddy, Cloudflare, etc.).
                                           -   - Required for SPF/DKIM/DMARC records and Mailchimp CNAMEs.
                                               -   - Amrit is experienced here, can set this up after aligning with Shane.
                                                   - - **Domain Strategy Confirmation.**
                                                     -   - Confirm whether all campaigns should originate from wizzbanger.com or whether volume should be distributed across both domains for safety.
                                                      
                                                         - ---

                                                         ## Execution Timeline

                                                         ### Week 1:
                                                         - Secure Google Admin and DNS access.
                                                         - - Begin inbox warming for wizzbanger.com.
                                                           - - Clean and segment ~20,000 contact records.
                                                            
                                                             - ### Following Week:
                                                             - - Build Mailchimp templates for Announcement, Reminder, and Urgency.
                                                               - - Test inbox placement across Gmail, Yahoo, and Outlook.
                                                                
                                                                 - ### Week 2 or 3:
                                                                 - - Launch campaign waves in controlled daily batches.
                                                                   - - Monitor bounce rates, spam reports, and valuation-to-listing conversions.
                                                                    
                                                                     - ---

                                                                     ## Budget & Compliance

                                                                     - **List Verification (Roughly 16-17k emails):** $150–$200 one-time.
                                                                     - - **Mailchimp:** Covered under existing subscription.
                                                                       - - **Rationale:** Verification is required to prevent bounces/spam complaints and protect domain reputation.
                                                                        
                                                                         - ---

                                                                         ## Other Considerations

                                                                         - Proper product analytics tool for app to measure user engagement and usage
                                                                         - - UTM attribution across all channels
                                                                           - - Installation of Tag Manager, PostHog across funnel domains
                                                                            
                                                                             - ---

                                                                             ## Outcome

                                                                             This plan provides a branded announcement campaign with controlled technical rollout, ensuring:

                                                                             - Deliverability safeguards on both boatsforsale.com and wizzbanger.com.
                                                                             - - Segmented outreach across private sellers, dealers, and general audiences.
                                                                               - - A clear, measurable funnel from valuation into marketplace listings.
