# 🌊 MASTER ECHO REPOSITORY

**The Universal Template for AmplifAI Performance Stack**

This repository contains the master echo landing page system that powers:
- **AmplifAI DSP** (Traffic acquisition)
- **Angle Desk** (Message discovery)
- **FunnelCrack** (Funnel intelligence)
- **AVALANCHE** (Infinite-cognition AI OS)

---

## **📊 WHAT THIS CAPTURES:**

### **Complete Tracking - 350+ Parameters:**

1. **AdKernel Tracking (65 params)** - Traffic source data
2. **Keitaro Routing (13 params)** - Tracker intelligence
3. **Creative DNA (44 params)** - Ad component tracking
4. **Echo Landing Page (26 params)** - Dynamic content
5. **Avalanche Tokens (35 params)** - Behavioral DNA
6. **Funnel Intelligence (19 params)** - Quality prediction

---

---

## 🤖 HUMAN 1% vs AI 99% - WHO DOES WHAT?

### **HUMAN RESPONSIBILITIES (1% - One-Time Setup Only):**

#### Step 1: Brand Repository Setup (5 minutes)
1. Create new GitHub repo: `brand-[BRAND_CODE]`
2. Clone master echo repo
3. Copy files to brand repo
4. Push to GitHub

#### Step 2: Customize brand-config.json (10 minutes)
1. Update brand name
2. Add GTM container ID (get from GTM account)
3. Set domain name
4. Add footer links and social links (privacy, terms, contact URLs)


#### Step 3: Add Brand Assets (5 minutes)
1. Upload logo to `/public/logo.png`
2. Upload 3-5 hero images to `/public/` folder
3. Name images clearly (e.g., `hero-business.jpg`, `hero-success.jpg`)

#### Step 4: Deploy to Cloudflare Pages (5 minutes)
1. Go to Cloudflare Pages
2. Click "Create a project"
3. Connect GitHub account
4. Select your brand repo
5. Click "Deploy"
6. Add custom domain: `lp.yourbrand.com`

#### Step 5: Get API Keys (10 minutes)
1. AdKernel API key (from AdKernel dashboard)
2. Ad Spy Tool API keys (from each platform)
3. Add to environment variables in deployment

**TOTAL HUMAN TIME: 35 minutes one-time setup**

---

### **AI RESPONSIBILITIES (99% - Automated Forever):**

#### Every 24 Hours Automatically:
1. ✅ Scan 10,000+ top ads from spy tools (Meta, TikTok, Anstrex, etc.)
2. ✅ Extract winning patterns (headlines, hooks, offers, images)
3. ✅ Combine market intelligence with EPS/APS performance data
4. ✅ Generate 100+ new ad variations (push, native, display, video)
5. ✅ Create all creative assets:
   - Headlines (hl parameter)
   - Subheadlines (sh parameter)
   - CTA text (cta parameter)
   - Images (img parameter - AI generates or selects)
   - Videos (for video channels)
6. ✅ Generate Echo landing page URLs with ALL parameters
7. ✅ Launch campaigns on AdKernel automatically
8. ✅ Monitor performance in real-time
9. ✅ Calculate EPS vs APS deltas
10. ✅ Pause losing ads automatically
11. ✅ Scale winning ads automatically (2x-10x budget)
12. ✅ Graduate winners to next channel (push → native → display → video → CTV)
13. ✅ Update creative based on learnings
14. ✅ Send performance reports to team email

#### Every Hour Automatically:
1. ✅ Check campaign performance
2. ✅ Adjust bids based on EPS/APS
3. ✅ Move budget from losers to winners
4. ✅ Fire conversion postbacks to AdKernel/Keitaro
5. ✅ Update audience segments based on behavior

#### On Every Click Automatically:
1. ✅ Capture all 350+ parameters
2. ✅ Store in cookies
3. ✅ Calculate EPS score (AI prediction)
4. ✅ Personalize landing page content
5. ✅ Track user behavior (scroll, time, clicks)
6. ✅ Update APS score based on behavior
7. ✅ Fire GTM events
8. ✅ Send conversion data to master database

#### On Every Conversion Automatically:
1. ✅ Calculate EPS vs APS delta
2. ✅ Send to ML training pipeline
3. ✅ Update bid strategies
4. ✅ Trigger follow-up sequences (email, SMS, AI calls)
5. ✅ Fire retargeting pixels
6. ✅ Update audience segments

**HUMAN DOES:** 35 minutes one-time setup  
**AI DOES:** Everything else, forever, 24/7/365

---

## **🚀 DEPLOYMENT INSTRUCTIONS:**

### **Step 1: Create Brand-Specific Repository**

For each new brand, create a new repository:

```bash
Repository name: brand-[BRAND_CODE]
Example: brand-kwv (Killer Whale Ventures)
```

### **Step 2: Clone Master Repository**

```bash
git clone [master-echo-repo-url]
cd master-echo
```

