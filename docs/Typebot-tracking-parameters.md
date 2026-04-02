# AmplifAI TypeBot Universal Intelligence Schema
## Tracking Parameters Reference & Setup Guide
**Version:** 1.0  
**System:** AmplifAI Acquisition OS  
**Applies to:** All brands using the AmplifAI Echo Funnel + TypeBot stack

---

## Table of Contents
1. [What This Document Is](#1-what-this-document-is)
2. [New Parameters Added in This Version](#2-new-parameters-added-in-this-version)
3. [Complete Parameter Reference](#3-complete-parameter-reference)
4. [TypeBot Setup: Step-by-Step](#4-typebot-setup-step-by-step)
5. [How Parameters Flow Through the System](#5-how-parameters-flow-through-the-system)
6. [brand-config.json New Sections](#6-brand-configjson-new-sections)
7. [Computed Variable Logic](#7-computed-variable-logic)
8. [GTM DataLayer Reference](#8-gtm-datalayer-reference)
9. [Conversion Tracker Redirect URL Structure](#9-conversion-tracker-redirect-url-structure)
10. [Validation Checklist](#10-validation-checklist)

---

## 1. What This Document Is

This document defines every tracking parameter that flows through the AmplifAI TypeBot funnel system. It tells you:

- **Which parameters are new** (added in this version)
- **Where each parameter comes from** (AdKernel, quiz answer, computed)
- **How to declare each variable in TypeBot**
- **How each variable reaches the conversion tracker**
- **What each variable is used for downstream**

> **CRITICAL NAMING RULE:** AdKernel does NOT use `_id` suffixes. Use `conversion` not `conversion_id`. Use `campaign` not `campaign_id`. See [AdKernel Core Parameters](#layer-1--adkernel-core-tracking) for the complete list of correct names.

> **UNIVERSAL ARCHITECTURE RULE:** All brand-specific values live EXCLUSIVELY in brand-config.json. Code reads from brand-config — it never contains brand values. Pain signals, desire signals, qualification gates, routing rules, income tiers, disqualification conditions, conversion types, copy variants — all in brand-config. Instructions reference brand-config keys, not specific values. This document is vertical-agnostic.

> **ROUTING RULE:** Disqualification routing is managed inside the TypeBot flow via native Condition blocks. The AI builds those Condition blocks by reading routing rules from brand-config. The disqualify redirect URL is always read from brand-config.conversion_event.disqualify_redirect — never hardcoded.

---

## 2. New Parameters Added in This Version

The following parameters are **new** in v1.0 of the Universal Schema. They did not exist in the previous BBM funnel build and must be added to:

- TypeBot variable declaration
- brand-config.json
- GTM dataLayer push
- Conversion tracker URL

### New Framework Psychology Variables
| Parameter | Why Added | Used By |
|-----------|-----------|---------|
| `market_sophistication` | Schwartz market awareness level — drives creative rotation | Ad targeting, creative library |
| `awareness_stage` | Computed from signal cascade — drives sequence selection | Email, SMS, retargeting |
| `pain_primary` | Alias for `pain_obstacle` — Bencivenga gap calculation | All downstream copy |
| `desire_primary` | Bencivenga desire side of gap — drives offer framing | Email, messaging framing |
| `motivation_type` | **THE marketing switch** — `pain` or `desire` — forks all copy | Every downstream touchpoint |
| `identity_type` | Tribal identity the user confirmed — drives echo protocol | persona, sales framing |
| `commitment_depth` | Count of quiz questions answered — Cialdini investment signal | APS, main conversion rate prediction |
| `cognitive_engagement_depth` | Time-weighted deliberation score — premium buyer detection | Sales routing |
| `belief_barrier` | Computed obstacle + identity string — objection pre-handle | Sales pre-brief |
| `brand_profile_summary` | Master personalization string — all downstream AI reads this | Every AI touchpoint |

### New Behavioral Signal Variables
| Parameter | Why Added | Used By |
|-----------|-----------|---------|
| `steps_completed` | Quiz completion depth — commitment measurement | LQS, APS, recovery |
| `quiz_completion_time` | Time from quiz open to lead capture | Buyer type segmentation |
| `drop_off_point` | Last question reached before abandon | Recovery sequence targeting |
| `post_booking_priority` | Post-conversion micro-commitment | Show rate signal, sales opener |

### New Conversion Event Variables (Universal)
| Parameter | Why Added | Used By |
|-----------|-----------|---------|
| `conversion_type` | Replaces booking-specific variables — works for any conversion | GTM routing, postback |
| `conversion_status` | Tracks booking state | Reminder triggers |
| `conversion_value` | Dollar value per conversion type | ROI, LTV tracking |
| `conversion_platform` | Platform handling conversion | API routing |

### New Lead Quality Score Inputs
| Parameter | Why Added | Used By |
|-----------|-----------|---------|
| `income_qualified` | Boolean — cleared income gate | LQS weight: +20 |
| `motivation_type_detected` | Boolean — signal cascade produced result | LQS weight: +10 |
| `awareness_stage_detected` | Boolean — computed successfully | LQS weight: +5 |

---

## 3. Complete Parameter Reference

### Layer 1 — AdKernel Core Tracking
**Source:** AdKernel macros in campaign URL  
**TypeBot:** Hidden variables, auto-injected via URL params  
**Save in Results:** YES  

| Parameter | AdKernel Macro | Type | Description |
|-----------|----------------|------|-------------|
| `conversion` | `{conversion}` | String | **PRIMARY** unique click ID. Never use `conversion_id`. |
| `campaign` | `{campaign}` | String | Campaign identifier. Never use `campaign_id`. |
| `banner` | `{banner}` | String | Creative/banner ID. Never use `banner_id`. |
| `publisher` | `{publisher}` | String | Traffic source ID. Never use `publisher_id`. |
| `offer` | `{offer}` | String | Offer identifier. |
| `goal_id` | `{goal_id}` | String | Conversion goal ID for Adkernel XML suite postback routing. |

---

### Layer 2 — AdKernel Personalization
**Source:** AdKernel native parameters  
**TypeBot:** Hidden variables, auto-injected  
**Save in Results:** YES 

> ⚠️ **Capitalization required:** `State_Name` (capital S and N), `Keyword` (capital K), `Query` (capital Q)

| Parameter | AdKernel Macro | Type | Notes |
|-----------|----------------|------|-------|
| `city` | `{city}` | String | Hyper-local personalization |
| `country_name` | `{country_name}` | String | Full country name |
| `region` | `{region}` | String | State/province |
| `State_Name` | `{State_Name}` | String | Full state name — capitals required |
| `device_type` | `{device_type}` | String | mobile / desktop / tablet |
| `os` | `{os}` | String | iOS / Android / Windows |
| `device_brand` | `{device_brand}` | String | Apple / Samsung / etc |
| `carrier` | `{carrier}` | String | Mobile carrier |
| `day_of_week` | `{day_of_week}` | String | Monday–Sunday |
| `date` | `{date}` | String | Click date |
| `ip` | `{ip}` | String | IP address — Save in Results: YES |
| `pubzone` | `{pubzone}` | String | Publisher zone/placement |
| `bid` | `{bid}` | Number | Bid amount in dollars |

---

### Layer 3 — Avalanche Intelligence Tokens
**Source:** URL parameters from ad → landing page  
**TypeBot:** Hidden variables, auto-injected  
**Save in Results:** YES  

| Parameter | Type | Values | Description |
|-----------|------|--------|-------------|
| `cta` | String | Echo CTA from ad |
| `at` | String | 1-5 | Archetype slot |
| `ag` | String | 1-5 | Angle slot |
| `ad` | String | P1_AT2_AG3_V007 | Full creative DNA string |
| `phase` | String | P1 \| P2 \| P3 \| P4 \| P5 | Funnel journey phase |
| `eps` | Number | 0-100 | Estimated Predictive Score at ad request and ad click |
| `av` | String | v1 \| v2 \| test-a | Ad variation ID |
| `mb` | String | Buyer ID | Media buyer identifier |
| `hl` | String | Headline text | Ad headline used |
| `sl` | String | Sub Headline text | Ad Sub headline used |

---

### Layer 4 — Framework Psychology Variables
**Source:** Signal cascade (ad → CTA → quiz → computed)  
**TypeBot:** Some captured via quiz input blocks, some computed via Set Variable blocks  
**Save in Results:** YES  

| Parameter | Input Type | Source | Values |
|-----------|-----------|--------|--------|
| `market_sophistication` | Set Variable | brand-config.json | 1-5 integer |
| `awareness_stage` | Set Variable (computed) | ag + cta + quiz | unaware \| problem_aware \| solution_aware \| product_aware |
| `pain_experience` | Choice input | Quiz question | Defined in brand-config |
| `pain_obstacle` | Choice input | Quiz question | Defined in brand-config |
| `pain_primary` | Set Variable | = pain_obstacle value | Same as pain_obstacle |
| `desire_primary` | Choice input | Quiz question | Defined in brand-config |
| `desire_values` | Multi-select input | Quiz question | Comma-separated selected values |
| `motivation_type` | Set Variable (computed) | Signal cascade | **pain** \| **desire** |
| `identity_type` | Choice input | Quiz question | Defined in brand-config |
| `commitment_depth` | Set Variable (computed) | = steps_completed | 0-10 |
| `cognitive_engagement_depth` | Set Variable (computed) | Time-weighted | 0-10 scale |
| `verification_type` | Choice input | Quiz question | phone-call \| video-call |
| `belief_barrier` | Set Variable (computed) | pain_obstacle + identity_type | Constructed string |

---

### Layer 5 — Demographics
**Source:** TypeBot quiz input blocks  
**Save in Results:** YES  

| Parameter | Input Type | Values | Notes |
|-----------|-----------|--------|-------|
| `demo_age` | Numeric input | 18-99 | Free numeric |
| `demo_income` | Choice input | Defined in brand-config | **QUALIFICATION GATE** |
| `demo_gender` | Choice input | Defined in brand-config | Optional per brand |

---

### Layer 6 — Brand Slots
**Source:** TypeBot picture choice / choice / multi-select input blocks  
**Save in Results:** YES  
**Configuration:** brand-config.json `brand_slots` section  

| Parameter | Input Type | Notes |
|-----------|-----------|-------|
| `brand_q1` | Picture choice | Highest-value visual question |
| `brand_q2` | Picture choice | Second visual preference |
| `brand_q3` | Picture choice or choice | Third preference |
| `brand_q4` | Choice | Demographic preference |
| `brand_q5` | Multi-select | Values/personality selection |

---

### Layer 7 — Lead Capture
**Source:** TypeBot text/email/phone input blocks  
**Save in Results:** YES  

| Parameter | Input Type | Format |
|-----------|-----------|--------|
| `email` | Email input | user@email.com |
| `first_name` | Text input | Free text |
| `mobile` | Phone input | E.164 format (+1XXXXXXXXXX) |

---

### Layer 8 — Conversion Event (Universal)
**Source:** brand-config.json + Cal.com API response  
**Save in Results:** YES  

| Parameter | Source | Values |
|-----------|--------|--------|
| `conversion_type` | brand-config.json | booking \| call \| sale \| lead \| app_install \| trial \| download |
| `conversion_status` | Set after event | pending \| confirmed \| cancelled \| no_show |
| `conversion_value` | brand-config.json | Dollar amount |
| `conversion_platform` | brand-config.json | cal.com \| stripe \| shopify \| typeform \| custom |
| `booking_id` | Cal.com API | Booking reference ID |
| `booking_date` | Cal.com API | YYYY-MM-DD |
| `booking_time` | Cal.com API | HH:MM |
| `booking_timezone` | Cal.com API | e.g. America/New_York |

---

### Layer 9 — Behavioral Signals
**Source:** Set Variable blocks throughout the TypeBot flow  
**Save in Results:** YES  

| Parameter | Set When | Logic |
|-----------|----------|-------|
| `funnel_step` | At each major step | step_1 → step_2 → step_3 |
| `steps_completed` | After each question answered | Increment counter |
| `quiz_completion_time` | First block of flow | `new Date().toISOString()` |
| `drop_off_point` | Start of each question group | String label of current question |
| `post_booking_priority` | Post-conversion choice block | Values from brand-config |

---

### Layer 10 — Predictive Intelligence (Computed)
**Source:** Set Variable blocks with custom code  
**Save in Results:** YES  

| Parameter | Computed From | Logic Summary |
|-----------|--------------|---------------|
| `aps_score` | eps + behavioral modifiers | See [Computed Variable Logic](#7-computed-variable-logic) |
| `lead_quality_score` | Weighted signal formula | See [Computed Variable Logic](#7-computed-variable-logic) |
| `brand_profile_summary` | Brand slots + framework vars | Constructed string |
| `qualified` | 
| `disqualified_reason` | If qualified = false
| `motivation_type` | Signal cascade | pain \| desire |
| `awareness_stage` | ag + cta + quiz | Schwartz level |
| `belief_barrier` | pain_obstacle + identity_type | Constructed string |

---

## 4. TypeBot Setup: Step-by-Step

### Step 1: Declare All Variables

In TypeBot editor:
1. Click the **@** Variables button (top right)
2. For each variable below: click **+**, type exact name, press Enter
3. After declaring all: enable **Save in results** for every variable except `ip`

**Copy this list — paste one at a time:**

```
# Layer 1 — AdKernel Core
conversion
campaign
banner
publisher
offer
goal_id

# Layer 2 — AdKernel Personalization
city
country_name
region
State_Name
device_type
os
device_brand
carrier
day_of_week
date
ip
pubzone
bid

# Layer 3 — Avalanche Tokens
cta
at
ag
ad
phase
eps
av
mb
hl
sh

# Layer 4 — Framework Psychology
market_sophistication
awareness_stage
pain_experience
pain_obstacle
pain_primary
desire_primary
desire_values
motivation_type
identity_type
commitment_depth
cognitive_engagement_depth
verification_type
belief_barrier

# Layer 5 — Demographics
demo_age
demo_income
demo_gender

# Layer 6 — Brand Slots
brand_q1
brand_q2
brand_q3
brand_q4
brand_q5

# Layer 7 — Lead Capture
email
first_name
mobile

# Layer 8 — Conversion Event
conversion_type
conversion_status
conversion_value
conversion_platform
booking_id
booking_date
booking_time
booking_timezone

# Layer 9 — Behavioral Signals
funnel_step
steps_completed
quiz_completion_time
drop_off_point
post_booking_priority

# Layer 10 — Predictive Intelligence
aps_score
lead_quality_score
brand_profile_summary
qualified
disqualified_reason
```

**Total: 63 variables**

### Step 2: Auto-Injection Verification

TypeBot automatically injects URL query parameters into matching declared variables. To verify:

1. Publish a test version of the TypeBot
2. Open the URL with test params appended:
```
https://your-typebot-url.typebot.io/your-bot-name
  ?conversion=TEST123
  &campaign=999
  &banner=TESTBANNER
  &cta=Test-CTA
  &at=2&ag=1&eps=20
  &city=Miami&device_type=mobile
```
3. Complete one question, then check TypeBot Results
4. Confirm `conversion`, `campaign`, `city`, `cta`, `eps` all populated correctly

### Step 3: Redirect URL Configuration

If using embedded TypeBot (not redirect), add prefilledVariables to pass cookie values:

```javascript
Typebot.initStandard({
  typebot: "your-typebot-id",
  prefilledVariables: {
    "conversion": getCookie('conversion'),
    "campaign": getCookie('campaign'),
    "banner": getCookie('banner'),
    "publisher": getCookie('publisher'),
    "offer": getCookie('offer'),
    "goal_id": getCookie('goal_id'),
    "cta": getCookie('cta'),
    "at": getCookie('at'),
    "ag": getCookie('ag'),
    "ad": getCookie('ad'),
    "phase": getCookie('phase'),
    "eps": getCookie('eps'),
    "av": getCookie('av'),
    "mb": getCookie('mb'),
    "hl": getCookie('hl'),
    "city": getCookie('city'),
    "device_type": getCookie('device_type'),
    "device_brand": getCookie('device_brand'),
    "market_sophistication": getCookie('market_sophistication'),
  }
});
```

---

## 5. How Parameters Flow Through the System

```
AD CLICK (AdKernel fires)
  │
  ├─ URL parameters: conversion, campaign, banner, publisher, offer,
  ├─ URL parameters: city, device_type, device_brand, os, carrier, day_of_week, date, ip, pubzone, bid
  ├─ URL parameters: cta, at, ag, ad, phase, eps, av, mb, hl, sh
  │
  ▼
LANDING PAGE (index.html)
  │
  ├─ Reads ALL URL params
  ├─ Sets cookies: 365-day expiry, all param names as cookie names
  ├─ Seeds: market_sophistication from brand-config
  │
  ▼
TYPEBOT (echo-funnel)
  │
  ├─ Auto-injects URL params → matching declared variables
  ├─ Quiz captures: brand_q1-q5, pain_experience, pain_obstacle, desire_primary,
  │                 desire_values, identity_type, demo_age, demo_income, verification_type
  ├─ Lead captures: email, first_name, mobile
  ├─ Computes: motivation_type, qualified, aps_score, lead_quality_score,
  │            brand_profile_summary, belief_barrier, steps_completed, drop_off_point
  ├─ Gates: qualified=false → redirect to register page
  │
  ▼
CONVERSION TRACKER (conversion-tracker.html)
  │
  ├─ Receives all params in URL query string (see Section 9)
  ├─ GTM fires: lead_conversion event with full dataLayer
  ├─ AdKernel postback: XML + DSP with aps_score
  ├─ Stores: all params in Supabase via n8n webhook
  │
  ▼
CONVERSION EVENT (cal.com / stripe / etc)
  │
  ├─ booking_id, booking_date, booking_time, booking_timezone captured
  ├─ GTM fires: thankyou_conversion event
  ├─ APS set to 100
  ├─ EPS/APS delta calculated and logged with all tracking parameters for compound AI predictive learning
  │
  ▼
DOWNSTREAM SYSTEMS
  │
  ├─ Email: motivation_type + pain_primary + desire_primary + identity_type + first_name
  ├─ SMS: mobile + booking_date + booking_time + booking_timezone + first_name
  ├─ AI Voice: brand_profile_summary + city + first_name + desire_primary
  ├─ Retargeting: motivation_type + awareness_stage + market_sophistication
  └─ Sales CRM: full fingerprint + lead_quality_score + aps_score + belief_barrier
```

---

## 6. brand-config.json New Sections

Add these sections to the existing brand-config.json. Do not remove existing sections.

### market_intelligence
```json
"market_intelligence": {
  "sophistication": 2,
  "sophistication_label": "problem_aware",
  "awareness_stage_default": "problem_aware",
  "sophistication_weights": {
    "ad_signal": 0.40,
    "cta_signal": 0.20,
    "quiz_answers": 0.40
  }
}
```

### conversion_event (replaces booking-specific config)
```json
"conversion_event": {
  "type": "booking",
  "platform": "cal.com",
  "value": 0,
  "qualified_threshold": 80,
  "disqualify_redirect": "https://www.beyondbordersmatchmaking.com/register"
}
```

### framework_variables
```json
"framework_variables": {
  "motivation_type": {
    "pain_signals": ["frustrating", "gave-up-on-", "not-", "-waste-my-time"],
    "desire_signals": ["future-", "life-", "", "-future"],
    "pain_weight": 0.60,
    "desire_weight": 0.40
  },
  "pain_experience": {
    "label": "",
    "input_type": "choice",
    "values": ["", "", "frustrating", "gave-up-on-"]
  },
  "pain_obstacle": {
    "label": "Biggest problem?",
    "input_type": "choice",
    "values": ["not-", "-waste-my-time", "hard-to-find-", "not-"]
  },
  "desire_primary": {
    "label": "What do you want most?",
    "input_type": "choice",
    "values": ["future-", "life-", "serious-", ""]
  },
  "desire_values": {
    "label": "What matters most?",
    "input_type": "multi-select",
    "values": ["", "", "", ""]
  },
  "identity_type": {
    "label": "How would you describe yourself?",
    "input_type": "choice",
    "values": ["ambitious-builder", "family-first", "", ""]
  }
}
```

### brand_slots
```json
"brand_slots": {
  "q1": {
    "label": " x preference",
    "input_type": "picture_choice",
    "values": ["", ""],
    "image_set": "x_preference"
  },
  "q2": {
    "label": "x preference",
    "input_type": "picture_choice",
    "values": ["", ""],
    "image_set": "x_preference"
  },
  "q3": {
    "label": "Preferred x",
    "input_type": "picture_choice",
    "values": ["", "", "", ""],
    "image_set": "x_Prefered"
  },
  "q4": {
    "label": "Preferred x",
    "input_type": "choice",
    "values": ["", "", "", "", ""]
  },
  "q5": {
    "label": "Preferred x",
    "input_type": "multi-select",
    "values": ["", "", "", ""]
  }
}
```

### lead_quality_scoring (updated formula)
```json
"lead_quality_scoring": {
  "weights": {
    "email_verified": 25,
    "phone_verified": 25,
    "scroll_depth_75": 15,
    "time_on_page_30": 15,
    "archetype_detected": 10,
    "form_fields_filled_3": 10,
    "steps_completed_9": 15,
    "qualified": 20,
    "motivation_type_detected": 10,
    "awareness_stage_detected": 5
  },
  "cap": 100,
  "routing": {
    "hot": 80,
    "warm": 50,
    "cold": 0
  },
  "ai_learning": true,
  "ai_learning_target": "conversion_confirmed",
  "ai_learning_cycle": "weekly",
  "model_confidence_threshold": 100
}
```

---

## 7. Computed Variable Logic

### motivation_type
```javascript
// Set Variable block — Execute on client: NO
// Trigger: After pain_obstacle is captured

const painSignals = ['','','',''];
const desireSignals = ['','','',''];

const painHits = [{{pain_experience}}, {{pain_obstacle}}]
  .filter(v => painSignals.includes(v)).length;

const desireHits = [{{desire_primary}}, {{desire_values}}]
  .filter(v => desireSignals.some(s => v && v.includes(s))).length;

return painHits >= desireHits ? 'pain' : 'desire';
```

### qualified
```javascript
// Set Variable block
// Trigger: After X

return {{qualified}} !== 'true';
```

### brand_profile_summary
```javascript
// Set Variable block
// Trigger: After all brand slots and framework variables captured

return 'Ideal partner: ' + {{brand_q1}} + ', ' + {{brand_q3}} + '.' +
  ' Personality: ' + {{brand_q5}} + '.' +
  ' Goal: ' + {{desire_primary}} + '.' +
  ' Pain: ' + {{pain_obstacle}} + '.' +
  ' Identity: ' + {{identity_type}} + '.';
```

### lead_quality_score
```javascript
// Set Variable block
// Trigger: After email and mobile are captured

let score = 0;
if ({{email}} && {{email}}.includes('@')) score += 25;
if ({{mobile}} && {{mobile}}.length >= 10) score += 25;
if (parseInt({{steps_completed}}) >= 9) score += 15;
if ({{demo_income}} && {{demo_income}} !== 'under-100k') score += 20;
if ({{motivation_type}}) score += 10;
if ({{awareness_stage}}) score += 5;
return Math.min(score, 100);
```

### aps_score
```javascript
// Set Variable block
// Trigger: Final block before redirect

let aps = parseInt({{eps}}) || 50;
if ({{email}}) aps += 15;
if ({{mobile}}) aps += 15;
if (parseInt({{steps_completed}}) >= 9) aps += 10;
if ({{motivation_type}}) aps += 5;
if ({{demo_income}} !== 'under-100k') aps += 10;
return Math.min(aps, 99);
```

### belief_barrier
```javascript
// Set Variable block
// Trigger: After pain_obstacle and identity_type captured

return 'Barrier: ' + {{pain_obstacle}} + ' | Identity: ' + {{identity_type}};
```

### steps_completed (increment on each answer)
```javascript
// Set Variable block — add after EVERY quiz input block
return (parseInt({{steps_completed}}) || 0) + 1;
```

---

## 8. GTM DataLayer Reference

The following variables must be present in the GTM dataLayer push on conversion-tracker.html. These extend the existing dataLayer structure — do not remove existing variables.

```javascript
window.dataLayer.push({
  event: 'lead_conversion',

  // Existing AdKernel Core (unchanged)
  conversion: '{{URL param: conversion}}',
  campaign: '{{URL param: campaign}}',
  banner: '{{URL param: banner}}',
  publisher: '{{URL param: publisher}}',
  goal_id: '{{URL param: goal_id}}',

  // Existing Avalanche tokens (unchanged)
  at: '{{URL param: at}}',
  ag: '{{URL param: ag}}',
  ad: '{{URL param: ad}}',
  phase: '{{URL param: phase}}',
  eps: parseInt('{{URL param: eps}}') || 50,

  // NEW — Framework Psychology
  motivation_type: '{{URL param: motivation_type}}',
  awareness_stage: '{{URL param: awareness_stage}}',
  market_sophistication: parseInt('{{URL param: market_sophistication}}') || 2,
  pain_primary: '{{URL param: pain_primary}}',
  desire_primary: '{{URL param: desire_primary}}',
  identity_type: '{{URL param: identity_type}}',
  belief_barrier: '{{URL param: belief_barrier}}',

  // NEW — Behavioral Signals
  steps_completed: parseInt('{{URL param: commitment_depth}}') || 0,
  quiz_completion_time: '{{URL param: quiz_completion_time}}',
  drop_off_point: '{{URL param: drop_off_point}}',

  // NEW — Predictive Intelligence
  aps_current: parseInt('{{URL param: aps}}') || 50,
  lead_quality_score: parseInt('{{URL param: lead_quality_score}}') || 0,
  qualified: '{{URL param: qualified}}' === 'true',
  brand_profile_summary: '{{URL param: brand_summary}}',

  // NEW — Conversion Event (universal)
  conversion_type: 'booking',

  // NEW — Brand Slots
  brand_q1: '{{URL param: brand_q1}}',
  brand_q2: '{{URL param: brand_q2}}',
  brand_q3: '{{URL param: brand_q3}}',
  brand_q4: '{{URL param: brand_q4}}',
  brand_q5: '{{URL param: brand_q5}}',

  // Existing Lead (unchanged)
  first_name: '{{URL param: name}}',
  email: '{{URL param: email}}',
  phone: '{{URL param: mobile}}',

  // Existing AdKernel Personalization (unchanged)
  city: '{{URL param: city}}',
  device_type: '{{URL param: device_type}}',
  device_brand: '{{URL param: device_brand}}',

  // Existing Funnel Step (unchanged)
  funnel_step: 'step_2',
  dsp_step: 'step_2',
});
```

---

## 9. Conversion Tracker Redirect URL Structure

The TypeBot redirect block must build this URL. All parameters are required. Concatenate into a single string with no line breaks.

```
/conversion-tracker.html
  ?conversion={{conversion}}
  &campaign={{campaign}}
  &banner={{banner}}
  &publisher={{publisher}}
  &offer={{offer}}
  &goal_id={{goal_id}}
  &at={{at}}&ag={{ag}}&ad={{ad}}&phase={{phase}}
  &eps={{eps}}&aps={{aps_score}}
  &av={{av}}&mb={{mb}}&hl={{hl}}
  &cta={{cta}}
  &name={{first_name}}&email={{email}}&mobile={{mobile}}
  &demo_age={{demo_age}}&demo_income={{demo_income}}
  &brand_q1={{brand_q1}}&brand_q2={{brand_q2}}&brand_q3={{brand_q3}}
  &brand_q4={{brand_q4}}&brand_q5={{brand_q5}}
  &pain_primary={{pain_obstacle}}&desire_primary={{desire_primary}}
  &pain_experience={{pain_experience}}&desire_values={{desire_values}}
  &motivation_type={{motivation_type}}&identity_type={{identity_type}}
  &awareness_stage={{awareness_stage}}&market_sophistication={{market_sophistication}}
  &lead_quality_score={{lead_quality_score}}&commitment_depth={{steps_completed}}
  &quiz_completion_time={{quiz_completion_time}}&drop_off_point={{drop_off_point}}
  &brand_summary={{brand_profile_summary}}&belief_barrier={{belief_barrier}}
  &qualified={{qualified}}&disqualified_reason={{disqualified_reason}}
  &city={{city}}&device_type={{device_type}}&device_brand={{device_brand}}
  &os={{os}}&carrier={{carrier}}&day_of_week={{day_of_week}}
  &conversion_type={{conversion_type}}
```

---

## 10. Validation Checklist

Run this checklist before publishing TypeBot and before launching any campaign.

### TypeBot Variable Declaration
- [ ] All 63 variables declared in Variables panel
- [ ] Variable names match exactly (case-sensitive)
- [ ] Save in results: ON for all
- [ ] No duplicate variable declarations

### Auto-Injection Test
- [ ] Open TypeBot URL with test params (see Section 4 Step 2)
- [ ] `conversion` value appears in TypeBot Results after test completion
- [ ] `city` value appears correctly
- [ ] `eps` value appears as number (not string)
- [ ] `cta` value matches the param passed

### Computed Variables Test
- [ ] `motivation_type` returns `pain` or `desire` (not null/undefined)
- [ ] `qualified` returns `true` or `false`
- [ ] `brand_profile_summary` contains no `undefined` tokens
- [ ] `aps_score` is between 21 and 99 for a test user
- [ ] `lead_quality_score` is between 0 and 100

### Routing Test
- [ ] disqualified = Y → redirect to disqualified page ✓
- [ ] qualified = Y → redirect to conversion-tracker.html ✓

### Conversion Tracker URL Test
- [ ] All params present in CT redirect URL
- [ ] `conversion` param present (not `conversion_id`)
- [ ] `aps` param has numeric value
- [ ] `qualified` param shows `true`

### GTM Test
- [ ] GTM Preview mode shows `lead_conversion` event on CT page load
- [ ] dataLayer contains `motivation_type` with value `pain` or `desire`
- [ ] dataLayer contains `aps_current` with numeric value
- [ ] AdKernel XML postback fires (check Network tab for xml.amplifai.it.com)
- [ ] AdKernel DSP postback fires (check Network tab for rtb2-useast.amplifai.it.com)

---

*AmplifAI Acquisition OS — Typebot Universal Intelligence Schema — v1.0*  
*Parameter Reference & Setup Guide*
