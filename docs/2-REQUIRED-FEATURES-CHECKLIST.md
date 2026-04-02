# ✅ REQUIRED FEATURES CHECKLIST

## PURPOSE
This checklist contains EVERY feature that MUST be present in the Echo LP system.
Before delivery, ALL boxes must be checked.

---

## 📋 PART 1: ECHO PERSONALIZATION (27 Parameters)

### Content Parameters
- [ ] hl (headline) - URL override
- [ ] sh (subheadline) - URL override
- [ ] cta (CTA text) - URL override
- [ ] img (background image) - URL override

### Styling Parameters
- [ ] btn_color (button color) - URL override
- [ ] btn_size (button size: small/medium/large/xlarge)
- [ ] btn_style (button style: square/rounded/pill/subtle)
- [ ] overlay (background overlay: light/medium/dark/xdark)
- [ ] font (font family override)

### Feature Toggles
- [ ] social_proof (enable social proof popup)
- [ ] social_text (custom social proof message)
- [ ] scarcity (enable scarcity message with number)
- [ ] scarcity_text (custom scarcity message)
- [ ] micro_yes (enable micro-commitment checkbox)
- [ ] micro_text (custom checkbox label)
- [ ] progress (show progress indicator "Step N of 3")
- [ ] test_all (enable ALL features at once)

### Tracking Parameters
- [ ] ad (ad number format: P1_AT2_AG3_V007)
- [ ] at (archetype/audience segment 1-5)
- [ ] ag (angle 1-5)
- [ ] archetype (legacy support)
- [ ] angle (legacy support)
- [ ] phase (journey phase)
- [ ] av (ad variation)
- [ ] mb (media buyer)
- [ ] eps_score (estimated predictive score 0-100)
- [ ] aps_score (actual predictive score - calculated on page)

---

## 📋 PART 2: GTM EVENTS (11 Required Events)

### Landing Page Events (Step 0)
- [ ] echo_lp_view - Page view event
- [ ] master_lp_view_retargeting - Retargeting pixel event

### CTA Click Events (Step 1)
- [ ] echo_cta_click - Button click event
- [ ] dsp_postback (step_1) - AdKernel postback
- [ ] master_lp_click_retargeting - Click retargeting pixel

### Conversion Tracker Events (Step 2)
- [ ] conversion_bridge_loaded - Tracker page loaded
- [ ] lead_conversion - Lead captured
- [ ] dsp_postback (step_2) - AdKernel postback
- [ ] master_lead_retargeting - Lead retargeting pixel

### Thank You Page Events (Step 3)
- [ ] thankyou_conversion - Final conversion
- [ ] dsp_postback (step_3) - AdKernel postback
- [ ] master_converted_retargeting - Converted user pixel

---

## 📋 PART 3: PARAMETER TRACKING (350+)

### Category 1: AdKernel Core (6)
- [ ] conversion (NOT conversion_id)
- [ ] campaign (NOT campaign_id)
- [ ] banner (NOT banner_id)
- [ ] publisher (NOT publisher_id)
- [ ] offer
- [ ] goal_id

### Category 10: Avalanche Fixed Tokens (8)
- [ ] at (archetype 1-5)
- [ ] ag (angle 1-5)
- [ ] ad (P1_AT2_AG3_V007 format)
- [ ] phase (journey phase)
- [ ] goal_id
- [ ] av (ad variation)
- [ ] mb (media buyer)
- [ ] eps (estimated predictive score)

### Categories 11-27: Avalanche Intelligence (~340 params)
- [ ] All parameters automatically stored in cookies
- [ ] All parameters passed through funnel
- [ ] Cookie expiration: 365 days

---

## 📋 PART 4: BRAND-CONFIG.JSON

### Required Sections
- [ ] brand (name, code, domain, gtmId, copyright)
- [ ] branding.font (family, url, fallback)
- [ ] branding.logo (filename, height, alt)
- [ ] landing_page.defaults
- [ ] landing_page.styling
- [ ] landing_page.features
- [ ] footer.enabled
- [ ] footer.logo
- [ ] footer.social_links (6 platforms)
- [ ] footer.links (privacy, terms, cookies, contact)
- [ ] conversion_tracker.splitTest
- [ ] thank_you_page

### Social Icons (All 6)
- [ ] facebook
- [ ] instagram
- [ ] twitter
- [ ] linkedin
- [ ] youtube
- [ ] tiktok

---

## 📋 PART 5: INTELLIGENCE SYSTEMS

### EPS System
- [ ] EPS value read from URL (if present)
- [ ] EPS stored in cookie
- [ ] EPS passed to GTM events
- [ ] EPS available on all funnel pages

### APS System
- [ ] APS calculation engine implemented
- [ ] Behavior tracking (time on page)
- [ ] Behavior tracking (mouse movements)
- [ ] Behavior tracking (CTA hovers)
- [ ] Behavior tracking (scroll depth - if applicable)
- [ ] APS updates in real-time
- [ ] APS passed to GTM events
- [ ] APS stored in cookie

### Cookie System
- [ ] setCookie function (365-day expiration)
- [ ] getCookie function
- [ ] Auto-store ALL URL parameters
- [ ] Pass ALL parameters through funnel
- [ ] Parameters persist across pages

---

## 📋 PART 6: FOOTER & BRANDING

### Footer Elements
- [ ] Footer enabled
- [ ] Logo displayed (if enabled)
- [ ] Logo links to brand website
- [ ] Social icons displayed (if enabled)
- [ ] Social icons use inline SVG (no image files)
- [ ] Social icons hover effect
- [ ] Footer links (Privacy, Terms, Cookies, Contact)
- [ ] Copyright text
- [ ] Mobile responsive

### Font Loading
- [ ] Font loaded from brand-config
- [ ] Google Fonts URL
- [ ] Fallback fonts defined
- [ ] Applied to ALL pages

---

## 📋 PART 7: LEGAL & COMPLIANCE

### Consent Text
- [ ] Displayed below CTA button
- [ ] 9px font size
- [ ] Gray color (barely visible but legal)
- [ ] Wraps properly on mobile
- [ ] Links to Privacy & Terms

### Required Links
- [ ] Privacy Policy link
- [ ] Terms of Service link
- [ ] Cookie Policy link
- [ ] Contact link

---

## 📋 PART 8: TESTING FEATURES

### Debug Mode
- [ ] debug=1 parameter works
- [ ] Console logs all GTM events
- [ ] Console shows config loaded
- [ ] Console shows all tracking

### Test Mode
- [ ] test_all=1 enables all features
- [ ] CTA can route to conversion-tracker for testing
- [ ] Full funnel testable without surveys

---

## 🔢 FEATURE COUNT VERIFICATION

**Required Minimum:**
- Echo Parameters: 27
- GTM Events: 11
- Tracking Categories: 27 (350+ params)
- Footer Elements: 10+
- Intelligence Systems: 8+

**TOTAL REQUIRED: 80+ distinct features**

**Before delivery, count actual features present:**
- Actual feature count: _______
- Required: 80+
- Status: PASS / FAIL

---

## ✅ FINAL VERIFICATION

Before delivery to user:

- [ ] All Echo parameters work
- [ ] All GTM events fire
- [ ] All 350+ parameters track
- [ ] Footer displays correctly
- [ ] Social icons work
- [ ] Legal text present
- [ ] Mobile responsive
- [ ] Full funnel tested
- [ ] User approval obtained

**Verified by:** __________
**Date:** __________
**Status:** APPROVED / REJECTED

---

**Last Updated:** 2026-03-01
**Maintained By:** Claude (with user oversight)
