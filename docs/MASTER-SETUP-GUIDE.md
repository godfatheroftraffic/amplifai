# Echo Landing Page System - Setup Guide

**Master Template Repository v2.1**

This is the universal Echo Landing Page system that works for ANY brand. You customize it by editing ONE file: `brand-config.json`

**NO CODE CHANGES NEEDED!**

---

## 🚀 Quick Start (15 Minutes)

### What You'll Get
- ✅ Landing page with your brand colors, logo, and content
- ✅ Thank you page with conversion tracking
- ✅ Split testing ready
- ✅ 350+ tracking parameters automatically captured
- ✅ GTM integration for all pixels/postbacks
- ✅ Mobile-optimized images
- ✅ 365-day cookie tracking

---

## 📋 Step-by-Step Setup

### **Step 1: Copy Files to Your Brand Repository**

1. Download these files from the master repository:
   - `index.html`
   - `thank-you.html`
   - `conversion-tracker.html`
   - `brand-config.json`
   - `.gitignore`

2. Create your brand repository folder:
   ```
   echo-lp-[brandname]/
   ├── index.html
   ├── thank-you.html
   ├── conversion-tracker.html
   ├── brand-config.json
   ├── .gitignore
   └── public/
       ├── logo.png
       ├── 4_[brandcode].jpg
       └── 4_[brandcode]_mobile.jpg
   ```

3. Upload to GitHub and connect to Cloudflare Pages

---

### **Step 2: Customize brand-config.json**

This is the ONLY file you need to edit!

#### **2A. Brand Information**

Open `brand-config.json` and find this section:

```json
"brand": {
  "name": "Your Brand Name",           ← Change this
  "code": "ybr",                        ← Change this (2-4 letters)
  "domain": "lp.yourbrand.com",         ← Change this
  "gtmId": "GTM-XXXXXXX",               ← Change this
  "logo": "logo.png",
  "copyright": "© 2024 Your Brand Name" ← Change this
}
```

**Example for "Killer Whale Ventures":**
```json
"brand": {
  "name": "Killer Whale Ventures",
  "code": "kwv",
  "domain": "lp.killerwhaleventures.com",
  "gtmId": "GTM-T639H2SD",
  "logo": "logo.png",
  "copyright": "© 2026 Killer Whale Ventures. All rights reserved."
}
```

---

#### **2B. Landing Page Content**

Find this section:

```json
"landing_page": {
  "defaults": {
    "headline": "Transform Your Business Today",     ← Change this
    "subheadline": "Join thousands...",              ← Change this
    "cta_text": "Get Started Now",                   ← Change this
    "cta_link": "https://calendly.com/...",          ← Change this
    "background_image": "4_ybr.jpg",                 ← Change this
    "overlay": "dark"
  }
}
```

**Example:**
```json
"landing_page": {
  "defaults": {
    "headline": "Consistent, Trusted Signals",
    "subheadline": "Clear rules. Clear trading.",
    "cta_text": "View Live Signals",
    "cta_link": "https://calendly.com/killerwhaleventures/meeting",
    "background_image": "5_kwv.jpg",
    "overlay": "dark"
  }
}
```

---

#### **2C. Button Styling**

Find this section:

```json
"styling": {
  "button_color": "#2563eb",        ← Your brand color (hex)
  "button_text_color": "#ffffff",
  "button_size": "large",           ← small, medium, large, xlarge
  "button_style": "rounded"         ← square, rounded, pill, subtle
}
```

**Popular Brand Colors:**
- Blue: `#2563eb`
- Green: `#10b981`
- Purple: `#7c3aed`
- Red: `#ef4444`
- Teal: `#1DBF8A` (KWV example)

---

#### **2D. Footer Links**

Find this section:

```json
"footer": {
  "links": {
    "privacy": {
      "enabled": true,
      "text": "Privacy",
      "url": "https://yourbrand.com/privacy"      ← Change this
    },
    "terms": {
      "enabled": true,
      "text": "Terms",
      "url": "https://yourbrand.com/terms"        ← Change this
    }
  }
}
```

**To hide a link:** Set `"enabled": false`

---

