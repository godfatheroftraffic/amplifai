# ASSET NAMING CONVENTION GUIDE v2.1

## Overview

This guide defines the **number-first naming convention** for all creative assets across AmplifAI's advertising system.

**Key Principle:** Number comes first for natural sorting, human readability, and easy cross-channel repurposing.

**Critical Distinction:** Ad creatives (Google Drive) are separate from landing page images (GitHub repository).

---

## TWO IMAGE SYSTEMS

### **1. AD CREATIVES (Google Drive + AdKernel)**
- Uploaded to Google Drive
- Uploaded to AdKernel campaigns
- **NOT** in GitHub repository
- Format-specific sizes (300x250, native, push, etc.)

### **2. LANDING PAGE IMAGES (GitHub /public/)**
- Hero/background images only
- Desktop + Mobile versions
- Deployed via GitHub → Cloudflare
- Same image parameter across ALL ad channels

---

## AD CREATIVE NAMING (Google Drive)

### Base Format:
```
{number}_{brandcode}_{format}.{ext}

Examples:
4_kwv_300x250.jpg
4_kwv_native.jpg
4_kwv_push.jpg
```

### Format Suffixes:

| Channel | Format | Example | Dimensions |
|---------|--------|---------|------------|
| **Display 300x250** | `_300x250` | `4_kwv_300x250.jpg` | 300x250px |
| **Display 728x90** | `_728x90` | `4_kwv_728x90.jpg` | 728x90px |
| **Display 970x250** | `_970x250` | `4_kwv_970x250.jpg` | 970x250px |
| **Display 160x600** | `_160x600` | `4_kwv_160x600.jpg` | 160x600px |
| **Native** | `_native` | `4_kwv_native.jpg` | 1200x627px |
| **Push** | `_push` | `4_kwv_push.jpg` | 192x192px |
| **Video Thumbnail** | `_video` | `4_kwv_video.jpg` | 1920x1080px |
| **Video File** | `_video` | `4_kwv_video.mp4` | 1920x1080px |

---

## LANDING PAGE IMAGE NAMING (GitHub /public/)

### Base Format:
```
{number}_{brandcode}.jpg          → Desktop version
{number}_{brandcode}_mobile.jpg   → Mobile version

Examples:
4_kwv.jpg          → Desktop hero (1920x1080px)
4_kwv_mobile.jpg   → Mobile hero (750x1334px, optimized)
```

### Why Two Versions?

**80% of traffic is mobile** → Mobile images must load lightning fast

| Version | Dimensions | File Size | Purpose |
|---------|------------|-----------|---------|
| Desktop | 1920x1080px | ~300-500KB | Desktop/tablet hero |
| Mobile | 750x1334px | ~80-150KB | Mobile-optimized |

### Mobile Optimization:
- Smaller dimensions (750x1334px vs 1920x1080px)
- Compressed file size (80-150KB vs 300-500KB)
- Faster load times (critical for mobile)
- Same visual composition

---

## GOOGLE DRIVE FOLDER STRUCTURE

```
[BRAND] - Creative Assets/
└── AD_IMAGES/
    ├── Top/                    ← Winner ad creatives only
    │   ├── 4_kwv_native.jpg
    │   └── 47_kwv_native.jpg
    │
    ├── Display/
    │   ├── 300x250/
    │   │   ├── 4_kwv_300x250.jpg
    │   │   └── 47_kwv_300x250.jpg
    │   ├── 728x90/
    │   │   ├── 4_kwv_728x90.jpg
    │   │   └── 47_kwv_728x90.jpg
    │   ├── 970x250/
    │   │   └── 4_kwv_970x250.jpg
    │   └── 160x600/
    │       └── 4_kwv_160x600.jpg
    │
    ├── Native/
    │   ├── 4_kwv_native.jpg
    │   └── 47_kwv_native.jpg
    │
    ├── Push/
    │   ├── 4_kwv_push.jpg
    │   └── 47_kwv_push.jpg
    │
    └── Video/
        ├── 4_kwv_video.jpg    (thumbnail)
        ├── 4_kwv_video.mp4    (video file)
        ├── 47_kwv_video.jpg
        └── 47_kwv_video.mp4
```

**Management:** Google Drive only  
**Upload to:** AdKernel campaigns  
**NOT** synced to GitHub

---

## GITHUB REPOSITORY STRUCTURE

```
/public/
├── logo.png
├── 4_kwv.jpg              ← Desktop hero
├── 4_kwv_mobile.jpg       ← Mobile hero
├── 5_kwv.jpg
├── 5_kwv_mobile.jpg
├── 21_kwv.jpg
└── 21_kwv_mobile.jpg
```

**Management:** GitHub repository  
**Deployment:** Cloudflare Pages  
**Purpose:** Landing page backgrounds only

---

## AD NAMING CONVENTION

Ads use a structured naming format:

