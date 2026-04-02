# 📁 MASTER FILES MANIFEST

## PURPOSE
This document lists ALL master files that should NEVER be replaced from scratch.
Claude must ALWAYS start from these files when making updates.

---

## 🎯 MASTER FILE: index__1_.html

**Location:** `/mnt/user-data/uploads/index__1_.html`

**Size:** 852 lines (26KB)

**Last Updated:** 2026-02-28

**Contains:**
- ✅ All 27 Echo personalization parameters
- ✅ Social proof popup system
- ✅ Scarcity messaging system
- ✅ Micro-yes checkbox system
- ✅ Progress indicator system
- ✅ test_all parameter support
- ✅ URL-based styling (btn_color, btn_size, btn_style, overlay, font)
- ✅ Dynamic content replacement (hl, sh, cta, img)
- ✅ brand-config.json loading
- ✅ AdKernel parameter handling
- ✅ Keitaro parameter handling

**Critical Features:**
```javascript
// Lines 467-471: test_all parameter
if (params.test_all === "1") {
  params.social_proof = "on";
  params.scarcity = params.scarcity || "3";
  params.progress = params.progress || "1";
  params.micro_yes = "on";
}

// Lines 26-27: Social proof & scarcity elements
<div id="scarcity" data-default="Only {N} spots remaining today">
<div id="social-proof">

// Lines 619: Complete parameter list
var contentParams = ["hl", "sh", "img", "link", "btn_color", ...];
```

**⚠️ DO NOT:**
- Start from scratch
- Remove any existing features
- Reduce line count below 852

**✅ DO:**
- Use this as BASE for all updates
- Add new features on top
- Preserve all existing functionality
- Increase line count when adding features

---

## 🎯 MASTER FILE: conversion-tracker-FINAL.html

**Location:** `/mnt/user-data/outputs/conversion-tracker-FINAL.html`

**Size:** 49KB

**Last Updated:** Earlier session (need to verify date)

**Contains:**
- ✅ Conversion bridge functionality
- ✅ Auto-redirect to thank-you page
- ✅ GTM event firing
- ✅ Parameter pass-through
- ✅ Progress animation
- ✅ Webhook support

**Critical Features:**
- 3-second auto-redirect
- Full parameter preservation
- Conversion tracking events

**⚠️ DO NOT:**
- Start from scratch
- Remove redirect logic

---

## 🎯 MASTER FILE: thank-you-FINAL.html

**Location:** `/mnt/user-data/outputs/thank-you-FINAL.html`

**Size:** 26KB

**Last Updated:** Earlier session (need to verify date)

**Contains:**
- ✅ Thank you confirmation
- ✅ GTM conversion events
- ✅ Parameter storage
- ✅ Success messaging
- ✅ Optional redirect

**Critical Features:**
- Final conversion tracking
- Parameter completion
- Success state

---

## 📊 MASTER FILE VERIFICATION CHECKLIST

Before making ANY changes, verify:

- [ ] Master file exists in specified location
- [ ] Current line count recorded
- [ ] All features documented above are present
- [ ] File is copied to /home/claude as working copy
- [ ] Original master preserved in uploads/outputs

After making changes, verify:

- [ ] New line count >= old line count
- [ ] All original features still present
- [ ] New features added successfully
- [ ] File tested and working
- [ ] User approval obtained

---

## 🚨 CRITICAL RULES

1. **NEVER start from scratch** - Always use master as base
2. **NEVER reduce features** - Only add, never subtract
3. **NEVER reduce line count** - New >= old always
4. **ALWAYS preserve** - Keep all existing functionality
5. **ALWAYS verify** - Test before delivery

---

**Last Updated:** 2026-03-01
**Maintained By:** Claude (with user oversight)