#### **2E. Split Testing (Optional)**

Find this section:

```json
"conversion_tracker": {
  "splitTest": {
    "enabled": true,
    "variants": [
      {
        "id": "control",
        "name": "control",
        "url": "https://calendly.com/yourbrand/meeting",  ← Change this
        "weight": 100,
        "enabled": true
      }
    ]
  }
}
```

**To add a second variant:**
```json
"variants": [
  {
    "id": "control",
    "name": "Calendly",
    "url": "https://calendly.com/yourbrand/meeting",
    "weight": 50,
    "enabled": true
  },
  {
    "id": "variant_a",
    "name": "TypeBot",
    "url": "https://typebot.io/yourbrand-survey",
    "weight": 50,
    "enabled": true
  }
]
```

**Weight = Traffic %:** 50/50 split = both get 50% traffic

---

### **Step 3: Add Your Images**

#### **3A. Create Your Brand Code**

Your brand code is 2-4 lowercase letters. Examples:
- Killer Whale Ventures → `kwv`
- Nike → `nike`
- Apple → `aapl`
- Your Brand → `ybr`

#### **3B. Image Naming Convention**

All images use **number-first naming:**

**Landing Page Images (in `/public/`):**
```
4_kwv.jpg              ← Desktop version (1920x1080px)
4_kwv_mobile.jpg       ← Mobile version (750x1334px)
5_kwv.jpg
5_kwv_mobile.jpg
```

**Why mobile versions?**
- 80% of traffic is mobile
- Faster load times (80-150KB vs 300-500KB)
- Same visual, just optimized

#### **3C. Create Images**

1. **Desktop version:** 1920x1080px, save as `4_[brandcode].jpg`
2. **Mobile version:** 750x1334px, save as `4_[brandcode]_mobile.jpg`
3. Upload both to `/public/` folder

#### **3D. Update brand-config.json**

```json
"landing_page": {
  "defaults": {
    "background_image": "4_kwv.jpg"    ← Use your image name
  }
}
```

**The system automatically loads:**
- Desktop users → `4_kwv.jpg`
- Mobile users → `4_kwv_mobile.jpg`

---

### **Step 4: Set Up Google Tag Manager**

#### **4A. Get Your GTM Container ID**

