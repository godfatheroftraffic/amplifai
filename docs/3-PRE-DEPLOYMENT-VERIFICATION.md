# 🔍 PRE-DEPLOYMENT VERIFICATION PROTOCOL

## PURPOSE
This protocol MUST be followed before delivering ANY files to the user.
It prevents delivering broken or incomplete work.

---

## ✅ STEP 1: LINE COUNT VERIFICATION

**Rule:** New files MUST have >= lines than old files (never fewer)

```bash
# Check index.html
wc -l /mnt/user-data/uploads/index__1_.html
wc -l /home/claude/index-v2.3-FINAL.html

# PASS if new >= 852 lines
# FAIL if new < 852 lines
```

**Results:**
- Old index.html: 852 lines
- New index.html: _____ lines
- Status: PASS / FAIL

**If FAIL:** DO NOT DELIVER. Find what was removed and add it back.

---

## ✅ STEP 2: FEATURE GREP VERIFICATION

**Rule:** All features in old file MUST exist in new file

```bash
# Test for Echo features
grep -c "social_proof" /mnt/user-data/uploads/index__1_.html  # Should be 5+
grep -c "social_proof" /home/claude/index-v2.3-FINAL.html     # Must be >= old

grep -c "scarcity" /mnt/user-data/uploads/index__1_.html
grep -c "scarcity" /home/claude/index-v2.3-FINAL.html

grep -c "micro_yes" /mnt/user-data/uploads/index__1_.html
grep -c "micro_yes" /home/claude/index-v2.3-FINAL.html

grep -c "test_all" /mnt/user-data/uploads/index__1_.html
grep -c "test_all" /home/claude/index-v2.3-FINAL.html
```

**Results:**
| Feature | Old Count | New Count | Status |
|---------|-----------|-----------|--------|
| social_proof | _____ | _____ | PASS/FAIL |
| scarcity | _____ | _____ | PASS/FAIL |
| micro_yes | _____ | _____ | PASS/FAIL |
| test_all | _____ | _____ | PASS/FAIL |
| progress | _____ | _____ | PASS/FAIL |

**If ANY FAIL:** DO NOT DELIVER. Add missing features.

---

## ✅ STEP 3: GTM EVENT VERIFICATION

**Rule:** All required GTM events MUST be present

```bash
# Check for all 11 events
grep "echo_lp_view" /home/claude/index-v2.3-FINAL.html
grep "master_lp_view_retargeting" /home/claude/index-v2.3-FINAL.html
grep "echo_cta_click" /home/claude/index-v2.3-FINAL.html
grep "dsp_postback" /home/claude/index-v2.3-FINAL.html
grep "master_lp_click_retargeting" /home/claude/index-v2.3-FINAL.html

# Repeat for tracker and thank-you files
```

**Results:**
- [ ] echo_lp_view present
- [ ] master_lp_view_retargeting present
- [ ] echo_cta_click present
- [ ] dsp_postback present (3 times - step_1, step_2, step_3)
- [ ] master_lp_click_retargeting present
- [ ] conversion_bridge_loaded present
- [ ] lead_conversion present
- [ ] master_lead_retargeting present
- [ ] thankyou_conversion present
- [ ] master_converted_retargeting present

**If ANY missing:** DO NOT DELIVER. Add missing events.

---

## ✅ STEP 4: PARAMETER NAMING VERIFICATION

**Rule:** Must use CORRECT parameter names (NOT _id suffixes)

```bash
# Check for CORRECT names
grep "conversion:" /home/claude/index-v2.3-FINAL.html  # Should exist
grep "campaign:" /home/claude/index-v2.3-FINAL.html    # Should exist

# Check for WRONG names (should NOT exist in dataLayer pushes)
grep "conversion_id:" /home/claude/index-v2.3-FINAL.html  # Should NOT in dataLayer
grep "campaign_id:" /home/claude/index-v2.3-FINAL.html    # Should NOT in dataLayer
```

**Results:**
- [ ] Uses `conversion` (not conversion_id)
- [ ] Uses `campaign` (not campaign_id)
- [ ] Uses `banner` (not banner_id)
- [ ] Uses `publisher` (not publisher_id)
- [ ] Uses `at` (archetype)
- [ ] Uses `ag` (angle)

**If WRONG names found:** DO NOT DELIVER. Fix parameter names.

---

## ✅ STEP 5: FOOTER & BRANDING VERIFICATION

**Rule:** All branding elements MUST be present

```bash
# Check for footer elements
grep -c "footer" /home/claude/index-v2.3-FINAL.html
grep -c "social-icon" /home/claude/index-v2.3-FINAL.html
grep -c "brand-config" /home/claude/index-v2.3-FINAL.html
```

