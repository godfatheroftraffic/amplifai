# HUMAN RESPONSIBILITIES - The 1% You Actually Do

## OVERVIEW

This document lists EVERYTHING a human needs to do for the Echo Master system.

**Spoiler alert:** It's not much. About 35 minutes one time.

---

## ONE-TIME SETUP (35 Minutes)

### Task 1: Create GitHub Repository (5 min)
**What:** Create a new repo for your brand  
**How:** 
1. Go to GitHub
2. Click "New repository"
3. Name: `brand-[CODE]` (e.g., `brand-kwv`)
4. Set to private
5. Clone master echo repo
6. Copy files
7. Push to your repo

**Tools needed:** GitHub account

---

### Task 2: Edit brand-config.json (10 min)
**What:** Customize 5 settings  
**How:** Open file, edit these fields:
- Brand name
- GTM container ID
- Domain
- Footer links (2-3 URLs)
- AdKernel campaign ID

**Tools needed:** Text editor

---

### Task 3: Upload Brand Assets (5 min)
**What:** Add your logo and 3-5 hero images  
**How:** 
1. Save logo as `logo.png`
2. Save hero images with clear names
3. Upload to `/public/` folder

**Tools needed:** Image files, FTP or Git

---

### Task 4: Deploy to Cloudflare (5 min)
**What:** Connect repo to Cloudflare Pages  
**How:**
1. Go to Cloudflare Pages
2. Create project
3. Connect GitHub
4. Select your repo
5. Deploy
6. Add custom domain

**Tools needed:** Cloudflare account

---

### Task 5: Add API Keys (10 min)
**What:** Add API keys for AdKernel and ad spy tools  
**How:**
1. Get keys from each platform
2. Add to Cloudflare environment variables

**Tools needed:** 
- AdKernel account
- Ad spy tool accounts

**Which keys:**
- AdKernel API key (REQUIRED)
- Meta Ads Library (optional - free)
- TikTok Creative Center (optional)
- Anstrex (optional but recommended)

---

## ONGOING RESPONSIBILITIES (5-10 Minutes Per Week)

### Task 6: Check Performance Email (5 min/week)
**What:** Review AI-generated weekly report  
**How:** 
1. Open email from AI system
2. Review top performers
3. Review recommendations
4. Approve or ignore

**Action needed:** 
- Approve budget increases for winners (optional)
- Approve new channel launches (optional)
- Everything else is automatic

---

### Task 7: Approve Major Changes (5 min/month)
**What:** Review AI recommendations for major strategy shifts  
**How:**
1. AI emails: "Recommend increasing budget 10x on CTV"
2. You reply: "Approved" or "Hold"

**Examples:**
- Scaling budget from $100/day to $1000/day
- Launching new channel
- Major creative shift

**Default:** If you don't respond, AI uses conservative approach

---

## THAT'S IT

**One-time setup:** 35 minutes  
**Ongoing:** 5-10 minutes per week

**Everything else is automated.**

---

## WHAT YOU DON'T DO (AI Does This)

❌ Generate ad copy  
❌ Create images  
❌ Write headlines  
❌ Design landing pages  
❌ Set up campaigns  
❌ Monitor performance  
❌ Adjust bids  
❌ Pause bad ads  
❌ Scale good ads  
❌ Create reports  
❌ Analyze data  
❌ Test variations  
❌ Optimize conversions  
❌ Manage budgets  
❌ Fire retargeting pixels  
❌ Send follow-up emails  
❌ Graduate campaigns to new channels  
❌ Generate videos  
❌ Select best images  
❌ Match ad to landing page  
❌ Calculate EPS/APS scores  
❌ Train ML models  
❌ Scan competitor ads  
❌ Extract winning patterns  
❌ Build audience segments  

**Literally everything above is automated.**

---

## SUPPORT

**If something breaks:**
1. Check TESTING.md for test scenarios
2. Check browser console for errors
3. Email dev team with:
   - What you were trying to do
   - What happened instead
   - Screenshot of error

**Response time:** Usually same day

**Most common issues:**
- Wrong GTM container ID → Fix in brand-config.json
- Images not loading → Check /public/ folder
- API keys missing → Add to Cloudflare env vars

---

## FINAL THOUGHTS

**This system was designed so AI does 99% of the work.**

Your job is literally:
1. Set it up once (35 min)
2. Check emails weekly (5 min)
3. Approve big changes occasionally (5 min)
4. **Collect revenue** 💰

That's it. That's the whole job.

If you're doing more than this, something is configured wrong.

**Contact support and we'll fix it.**

---
