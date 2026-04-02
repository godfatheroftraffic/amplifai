# ECHO MASTER - DEPLOYMENT GUIDE

## Overview
This is the Master Echo Landing Page repository. All brand deployments copy from here and customize only `brand-config.json`.

---

## Quick Start Deployment

## HUMAN QUICK START (35 Minutes Total)

### STEP 1: Create Brand Repo (5 minutes)

**What You Do:**
1. Go to GitHub
2. Click "New repository"
3. Name it: `brand-kwv` (replace `kwv` with your brand code)
4. Make it private
5. Clone the master echo repo
6. Copy all files to your brand repo
7. Push to GitHub

**Command Line (Copy/Paste):**
```bash
# Clone master
git clone https://github.com/amplifai/echo-lp-master.git

# Copy to new brand folder
cp -r echo-lp-master brand-kwv
cd brand-kwv

# Initialize as new repo
git init
git add .
git commit -m "Initial brand setup"
git remote add origin https://github.com/yourorg/brand-kwv.git
git push -u origin main
```

---

### STEP 2: Customize brand-config.json (10 minutes)

**What You Do:**
Open `brand-config.json` and fill in these 5 things:
```json
{
  "brand": {
    "name": "Killer Whale Ventures",              // ← Your brand name
    "gtmId": "GTM-T639H2SD",                      // ← Get from GTM dashboard
    "domain": "lp.killerwhaleventures.com",       // ← Your landing page domain
    "copyright": "© 2024 Killer Whale Ventures"   // ← Your copyright
  }
}
```

**Then scroll down and update:**

1. **Footer links** (your privacy policy, terms, contact page)
2. **Default headline/CTA** (optional - can be overridden by AI)

**Save the file. That's it.**

---

### STEP 3: Add Your Logo & Images (5 minutes)

**What You Do:**
1. Put your logo in: `/public/logo.png`
2. Add 3-5 hero images to `/public/` folder

**AI will automatically:**
- Select best image per ad
- Generate new images as needed
- Test which images convert best

---

### STEP 4: Deploy to Cloudflare (5 minutes)

**What You Do:**
1. Go to [Cloudflare Pages](https://dash.cloudflare.com/)
2. Click "Create a project"
3. Click "Connect to Git"
4. Select your brand repo
5. Build settings:
   - Framework: **None**
   - Build command: **Leave blank**
   - Output directory: **/**
6. Click "Save and Deploy"
7. Wait 2 minutes for deployment
8. Click "Custom domains"
9. Add sub domain: `lp.yourbrand.com`
10. Done!

**Cloudflare automatically:**
- Builds your site
- Adds SSL certificate
- Sets up CDN
- Handles all traffic

---

### STEP 5: Connect API Keys (10 minutes)

**What You Do:**
In Cloudflare Pages → Settings → Environment variables, add:

API KEYS
ADKERNEL_API_KEY = your_key_here
META_ADS_API_KEY = your_key_here
TIKTOK_API_KEY = your_key_here
ANSTREX_API_KEY = your_key_here

**Where to get API keys:**
- **AdKernel:** Dashboard → Settings → API
- **Meta Ads Library:** Free, no key needed (public API)
- **TikTok Creative Center:** ads.tiktok.com → API
- **Anstrex:** anstrex.com → Account → API

**AI will automatically:**
- Connect to all platforms
- Pull top ads daily
- Extract patterns
- Generate new ads
- Launch campaigns
- Optimize performance

---

## ✅ THAT'S IT! 

**You did 35 minutes of work.**  
**AI now runs everything forever.**

---

## WHAT HAPPENS NEXT (AI Does This Automatically):

### First 24 Hours:
1. AI scans 10,000+ top ads
2. AI generates 100 ad variations
3. AI launches on push traffic ($100 budget)
4. AI monitors performance hourly
5. AI pauses 80% (losers)
6. AI scales 20% (winners)

### Day 2-7:
1. AI generates 100 more ads based on Day 1 learnings
2. AI graduates top 20 push ads to native
3. AI tests landing page variations with pop traffic
4. AI learns which images + headlines convert best
5. AI builds winning combinations database

### Week 2+:
1. AI scales winners to display
2. AI creates videos from proven scripts
3. AI launches on CTV with confidence
4. AI continuously optimizes everything
5. AI reports performance to you via email

### Forever:
1. AI monitors 10,000+ ads daily
2. AI generates 100+ variations daily
3. AI optimizes across all channels
4. AI scales budget to winners
5. **You just check email reports and collect revenue**

---
---

## Testing Deployment

### Test Landing Page
```
https://lp.yourbrand.com/?hl=Test%20Headline&cta=Click%20Here&img=your-image.jpg
```

Should display:
- Your brand's GTM container loading
- Custom headline/CTA from URL params
- Background image from /public/ folder
- Footer with your brand's links

### Test Conversion Tracker
```
https://lp.yourbrand.com/conversion-tracker.html?testsurvey=high_eps&dest=https://calendly.com/yourbrand/meeting
```

Should:
- Show progress bar
- Console logs show EPS/APS scores
- Redirect after 3 seconds
- GTM events fire

See TESTING.md for complete test scenarios.

---

## Updating from Master

When master repo is updated:

```bash
# In your brand repo
git remote add master https://github.com/yourusername/echo-lp-master.git
git fetch master
git merge master/main --no-commit

# Review changes, keep your brand-config.json
git checkout --ours brand-config.json

# Commit merge
git commit -m "Update from master"
```

---

## File Structure

```
/brand-echo-repo/
  ├── index.html                    ← Landing page (loads brand-config.json)
  ├── conversion-tracker.html       ← Conversion bridge (loads brand-config.json)
  ├── .gitignore                    ← Prevents config overwrites
  ├── public/
  │   ├── .gitkeep
  │   ├── brand-hero-image.jpg      ← Your brand images
  │   └── brand-logo.png
  └── docs/                         ← Reference only
         ── brand-config.json             ← CUSTOMIZE THIS FILE ONLY
```

---

## Support

See other docs:
- **TESTING.md** - Test scenarios for landing page & converter
- **BRAND-CONFIG-GUIDE.md** - Detailed config options
- **README.md** - Project overview

Questions? Check GitHub docs or contact @godfatheroftraffic