1. Go to [tagmanager.google.com](https://tagmanager.google.com)
2. Create a new container (or use existing)
3. Copy the Container ID (looks like `GTM-XXXXXXX`)

#### **4B. Add to brand-config.json**

```json
"brand": {
  "gtmId": "GTM-T639H2SD"    ← Paste your GTM ID here
}
```

#### **4C. Create GTM Variables**

In GTM, create these Data Layer Variables:

| Variable Name | Data Layer Variable Name |
|---------------|--------------------------|
| conversion | conversion |
| goal_id | goal_id |
| dsp_step | dsp_step |
| aps_current | aps_current |
| archetype | archetype |
| angle | angle |
| ad | ad |
| campaign | campaign |
| banner | banner |
| publisher | publisher |

**How to create:**
1. GTM → Variables → New
2. Variable Type: Data Layer Variable
3. Data Layer Variable Name: `conversion` (example)
4. Save

#### **4D. Create Postback Tags**

**Tag 1: AdKernel XML Postback**
- Tag Type: Custom Image
- Image URL: `https://xml.amplifai.it.com/conversion?id={{goal_id}}&c={{conversion}}&value={{conversion_value}}&quality_score={{aps_current}}`
- Trigger: `dsp_postback` event

**Tag 2: AdKernel DSP Postback**
- Tag Type: Custom Image
- Image URL: `https://rtb2-useast.amplifai.it.com/conversion?cid={{conversion}}&step={{dsp_step}}&value={{conversion_value}}&quality_score={{aps_current}}`
- Trigger: `dsp_postback` event

**Tag 3: Facebook Pixel (Example - Optimizer Archetype)**
- Tag Type: Facebook Pixel
- Trigger: `master_lead_retargeting` + `archetype` equals `optimizer`

**Tag 4: TikTok Pixel (Example - High Value Leads)**
- Tag Type: TikTok Pixel
- Trigger: `master_converted_retargeting` + `aps_current` > 70

---

### **Step 5: Deploy to Cloudflare Pages**

#### **5A. Connect GitHub to Cloudflare**

1. Go to [dash.cloudflare.com](https://dash.cloudflare.com)
2. Pages → Create a project → Connect to Git
3. Select your repository
4. Build settings:
   - Framework preset: None
   - Build command: (leave empty)
   - Build output directory: `/`
5. Click "Save and Deploy"

#### **5B. Set Custom Domain**

1. Cloudflare Pages → Custom domains
2. Add domain: `lp.yourbrand.com`
3. Update DNS in Cloudflare:
   - Type: CNAME
   - Name: lp
   - Target: [your-project].pages.dev

**Done! Your landing page is live!** 🎉

---

## 🎨 Customization Examples

### Example 1: Change Button Color to Green

```json
"styling": {
  "button_color": "#10b981",
  "button_text_color": "#ffffff"
}
```

### Example 2: Enable Social Proof

```json
"features": {
  "social_proof": {
    "enabled": true,
    "default_text": "Join 10,000+ satisfied customers"
  }
}
```

### Example 3: Add Scarcity Timer

```json
"features": {
  "scarcity": {
    "enabled": true,
    "default_spots": 3,
    "default_text": "Only {spots} spots remaining!"
  }
}
```

### Example 4: Enable Auto-Redirect After Thank You

```json
"thank_you_page": {
  "redirect": {
    "enabled": true,
    "url": "https://yourbrand.com/welcome",
    "delay_seconds": 3
  }
}
```

---

## 📊 Understanding Tracking Steps

The system fires different GTM events at each funnel stage:

### **Step 0: Page View**
- Page: `index.html`
- Event: `echo_page_view`, `master_lp_view_retargeting`
- When: User lands on page
- No postback (just pixel for retargeting)

### **Step 1: Landing Page Click**
- Page: `index.html`
- Event: `echo_cta_click`, `dsp_postback`, `master_lp_click_retargeting`
- When: User clicks CTA button
- Postback: Yes (step_1)

### **Step 2: Survey/Form Complete**
- Page: `conversion-tracker.html`
- Event: `lead_conversion`, `dsp_postback`, `master_lead_retargeting`
- When: User completes survey/form
- Postback: Yes (step_2)

### **Step 3: Booking/Purchase Confirmed**
- Page: `thank-you.html`
- Event: `thankyou_conversion`, `dsp_postback`, `master_converted_retargeting`
- When: User confirms booking/purchase
- Postback: Yes (step_3)

---

## 🔧 Advanced: Webhooks (Optional)

If you want to trigger AI calls, SMS, or emails based on lead quality:

```json
"webhooks": {
  "enabled": true,
  "endpoints": {
    "ai_call": {
      "enabled": true,
      "url": "https://api.yourbrand.com/webhooks/ai-call",
      "min_eps": 70    ← Only call leads with EPS ≥ 70
    },
    "sms": {
      "enabled": true,
      "url": "https://api.yourbrand.com/webhooks/sms",
      "min_eps": 50
    },
    "email": {
      "enabled": true,
      "url": "https://api.yourbrand.com/webhooks/email",
      "min_eps": 30
    }
  }
}
```

**EPS = Estimated Performance Score (1-100)**
- 70+ = High quality lead
- 50-69 = Medium quality
- 30-49 = Low quality
- <30 = Very low quality

---

## 📱 Testing Your Setup

### **Test 1: Basic Page Load**

Visit: `https://lp.yourbrand.com/?debug=1`

**You should see in console:**
```
✅ brand-config.json loaded successfully
✅ GTM Loaded: GTM-XXXXXXX
🍪 Storing all tracking parameters in cookies (365-day expiration)...
✅ All 350+ parameters stored in cookies
📊 echo_page_view fired
```

### **Test 2: CTA Click**

Click the CTA button. **You should see:**
```
📊 echo_cta_click fired
📊 dsp_postback fired (step_1: LP Click)
📊 master_lp_click_retargeting fired
```

### **Test 3: Full Funnel (with Survey)**

Visit: `https://lp.yourbrand.com/conversion-tracker.html?testsurvey=1&debug=1`

**You should see:**
```
🎯 Conversion Tracker v2.1 [TEST: 1]
   Conversion: TEST_CONV_1
   EPS (Initial): 85
   APS (Current): 85
   Archetype: optimizer
   Angle: data_driven
✅ GTM events fired
✅ dsp_postback event fired (GTM will handle pixel firing)
✅ master_lead_retargeting fired
```

### **Test 4: Thank You Page**

Visit: `https://lp.yourbrand.com/thank-you.html?type=booking&debug=1`

**You should see:**
```
✅ GTM Data Layer Complete!
📊 Parameters: [number]
🔑 Conversion: [value]
✅ dsp_postback event fired (GTM handles pixels)
✅ master_converted_retargeting fired
```

---

## 🐛 Troubleshooting

### "brand-config.json not found"

**Problem:** File not uploaded or wrong location
**Solution:** Make sure `brand-config.json` is in the root folder (same level as index.html)

### "Background image not loading"

**Problem:** Image name doesn't match config or missing mobile version
**Solution:**
1. Check image name in config matches actual filename
2. Make sure both desktop AND mobile versions exist:
   - `4_kwv.jpg`
   - `4_kwv_mobile.jpg`
3. Both must be in `/public/` folder

### "GTM events not firing"

**Problem:** GTM ID wrong or GTM blocked by ad blocker
**Solution:**
1. Verify GTM ID in brand-config.json
2. Check browser console for GTM errors
3. Disable ad blocker for testing
4. Check GTM Preview mode

### "Postbacks not firing in AdKernel"

**Problem:** GTM tags not set up correctly
**Solution:**
1. Check GTM tags are created (see Step 4D)
2. Verify triggers match event names exactly
3. Use GTM Preview mode to debug
4. Check AdKernel campaign ID in brand-config.json

---

## 📚 File Structure Reference

```
echo-lp-[brandname]/
├── index.html                  ← Landing page (DO NOT EDIT)
├── thank-you.html              ← Thank you page (DO NOT EDIT)
├── conversion-tracker.html     ← Conversion tracker (DO NOT EDIT)
├── brand-config.json           ← EDIT THIS FILE ONLY
├── .gitignore
└── public/
    ├── logo.png                ← Your logo
    ├── 4_[brand].jpg           ← Desktop background
    ├── 4_[brand]_mobile.jpg    ← Mobile background
    ├── 5_[brand].jpg           ← Additional images
    └── 5_[brand]_mobile.jpg
```

---

## 🎯 Next Steps

1. **Set up Google Drive** for ad creatives (see `/docs/GOOGLE-DRIVE-SETUP.md`)
2. **Learn image naming** (see `/docs/ASSET-NAMING-GUIDE.md`)
3. **Understand winner workflow** (see `/docs/IMAGE-WORKFLOW.md`)

---

## 💡 Pro Tips

### Tip 1: Use URL Parameters to Override

You can test different content without editing config:

```
?hl=New+Headline&sh=New+Subheadline&btn_color=10b981
```

### Tip 2: Test Different Images

```
?img=5_kwv.jpg
```

### Tip 3: Enable All Features for Testing

```
?test_all=1
```

This enables: social proof, scarcity, progress indicator, micro-yes

### Tip 4: A/B Test Headlines

Create split test variants in config with different Calendly links:
- Control → Calendly with headline A
- Variant → Calendly with headline B
- Track which converts better in Calendly analytics

---

## 🆘 Support

**Questions?** Check these resources:
1. `/docs/` folder for detailed guides
2. GTM community forums for tag setup
3. AdKernel documentation for postback setup

---

## 📝 Changelog

### v2.1 (2026-02-24)
- ✅ Complete brand-config.json loading
- ✅ GTM-managed postbacks (no hardcoded pixels)
- ✅ Archetype/angle conditional retargeting
- ✅ Mobile image optimization
- ✅ 365-day cookie tracking
- ✅ 350+ parameter capture

---

**Built by AmplifAI Performance Stack** 🚀