### **Step 3: Customize for Brand**

1. **Update GTM Container ID:**
   - Open `index.html`
   - Find: `GTM-XXXXXXX`
   - Replace with brand's GTM container ID
   - Repeat for `thank-you.html`

2. **Add Brand Images:**
   - Place images in `/public/` folder
   - Use exact filenames from creative tracking system

3. **Set Default Content (Optional):**
   - Edit default headline in `index.html`
   - Edit default subheadline
   - Edit default CTA text

### **Step 4: Deploy to GitHub**

```bash
git init
git add .
git commit -m "Initial brand setup"
git remote add origin [your-brand-repo-url]
git push -u origin main
```

### **Step 5: Connect to Cloudflare Pages**

1. Go to Cloudflare Pages
2. Create New Project
3. Connect to GitHub
4. Select your brand repository
5. Build settings:
   - Framework preset: **None (Static site)**
   - Build command: **Leave blank**
   - Build output directory: **/**
6. Deploy

### **Step 6: Add Custom Domain**

1. In Cloudflare Pages → Custom domains
2. Add: `lp.[branddomain].com`
3. Update DNS (Cloudflare will show required records)
4. Wait for SSL certificate (automatic)

---

## **🔗 URL STRUCTURE:**

### **Landing Page URL Format:**

```
https://lp.branddomain.com/
  ?conversion={clickid}
  &goal_id=3214532
  &campaign={campaign_id}
  &banner={banner_id}
  &hl=Your%20Headline%20Here
  &sh=Your%20Subheadline
  &cta=Get%20Started
  &img=background-image.jpg
  &archetype=AT1
  &angle=AG3
  &phase=P3
  &av=vid001
  &ss=boldstatement
  ... (up to 182 parameters)
```

### **Thank You Page URL:**

```
https://lp.branddomain.com/thank-you.html
```

---

## **🎯 HOW IT WORKS:**

### **Landing Page (index.html):**

1. **Reads URL parameters** (350+)
2. **Stores in cookies** (30-day expiration)
3. **Applies dynamic content:**
   - Headline from `?hl=`
   - Subheadline from `?sh=`
   - CTA text from `?cta=`
   - Background image from `?img=`
   - Styling from other params
4. **Fires GTM event:** `echo_page_view`
5. **Tracks behavior:**
   - Time on page
   - CTA clicks

### **Thank You Page (thank-you.html):**

1. **Reads all cookies** (set by landing page)
2. **Builds complete data layer** (all 360+ params)
3. **Fires GTM event:** `thankyou_conversion`
4. **GTM tags fire:**
   - AdKernel XML conversion
   - AdKernel DSP conversion
   - Keitaro S2S postback (when configured)

---

## **📊 GTM CONFIGURATION REQUIRED:**

### **Variables:**

All variables should already be configured in your GTM master template container. If not, import the master GTM JSON file.

### **Tags (2 minimum):**

1. **AdKernel XML - Conversion Tracking**
   - Fires on: `thankyou_conversion`
   - URL: `https://xml.amplifai.it.com/conversion?id={{DLV - goal_id}}&c={{DLV - conversion}}&count=1&value={{DLV - conversion_value}}`

2. **AdKernel DSP - Conversion Tracking**
   - Fires on: `thankyou_conversion`
   - URL: `https://rtb2-useast.amplifai.it.com/conversion?cid={{DLV - conversion}}&step={{DLV - dsp_step}}`

---

## **🔧 CUSTOMIZATION OPTIONS:**

### **Echo Landing Page Dynamic Parameters:**

| Parameter | Purpose | Example |
|-----------|---------|---------|
| `hl` | Headline text | `Stop%20Wasting%20Time` |
| `sh` | Subheadline text | `Get%20Results%20Today` |
| `cta` | CTA button text | `Start%20Now` |
| `img` | Background image filename | `hero-bg.jpg` |
| `link` | CTA destination URL | `https://form.com/signup` |
| `overlay` | Overlay darkness | `light`, `medium`, `dark`, `xdark` |
| `btn_color` | Button color | `#2563eb` |
| `btn_size` | Button size | `small`, `medium`, `large`, `xlarge` |
| `btn_style` | Button style | `square`, `rounded`, `pill` |
| `social_proof` | Show social proof | `on`, `off` |
| `social_text` | Social proof text | `Join%2010000%2B%20customers` |
| `scarcity` | Scarcity number | `3`, `5`, `10` |
| `scarcity_text` | Scarcity message | `Only%203%20spots%20left` |

### **Example Dynamic URL:**

```
https://lp.branddomain.com/
  ?conversion=CLICK123
  &goal_id=3214532
  &hl=Transform%20Your%20Business
  &sh=In%2030%20Days%20Or%20Less
  &cta=Start%20Free%20Trial
  &img=business-hero.jpg
  &overlay=dark
  &btn_color=%232563eb
  &btn_size=large
  &btn_style=pill
  &social_proof=on
  &social_text=Join%2050000%2B%20entrepreneurs
  &scarcity=5
  &scarcity_text=Only%205%20spots%20remaining
```

---

## **🌊 AVALANCHE INTEGRATION:**

The system automatically captures **Avalanche tokens** for infinite-cognition AI:

### **Core Tokens:**
- `session_token` - Unique session ID
- `belief_pattern` - User belief state
- `user_fingerprint` - Behavioral DNA
- `emotional_readiness` - Ready-to-convert score
- `remnant_index` - Resurrection eligibility

### **Performance Signals:**
- `eps_score` - Emotional Performance Signal
- `aps_score` - Archetypal Performance Signal
- `attention_root` - What captured attention
- `friction_point` - Where user hesitated

### **Memory Chain:**
- `seen_day` - Day of journey (day0, day1, etc.)
- `interaction_count` - Number of interactions
- `previous_exit_reason` - Why they left before
- `memory_chain_id` - Continuous memory ID

---

## **🎨 CREATIVE DNA TRACKING:**

### **Video/CTV Ads:**
- `ss` - Skip stopper type
- `ht` - Hook type
- `vs` - Voiceover style
- `bm` - Background music
- `vl` - Video length

### **Display/Native Ads:**
- `ii` - Interruptor image
- `ih` - Image hero
- `bc` - Body copy style
- `sp` - Social proof type

### **Push Ads:**
- `pi` - Push icon
- `hl` - headline
- `ul` - Urgency level

### **Pop Ads:**
- `ag` - Attention grabber
- `vh` - Visual hero
- `eit` - Exit intent trigger

---

## **📈 ANGLE DESK INTEGRATION:**

Automatically tracks testing phases:

- `archetype` - at=1, at=2, at=3, at=4, at=5
- `angle` - ag=1, ag=2, ag=3, ag=4, ag=5
- `phase` - P1, P2, P3, P4, P5, P6, P7
- `variant` - ad variant number

AI learns: **"Which creative DNA works best for which archetype in which phase?"**

---

## **🔐 SECURITY & PRIVACY:**

- Cookies expire after 365 days
- No PII stored in cookies
- HTTPS required (Cloudflare auto-SSL)
- GTM handles all analytics
- GDPR compliant (no tracking without GTM consent)

---

## **🧪 TESTING CHECKLIST:**

### **Before Launch:**

- [ ] GTM Container ID updated
- [ ] Brand images uploaded to `/public/`
- [ ] Test URL with all parameters
- [ ] Verify cookies are set (DevTools → Application → Cookies)
- [ ] Check GTM data layer (DevTools → Console)
- [ ] Test conversion flow end-to-end
- [ ] Verify AdKernel receives conversions
- [ ] Test on mobile device
- [ ] Check page load speed (<2 seconds)
- [ ] SSL certificate active

### **Test URL Generator:**

```
https://lp.branddomain.com/
  ?conversion=TEST123
  &goal_id=3214532
  &campaign=999
  &banner=888
  &hl=Test%20Headline
  &sh=Test%20Subheadline
  &cta=Test%20CTA
  &img=test-background.jpg
```

---

## **🚨 TROUBLESHOOTING:**

### **Images Not Loading:**
- Check image is in `/public/` folder
- Verify filename matches exactly (case-sensitive)
- Try purging Cloudflare cache

### **Cookies Not Storing:**
- Check browser allows cookies
- Verify parameters are in URL
- Check cookie expiration (365 days default)

### **GTM Not Firing:**
- Verify GTM Container ID is correct
- Check event name spelling: `thankyou_conversion`
- Look for errors in browser console
- Use GTM Preview mode for debugging

### **Conversions Not Tracking in AdKernel:**
- Verify `conversion` and `goal_id` are present
- Check AdKernel postback URLs are correct
- Look for 200 response in Network tab
- Verify goal_id matches AdKernel campaign

---

## **📞 SUPPORT:**

For issues or questions:
1. Check browser console for errors
2. Verify GTM Preview mode shows data
3. Test with simple URL first
4. Check Network tab for failed requests

---

## **🎯 NEXT STEPS:**

1. ✅ Deploy to brand repository
2. ✅ Connect to Cloudflare Pages
3. ✅ Add custom domain
4. ✅ Test end-to-end
5. ✅ Launch first campaign
6. ✅ Monitor GTM data
7. ✅ Analyze Avalanche patterns
8. ✅ **SCALE TO THE MOON** 🚀

---

**This is the most sophisticated echo landing page system ever built.**

It captures **350+ parameters** across:
- Traffic source (AdKernel)
- Routing (Keitaro)
- Creative DNA (All DSP channels)
- Dynamic content (Echo)
- Behavioral DNA (Avalanche)
- Funnel intelligence (Quality signals)

**AI learns everything. Humans touch nothing. System scales infinitely.** 🌊