**Visual check required:**
- [ ] Footer visible at bottom
- [ ] Logo displays (if enabled)
- [ ] 6 social icons display (if enabled)
- [ ] Icons use inline SVG
- [ ] Icons hover effect works
- [ ] Footer links present
- [ ] Legal consent text below CTA
- [ ] Mobile responsive

**If ANY missing:** DO NOT DELIVER. Add missing elements.

---

## ✅ STEP 6: DOCUMENTATION CROSS-CHECK

**Rule:** Implementation MUST match ALL documentation

Check against these docs:
- [ ] COMPLETE-PARAMETER-MASTER-REFERENCE-v2.0.md
- [ ] ECHO-MASTER-IMPLEMENTATION-GUIDE.md
- [ ] GTM-COMPLETE-VARIABLE-LIST.md
- [ ] REQUIRED-FEATURES-CHECKLIST.md

**Process:**
1. Open each doc
2. Find relevant sections
3. Verify implementation matches
4. Check off when verified

**If MISMATCH found:** DO NOT DELIVER. Fix to match docs.

---

## ✅ STEP 7: REQUIRED-FEATURES-CHECKLIST COMPLETION

**Rule:** ALL boxes in 2-REQUIRED-FEATURES-CHECKLIST.md MUST be checked

```bash
# Count unchecked boxes
grep "\- \[ \]" /mnt/user-data/outputs/2-REQUIRED-FEATURES-CHECKLIST.md | wc -l
# Should be 0
```

**Results:**
- Unchecked boxes remaining: _____
- Status: PASS (0) / FAIL (>0)

**If FAIL:** DO NOT DELIVER. Complete missing features.

---

## ✅ STEP 8: USER TESTING

**Rule:** User MUST test before final approval

**Provide user with:**
1. Test URLs with all features enabled
2. Expected behavior for each test
3. Checklist of what to verify
4. Screenshots of expected results

**User must verify:**
- [ ] All Echo features work
- [ ] All GTM events fire
- [ ] Social icons display
- [ ] Footer shows correctly
- [ ] Mobile responsive
- [ ] Full funnel works

**User approval:** YES / NO

**If NO:** DO NOT DELIVER. Fix issues and re-test.

---

## ✅ STEP 9: FINAL FILE COMPARISON

**Rule:** Verify EXACTLY what's being delivered

```bash
# List all files being delivered
ls -lh /home/claude/*FINAL*.html
ls -lh /home/claude/*v2.3*.html

# Show file sizes
du -h /home/claude/index-v2.3-FINAL.html
du -h /home/claude/tracker-v2.3-FINAL.html
du -h /home/claude/thank-you-v2.3-FINAL.html
du -h /home/claude/brand-config-v3.0-FINAL.json
```

**Delivery manifest:**
| File | Size | Line Count | Status |
|------|------|------------|--------|
| index-v2.3-FINAL.html | _____ | _____ | PASS/FAIL |
| tracker-v2.3-FINAL.html | _____ | _____ | PASS/FAIL |
| thank-you-v2.3-FINAL.html | _____ | _____ | PASS/FAIL |
| brand-config-v3.0-FINAL.json | _____ | _____ | PASS/FAIL |

**All files PASS?** YES / NO

---

## ✅ STEP 10: FINAL APPROVAL CHECKPOINT

**Before calling present_files tool:**

- [ ] Line count >= old files
- [ ] Feature grep passed
- [ ] GTM events verified
- [ ] Parameter names correct
- [ ] Footer/branding present
- [ ] Documentation matches
- [ ] Checklist 100% complete
- [ ] User tested and approved
- [ ] File comparison done
- [ ] No errors in console
- [ ] Ready for production

**FINAL STATUS:** APPROVED / REJECTED

**Approved by:** __________
**Date:** __________
**Time:** __________

---

## 🚨 CRITICAL FAILURE MODES

**If ANY of these occur, STOP and FIX:**

❌ New file has FEWER lines than old file
❌ Feature grep shows missing features
❌ GTM events missing
❌ Wrong parameter names (_id suffixes)
❌ Footer/branding missing
❌ Documentation mismatch
❌ Checklist incomplete
❌ User found bugs
❌ Console errors
❌ Tests failing

**DO NOT DELIVER until ALL issues resolved.**

---

## 📝 DELIVERY PROTOCOL

**Only after ALL verifications PASS:**

1. Copy files to /mnt/user-data/outputs/
2. Call present_files tool
3. Provide user with:
   - File list
   - What changed
   - What was added
   - Test instructions
   - Deployment guide

4. Get user confirmation of receipt
5. Document delivery in changelog

---

**Last Updated:** 2026-03-01
**Maintained By:** Claude (with user oversight)
