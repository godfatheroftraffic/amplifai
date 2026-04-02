# CONVERSION TRACKER - TESTING GUIDE

## TEST ENVIRONMENT
**Live URL:** https://lp.killerwhaleventures.com/conversion-tracker.html

## PRE-DEPLOYMENT CHECKLIST
- [ ] Upload conversion-tracker.html to server
- [ ] Upload brand-config.json to server 
- [ ] Verify GTM container GTM-XXXXXXX is live
- [ ] Confirm AdKernel campaign ID is active
- [ ] Set FormBricks redirect URL to conversion tracker

---

## 🧪 HUMAN TESTING CHECKLIST (One-Time, 15 Minutes)

**Before AI takes over, verify these 5 things work:**

### ✅ Test 1: Landing Page Loads (2 minutes)

**Your Action:**
Go to: `https://lp.yourbrand.com/`

**What You Should See:**
- Your brand's landing page
- Default headline shows
- Default CTA button shows
- Background image shows
- Footer links work

**If something's wrong:**
- Check `brand-config.json` → `gtmId` is correct
- Check images are in `/public/` folder
- Check Cloudflare deployment succeeded

---

### ✅ Test 2: URL Parameters Work (2 minutes)

**Your Action:**
Go to: `https://lp.yourbrand.com/?hl=Test+Headline&cta=Click+Me&img=hero-business.jpg`

**What You Should See:**
- Headline changes to "Test Headline"
- CTA button says "Click Me"
- Background image is `hero-business.jpg`

**If something's wrong:**
- Check browser console for errors (F12)
- Check image filename matches exactly

---

### ✅ Test 3: GTM Fires (3 minutes)