### Format:
```
P{phase}_AT{archetype}_AG{angle}_V{variant}

Where:
- P = Phase (1-7)
- AT = Archetype (1-5)
- AG = Angle (1-5)
- V = Variant number (matches image number)
```

### Examples:
```
P1_AT2_AG3_V004    → Uses image 4
P2_AT1_AG4_V005    → Uses image 5
P3_AT2_AG1_V047    → Uses image 47
```

### AdKernel Banner ID Mapping:
```
AdKernel Auto-Assigns Banner IDs:

banner_id | ad_variation    | image      | channel
12345     | P1_AT2_AG3_V004 | 4_kwv.jpg  | native
12346     | P1_AT2_AG3_V004 | 4_kwv.jpg  | display
12347     | P1_AT2_AG3_V004 | 4_kwv.jpg  | push

We map banner_id → ad_variation in reports
```

---

## URL PARAMETER USAGE

### In All Ad URLs (Same Parameter):
```
Landing page URL parameter:
?img=4_kwv.jpg

Used for ALL channels:
- Display ads → ?img=4_kwv.jpg
- Native ads → ?img=4_kwv.jpg
- Push ads → ?img=4_kwv.jpg
- Video ads → ?img=4_kwv.jpg
```

### Landing Page Logic:
```javascript
// URL: ?img=4_kwv.jpg
// System auto-detects mobile vs desktop

if (isMobile) {
  load '/public/4_kwv_mobile.jpg'
} else {
  load '/public/4_kwv.jpg'
}
```

### One Master Echo Landing Page:
- ✅ Same URL parameter across ALL channels
- ✅ Same landing page template
- ✅ Automatic mobile/desktop detection
- ✅ No channel-specific pages needed

---

## SPECIAL CAMPAIGN SUFFIXES

For retargeting, holidays, or customer stage-specific campaigns:

### Ad Creatives (Google Drive):
```
4_kwv_native.jpg           → Standard
4_kwv_retarget_native.jpg  → Retargeting only
4_kwv_holiday_native.jpg   → Holiday campaign only
4_kwv_stage2_native.jpg    → Customer stage 2 only
```

### Landing Page Images (GitHub):
```
4_kwv.jpg                  → Standard desktop
4_kwv_mobile.jpg           → Standard mobile
4_kwv_retarget.jpg         → Retargeting desktop
4_kwv_retarget_mobile.jpg  → Retargeting mobile
4_kwv_holiday.jpg          → Holiday desktop
4_kwv_holiday_mobile.jpg   → Holiday mobile
```

### AI Campaign Rules:
```
AI knows:
- Load 4_kwv_retarget.jpg ONLY in retargeting campaigns
- Load 4_kwv_holiday.jpg ONLY during holiday campaigns
- Never mix standard with special campaign images
```

---

## BRAND CODES

Each brand gets a 2-4 letter code:

| Brand | Code |
|-------|------|
| Killer Whale Ventures | `kwv` |
| Your Brand Name | `ybr` |
| Example Corp | `exc` |

**Rule:** Lowercase, no spaces, memorable abbreviation

---

## WINNER REPURPOSING WORKFLOW

### Step 1: Identify Winner in Google Drive
```
Testing: Native ads in Google Drive
Winner: 47_kwv_native.jpg
Performance: 6.1% CTR, $7.50 CPA
```

### Step 2: AI Creates Landing Page Versions
```
AI generates for GitHub /public/:
- 47_kwv.jpg (1920x1080px desktop)
- 47_kwv_mobile.jpg (750x1334px mobile)

Commits to GitHub → Cloudflare auto-deploys
```

### Step 3: AI Creates All Ad Format Versions
```
AI generates for Google Drive:
- 47_kwv_300x250.jpg
- 47_kwv_728x90.jpg
- 47_kwv_970x250.jpg
- 47_kwv_160x600.jpg
- 47_kwv_push.jpg
- 47_kwv_video.jpg + .mp4

Uploads to Google Drive AD_IMAGES folders
```

### Step 4: Upload to AdKernel
```
PM or AI uploads from Google Drive to AdKernel:
- Display campaigns get display sizes
- Native campaigns get native size
- Push campaigns get push size
- Video campaigns get video files

AdKernel assigns banner IDs automatically
```

### Step 5: Launch Cross-Channel Campaigns
```
All ads use same landing page URL:
?img=47_kwv.jpg

Landing page auto-loads:
- Desktop: 47_kwv.jpg
- Mobile: 47_kwv_mobile.jpg
```

---

## SORTING & REPORTING

### Natural Sort Order:
```
✅ Number-first sorts correctly:
4_kwv.jpg
5_kwv.jpg
21_kwv.jpg
47_kwv.jpg

❌ Brand-first breaks sorting:
kwv_4.jpg
kwv_11.jpg   ← Comes before kwv_5
kwv_5.jpg
```

---

**Last Updated:** 2026-02-24  
**Version:** 2.1  
**Maintained By:** AmplifAI Performance Stack
