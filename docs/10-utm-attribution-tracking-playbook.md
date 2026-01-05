# BoatsForSale.com Attribution & UTM Tracking Playbook 2.0

**Version:** Sprint 6.27.2025 (Draft for Implementation)  
**Prepared By:** Shane Firek

---

## Purpose

Provide end-to-end documentation for implementing campaign attribution tracking across BoatsForSale.com. Written to be accessible and educational for junior developers, with long-term scalability in mind.

### Goals

- Prove that marketing campaigns are driving leads (Google Ads, Meta, Brunswick, POP Sells)
- - Show which partners are generating results
  - - Track source of traffic over time or tie users to conversions
    - - Generate reliable reporting or billing for pay-per-lead (PPL) deals
     
      - Attribution is the foundation for scalable growth. Getting it right means understanding and capturing how users arrive on the site, and linking that visit to any action they take—now or later.
     
      - ---

      ## Attribution Architecture Overview

      | Layer | Purpose | Status |
      |-------|---------|--------|
      | UTM Parameter Capture | Extract UTM values from URL and store locally | ✅ Implemented |
      | Session Identifier | Create unique session ID for visit tracking | ✅ Implemented |
      | Form Data Injection | Auto-fill form fields with UTM + session ID values | ✅ Implemented |
      | Lead-Visit Matching | Match conversion to original session in backend | ✅ Webhook 2: /submit-lead |
      | CRM Attribution | Store all metadata in Airtable CRM or equivalent | ✅ Implemented |

      ---

      ## Where UTM Tracking Should Be Implemented

      UTM tracking needs to run on every page, but most parts only need to be installed once.

      | Layer | Implementation Location | Notes |
      |-------|------------------------|-------|
      | UTM Storage JavaScript | WordPress: footer.php or header.php (or header injection plugin) | Captures UTM parameters from the URL and stores them in localStorage |
      | Session ID Generator | Same as above | Creates unique session identifier |
      | Form Hidden Fields | Contact forms (Gravity Forms, WPForms, custom HTML) | Passes attribution data on submission |
      | n8n Webhook Integration | Backend automation | Receives and processes form data |

      ---

      ## Step 1: Capture UTM Parameters and Create Session Identifier (WordPress Compatible)

      If using WordPress, paste this inside `footer.php` (before `</body>`) or via a plugin like "Insert Headers and Footers."

      ```javascript
      <script>
      (function() {
        const urlParams = new URLSearchParams(window.location.search);
        const utmKeys = ['utm_source', 'utm_medium', 'utm_campaign', 'utm_content', 'utm_term'];

        if (!localStorage.getItem('session_id')) {
          localStorage.setItem('session_id', crypto.randomUUID());
        }

        utmKeys.forEach(key => {
          const value = urlParams.get(key);
          if (value) localStorage.setItem(key, value);
        });
      })();
      </script>
      ```

      ---

      ## Step 2: Log Visit Data to n8n (Webhook 1)

      Paste into `footer.php` (before `</body>`) or use a plugin like Insert Headers and Footers in WordPress.

      ```javascript
      <script>
      window.addEventListener('load', function () {
        const payload = {
          utm_source: localStorage.getItem('utm_source'),
          utm_medium: localStorage.getItem('utm_medium'),
          utm_campaign: localStorage.getItem('utm_campaign'),
          session_id: localStorage.getItem('session_id'),
          landing_url: window.location.href,
          referrer: document.referrer,
          timestamp: new Date().toISOString(),
          device_type: window.innerWidth < 768 ? 'mobile' : 'desktop'
        };

        fetch('https://twinvee.app.n8n.cloud/webhook/log-utm-visit', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        });
      });
      </script>
      ```

      ---

      ## Step 3: Auto-Fill Forms with UTM + Session Data

      Pre-fill hidden form fields with UTM parameters and session ID so attribution data travels with form submissions.

      ```javascript
      <script>
      document.addEventListener('DOMContentLoaded', function () {
        const keys = ['utm_source', 'utm_medium', 'utm_campaign', 'utm_content', 'session_id'];

        keys.forEach(key => {
          const val = localStorage.getItem(key);
          const input = document.querySelector(`input[name="${key}"]`);
          if (input && val) input.value = val;
        });
      });
      </script>
      ```

      ---

      ## Step 4: Match the Lead to the Visit in n8n (Webhook 2)

      Suggested Form Hook (for WordPress or HTML Forms):

      ```javascript
      <script>
      document.querySelector('#contact-form form')?.addEventListener('submit', function () {
        const payload = {
          session_id: localStorage.getItem('session_id'),
          utm_source: localStorage.getItem('utm_source'),
          utm_campaign: localStorage.getItem('utm_campaign'),
          lead_email: document.querySelector('input[name="email"]')?.value,
          submission_time: new Date().toISOString()
        };

        fetch('https://twinvee.app.n8n.cloud/webhook/submit-lead', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        });
      });
      </script>
      ```

      ---

      ## Airtable Schema

      ### Table: Visits

      | Field | Type |
      |-------|------|
      | session_id | Text (Primary) |
      | utm_source | Text |
      | utm_campaign | Text |
      | landing_url | URL |
      | referrer | URL |
      | timestamp | Created Time |
      | device_type | Single select (mobile/desktop) |
      | status | Single select (anonymous/converted) |

      ### Table: Leads

      | Field | Type |
      |-------|------|
      | session_id | Text |
      | utm_source | Text |
      | utm_campaign | Text |
      | lead_email | Email |
      | submission_time | Date/Time |

      ---

      ## Implementation Checklist

      | Task | Owner | Status |
      |------|-------|--------|
      | Build UTM + session capture | Development | ✅ |
      | Inject hidden fields into all forms | Development | ✅ |
      | Enable visit logging to n8n | Development | ✅ |
      | Build lead-to-visit matching logic in n8n | Development | ✅ |
      | Display attribution data in Airtable CRM | Dev + GTM | ✅ |
      | Set up reporting on attribution results | Operations | To Do |

      ---

      ## Summary

      You now have two webhook-powered paths:

      - `log-utm-visit`: fires on **page load**, stores metadata anonymously
      - - `submit-lead`: fires on **form submission**, connects lead to session
       
        - This framework makes it possible to track partner ROI, lead conversion performance, and campaign effectiveness across every channel.
       
        - If you're on WordPress, all of this can be implemented via theme file access or plugin-based header injection. Use DOM-safe selectors and test with `console.table`.
       
        - For questions, contact Shane Firek or the GTM technical lead.
       
        - ---

        *Last Updated: July 15, 2025*
        *Category: Marketing, Sprint, BFS*