**Your Action:**
1. Install [GTM Preview Chrome Extension](https://chrome.google.com/webstore)
2. Go to GTM container
3. Click "Preview"
4. Enter: `https://lp.yourbrand.com/`
5. Check GTM Preview shows events

**What You Should See:**
- Event: `echo_page_view`
- Variables populated with data

**If something's wrong:**
- Check `gtmId` in `brand-config.json`
- Check GTM container is published

---

### ✅ Test 4: Conversion Tracker (5 minutes)

**Your Action:**
Go to: `https://lp.yourbrand.com/conversion-tracker.html?testsurvey=high_eps&dest=https://calendly.com/yourbrand/meeting`

**What You Should See:**
- Progress bar animates
- Console shows: "EPS Score: 95"
- Redirects after 3 seconds
- Calendly opens

**Open browser console (F12) and check for:**

✅ EPS Score: 95
✅ Master Database sent
✅ Email Platform sent
✅ GTM events fired
✅ Redirecting to: https://calendly.com/

**If something's wrong:**
- Check console for red errors
- Verify `dest` parameter is correct

### ✅ Test 5: Cookies Store Data (3 minutes)

**Your Action:**
1. Go to: `https://lp.yourbrand.com/?conversion=TEST123&campaign=999`
2. Open browser DevTools (F12)
3. Go to: Application → Cookies → lp.yourbrand.com

**What You Should See:**

conversion = TEST123
campaign = 999
... (other parameters stored as cookies)

**If something's wrong:**
- Check browser allows cookies
- Check parameters are in URL

---

## ✅ ALL TESTS PASSED? 

**Congratulations! Your setup is complete.**

**AI will now:**
- Generate ads automatically
- Launch campaigns automatically  
- Optimize performance automatically
- Scale winners automatically
- Report to you via email

**You're done. Go do something else.** ☕

---

## ⚠️ IF TESTS FAILED:

### Common Issues & Fixes:

**Landing page won't load:**
- Check Cloudflare deployment status
- Verify DNS points to Cloudflare
- Wait 5 minutes for DNS propagation

**Images won't load:**
- Check images are in `/public/` folder
- Check filename spelling (case-sensitive!)
- Clear Cloudflare cache

**GTM not firing:**
- Check `gtmId` in `brand-config.json`
- Verify GTM container is published
- Check no browser ad blockers

**Conversion tracker not redirecting:**
- Check `dest` parameter in URL
- Check console for errors
- Verify redirect URL is valid

---

## ADDITIONAL TEST SCENARIOS

### TEST 1: Basic Flow (High EPS)
**URL:**
```
https://lp.brand.com/conversion-tracker.html?testsurvey=high_eps&dest=https://calendly.com
```

**Expected Results:**
- ✅ Progress bar animates
- ✅ Console shows: EPS Score: 95
- ✅ Console shows: "AI Call Platform sent"
- ✅ Console shows: "SMS Platform sent"
- ✅ Console shows: "Email Platform sent"
- ✅ GTM events fire: lead_conversion, master_lead_retargeting
- ✅ DSP postbacks fire (check Network tab for AdKernel/Keitaro)
- ✅ Redirects to Calendly after 3 seconds
- ✅ Calendly pre-filled with name

---

### TEST 2: Low EPS (Conditional Webhooks)
**URL:**
```
https://lp.beand.com/conversion-tracker.html?testsurvey=low_eps&dest=https://calendly.com/
```

**Expected Results:**
- ✅ EPS Score: 25
- ❌ Console shows: "Skipping AI Call (EPS too low)"
- ❌ Console shows: "Skipping SMS (EPS too low)"
- ✅ Console shows: "Email Platform sent" (EPS >= 30 required, will fail)
- ✅ Master Database still fires
- ✅ Redirects normally

---

### TEST 3: Missing Email
**URL:**
```
https://lp.brand.com/conversion-tracker.html?testsurvey=no_email&dest=https://calendly.com/
```

**Expected Results:**
- ✅ Console shows: "Skipping Email (no email)"
- ✅ AI Call fires (has phone)
- ✅ SMS fires (has phone)
- ✅ Redirects normally

---

### TEST 4: Missing Phone
**URL:**
```
https://lp.brand.com/conversion-tracker.html?testsurvey=no_phone&dest=https://calendly.com/
```

**Expected Results:**
- ❌ Console shows: "Skipping AI Call (no phone)"
- ❌ Console shows: "Skipping SMS (no phone)"
- ✅ Email fires (has email)
- ✅ Redirects normally

---

### TEST 5: Minimal Data
**URL:**
```
https://lp.brand.com/conversion-tracker.html?testsurvey=minimal&dest=https://calendly.com/
```

**Expected Results:**
- ✅ EPS: 30
- ❌ All PII webhooks skip (no email/phone)
- ✅ Master Database fires
- ✅ Redirects normally

---

### TEST 6: Real Survey Flow (End-to-End)
**Steps:**
1. Go to: https://lp.killerwhaleventures.com/?trck=KWV_TEST_001&subid=TEST_SUBID&hl=Test&cta=View%20Demo&link=https://app.formbricks.com/s/cml9est324q03zf01b6zrsc6d&img=kwv_5.jpg
2. Click "View Demo"
3. Complete FormBricks survey with:
   - Email: your-real-email@example.com
   - Phone: your-real-phone
   - Answer all questions
4. Submit survey

**Expected Results:**
- ✅ Redirects to conversion-tracker.html
- ✅ Progress bar shows
- ✅ GTM events fire (check GTM Preview)
- ✅ Console shows all webhooks firing
- ✅ Redirects to Calendly
- ✅ Calendly pre-filled with email, name, survey answers
- ✅ Check Cloudflare Worker logs for webhook

---

### TEST 7: Webhook Failure & Retry
**Steps:**
1. Temporarily break webhook URL in code (change to fake URL)
2. Load page: `?testsurvey=1&dest=https://example.com`
3. Check localStorage: `localStorage.getItem('webhook_queue')`
4. Fix webhook URL
5. Reload page

**Expected Results:**
- ✅ First load: Webhook fails, queued in localStorage
- ✅ Console shows: "Queued for retry: [webhook name]"
- ✅ Second load: Console shows "Retrying X queued webhooks"
- ✅ Webhook succeeds on retry
- ✅ Queue cleared

---

### TEST 8: Split Test
**URL:**
```
https://lp.brand.com/conversion-tracker.html?testsurvey=1
```
(No dest parameter - uses split test config)

**Expected Results:**
- ✅ Randomly selects variant (100% to control currently)
- ✅ Sets cookie: split_variant=control
- ✅ Subsequent loads return same variant
- ✅ Redirects to configured variant URL

---

### TEST 9: Forced Variant
**URL:**
```
https://lp.brand.com/conversion-tracker.html?testsurvey=1&variant=control
```

**Expected Results:**
- ✅ Console shows: "Forced variant: control"
- ✅ Skips random selection
- ✅ Redirects to control URL

---

### TEST 10: Bot Detection
**Steps:**
1. Open in headless Chrome: `chrome --headless`
2. Or simulate fast timing by loading page and immediately checking

**Expected Results:**
- ✅ Console shows: "Bot detected"
- ❌ Webhooks don't fire (saved costs)
- ✅ Still redirects normally

---

### TEST 11: Archetype Pixel Routing
**URL:**
```
https://lp.brand.com/conversion-tracker.html?testsurvey=1&archetype=optimizer&dest=https://example.com
```

**Expected Results:**
- ✅ GTM dataLayer shows: `recommended_pixels: ['facebook', 'linkedin', 'google']`
- ✅ GTM can use this to selectively fire pixels

---

### TEST 12: Angle Personalization
**URL:**
```
https://lp.brand.com/conversion-tracker.html?testsurvey=1&angle=data_driven&dest=https://example.com
```

**Expected Results:**
- ✅ Email webhook payload includes: `"subject": "Your Data-Backed Growth Strategy - KWV"`
- ✅ SMS webhook includes: "here's your data-driven action plan"
- ✅ AI Call webhook includes: `"call_script_id": "kwv_data_driven_expert"`

---

### TEST 13: Funnel Step Increment
**URL:**
```
https://lp.brand.com/conversion-tracker.html?testsurvey=1&funnel_step=step_3&dest=https://example.com
```

**Expected Results:**
- ✅ Redirect URL includes: `funnel_step=step_4`
- ✅ Next page receives step_4
- ✅ DSP postback uses step_3

---

### TEST 14: GTM Preview Mode
**Steps:**
1. Open GTM Preview for container GTM-T639H2SD
2. Load: `?testsurvey=1&dest=https://example.com`
3. Check GTM Preview sidebar

**Expected Results:**
- ✅ See event: conversion_bridge_loaded
- ✅ See event: lead_conversion
- ✅ See event: master_lead_retargeting
- ✅ See event: conversion_bridge_redirect
- ✅ All events have correct dataLayer variables

---

### TEST 15: DSP Postback Verification
**Steps:**
1. Open browser Network tab
2. Filter: "conversion"
3. Load: `?testsurvey=1&dest=https://example.com`

**Expected Results:**
- ✅ Request to: xml.amplifai.it.com/conversion?id=3214529&c=TEST_CONV_1&step=3&quality_score=85
- ✅ Request to: rtb2-useast.amplifai.it.com/conversion?cid=TEST_CONV_1&step=3&quality_score=85
- ⚠️ May return 400 if test conversion ID not in AdKernel (expected)

---

## PRODUCTION READINESS CHECKLIST

### Before Going Live:
- [ ] Test all 15 scenarios above
- [ ] Verify GTM tags fire correctly in Preview mode
- [ ] Confirm AdKernel campaign accepts real conversion IDs
- [ ] Test with real email/phone (verify no spam)
- [ ] Verify Calendly receives correct pre-fill data
- [ ] Check webhook endpoints return 200 OK
- [ ] Verify localStorage queue works across page reloads
- [ ] Test on mobile devices
- [ ] Test on different browsers (Chrome, Safari, Firefox)
- [ ] Verify GDPR compliance (consent flags working)

### FormBricks Configuration:
- [ ] Survey redirect URL set to: https://lp.brand.com/conversion-tracker.html
- [ ] Webhook URL set to: https://formbricks-gtm-bridge.team-431.workers.dev/
- [ ] Webhook trigger: Response Finished

### DNS/Hosting:
- [ ] conversion-tracker.html deployed to production
- [ ] HTTPS enabled
- [ ] CORS headers configured if needed

---

## TROUBLESHOOTING

### Issue: Webhooks not firing
**Check:**
- Console errors
- PII consent flags
- EPS score vs. thresholds
- Email/phone validation
- Bot detection status

### Issue: Not redirecting
**Check:**
- selectedVariant is defined
- Console shows "Final URL"
- No JavaScript errors
- Fallback link appears after 10 seconds

### Issue: GTM events not firing
**Check:**
- GTM container loaded (check Network tab)
- No duplicate injection error
- dataLayer.push() calls in console
- GTM Preview mode shows events

### Issue: DSP postback 400 error
**Expected:**
- Test conversion IDs return 400
- Real campaign IDs return 200

### Issue: Parameters not passing
**Check:**
- URL parameters present
- Cookies set correctly
- getParam() deduplication working
- hasPIIConsent() returning true

---

## MONITORING

### Key Metrics to Track:
- Webhook success rate (should be >95%)
- Webhook retry queue size (should stay near 0)
- Bot detection rate (typically 5-15%)
- EPS score distribution
- Conversion by archetype/angle
- Split test variant distribution

### Error Monitoring:
- Check error logging endpoint for failures
- Monitor localStorage queue growth
- Track webhook timeout frequency

---

## SUPPORT

**Questions?**
- Check console logs (always use ?testsurvey=1 for debugging)
- Review webhook payloads in Network tab
- Verify GTM container in Preview mode
- Check localStorage for queued webhooks
