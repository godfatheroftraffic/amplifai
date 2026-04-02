# COMPLETE PARAMETER MASTER REFERENCE - v2.0

## THE COMPETITIVE ADVANTAGE

This document defines ALL 350+ parameters that power AmplifAI's predictive intelligence system:
- **EPS (Estimated Predictive Score)**: AI predicts conversion probability at ad click using 200+ data points
- **APS (Actual Predictive Score)**: Updates in real-time based on actual user behavior  
- **Learning Loop**: EPS → APS delta trains the AI to improve predictions over time

**Every parameter feeds the intelligence system. No shortcuts. This is the source of truth.**

---

## TOTAL PARAMETER COUNT: 350+

### Breakdown by Category:
1. AdKernel Core: 6 parameters
2. AdKernel Native: 38 parameters
3. Keitaro Routing: 13 parameters
4. Creative DNA - Static Ads (Meta): 21 parameters
5. Creative DNA - Video Ads (YouTube): 22 parameters
6. Echo Landing Page Personalization: 27 parameters
7. AdKernel Dynamic Personalization Macros: 10 macros
8. Keitaro Dynamic Placeholders: 8 placeholders
9. Funnel Journey & Behavior Tracking: 14 parameters
10. Avalanche Fixed Tokens: 8 parameters
11. Avalanche Creative (AVID): 13 parameters
12. Avalanche Behavioral + Intent: 7 parameters
13. Avalanche Segmentation + Context: 8 parameters
14. Avalanche Emotional/Psychological: 12 parameters
15. Avalanche Conversion/Offer Logic: 9 parameters
16. Avalanche Behavior Prediction: 10 parameters
17. Avalanche Narrative/Story: 6 parameters
18. Avalanche UX/Layout: 5 parameters
19. Avalanche System Evolution: 4 parameters
20. Avalanche Compliance: 4 parameters
21. Avalanche Signal Intelligence: 4 parameters
22. Avalanche Spiritual/Ethical: 5 parameters
23. Avalanche Retargeting/Virality: 4 parameters
24. Avalanche Creative Reuse: 6 parameters
25. Avalanche Advanced Conversion: 8 parameters
26. User Identity (PII): 8 parameters
27. System Conversion Events: 6 parameters

---

## CRITICAL NAMING RULES

### ❌ WRONG (Never Use These!)

AdKernel does NOT use `_id` suffixes:

| ❌ WRONG | ✅ CORRECT | Macro |
|---------|-----------|-------|
| `conversion_id` | `conversion` | `{conversion}` |
| `campaign_id` | `campaign` | `{campaign}` |
| `banner_id` | `banner` | `{banner}` |
| `publisher_id` | `publisher` | `{publisher}` |
| `offer_id` | `offer` | `{offer}` |

### ⚠️ Capitalization Matters!

| ❌ Wrong | ✅ Correct | Why |
|---------|-----------|-----|
| `keyword` | `Keyword` | AdKernel uses capital K |
| `query` | `Query` | AdKernel uses capital Q |
| `state_name` | `State_Name` | AdKernel uses capital S & N |

**Official Reference:** https://media.amplifai.it.com/help-center/using-macros-in-direct-advertising-campaigns/

---

## CATEGORY 1: AdKernel Core Tracking (6 parameters)

**Purpose:** Core conversion tracking identifiers from AdKernel DSP.

**Source:** https://media.amplifai.it.com/help-center/using-macros-in-direct-advertising-campaigns/

| Parameter | Macro | Type | Description | AI/Human Use |
|-----------|-------|------|-------------|--------------|
| `conversion` | `{conversion}` | String | Unique click/conversion ID - THE primary tracking identifier | Use for deduplication, attribution, postback matching. CRITICAL for EPS→APS tracking. |
| `campaign` | `{campaign}` | String | Campaign identifier from DSP | Analyze performance by campaign, attribute conversions, optimize spend allocation. |
| `banner` | `{banner}` | String | Creative/banner identifier | Track which ad creative drove click/conversion. A/B test creatives, auto-scale winners. |
| `goal_id` | `{goal_id}` | String | Conversion goal ID (e.g., lead, sale, signup) | Different goals = different value. Route to appropriate funnel, calculate ROI. |
| `offer` | `{offer}` | String | Offer identifier | Track which offer/product attracted user. Optimize offer mix, personalize landing page. |
| `publisher` | `{publisher}` | String | Traffic source/publisher ID | Quality varies by source. Blacklist bad sources, scale good ones, adjust bids. |

**CRITICAL:** Store using primary names (`conversion` NOT `conversion_id`). Accept aliases for compatibility but store as official names.

**Reading Strategy:**
```javascript
// Try primary name first, then aliases
conversion: getParam('conversion', ['trck', 'click_id'])
campaign: getParam('campaign', ['campaign_id'])
banner: getParam('banner', ['creative_id', 'banner_id'])
publisher: getParam('publisher', ['publisher_id'])
```

---

## CATEGORY 2: AdKernel Native Parameters (38 parameters)

**Purpose:** Rich contextual data from AdKernel for audience segmentation, personalization, and EPS prediction.

**Critical for EPS:** Device, geo, time data feeds AI prediction at click-time.

| Parameter | Macro | Type | Description | EPS Impact | Personalization Use |
|-----------|-------|------|-------------|-----------|---------------------|
| `pubzone` | `{pubzone}` | String | Publisher zone/placement | Different zones = different intent | Route messaging by placement quality |
| `country_name` | `{country_name}` | String | Full country name (e.g., "United States") | Geo = conversion predictor | Personalize copy: "Join 10,000 {country_name} users" |
| `region` | `{region}` | String | State/province | Regional performance varies | Legal compliance, regional offers |
| `city` | `{city}` | String | City name | Hyper-local targeting signal | "Transform your {city} business" |
| `device_type` | `{device_type}` | String | mobile / desktop / tablet | Mobile converts differently | Mobile = larger CTA, simpler forms |
| `os` | `{os}` | String | Operating system (iOS, Android, Windows, etc.) | iOS > Android LTV typically | "Download for {os}" |
| `browser` | `{browser}` | String | Browser name (Chrome, Safari, etc.) | Browser = user sophistication signal | Compatibility notices |
| `Keyword` | `{Keyword}` | String | Search keyword (⚠️ capital K!) | Intent signal from search terms | Match landing page to keyword |
| `bid` | `{bid}` | Number | Bid amount in dollars | Higher bid = higher value traffic (usually) | Cost tracking, ROI calculation |
| `date` | `{date}` | String | Click date | Seasonal patterns, day-of-week performance | Time-based offers |
| `day_of_month` | `{day_of_month}` | Number | Day (1-31) | Paycheck cycles, month-end urgency | "Month-end sale ends {day_of_month}" |
| `day_of_week` | `{day_of_week}` | String | Day name (Monday-Sunday) | Weekday vs weekend behavior differs | "Happy {day_of_week}! Special offer" |
| `device_brand` | `{device_brand}` | String | Device manufacturer (Apple, Samsung, etc.) | Premium brands = higher LTV | Segment by affluence |
| `device_model` | `{device_model}` | String | Specific device model | Screen size, capabilities | Responsive optimization |
| `request_id` | `{request_id}` | String | Unique request identifier | Technical debugging | Server-side tracking |
| `month` | `{month}` | String | Month name | Seasonal campaigns | "{month} Special Pricing" |
| `original_subid` | `{original_subid}` | String | Original sub ID before routing | Multi-hop attribution | Full attribution chain |
| `os_type` | `{os_type}` | String | OS category | Mobile vs desktop OS patterns | Platform-specific flows |
| `postback_id` | `{postback_id}` | String | Postback identifier | Server-to-server tracking | Postback matching |
| `app_bundle` | `{app_bundle}` | String | App bundle ID (mobile in-app) | In-app vs web traffic quality | In-app specific flows |
| `app_id` | `{app_id}` | String | Application ID | App traffic attribution | App-specific offers |
| `pubfeed` | `{pubfeed}` | String | Publisher feed identifier | Feed quality varies | Optimize by feed |
| `subid` | `{subid}` | String | Sub ID for routing | Granular source tracking | Multi-variate attribution |
| `payout` | `{payout}` | Number | Payout amount | Revenue per conversion | ROI calculation |
| `pubpoint` | `{pubpoint}` | String | Publisher point/placement | Micro-placement optimization | A/B test placements |
| `Query` | `{Query}` | String | Search query (⚠️ capital Q!) | User intent from search | Match LP copy to query |
| `site_id` | `{site_id}` | String | Site identifier | Site quality varies wildly | Blacklist/whitelist sites |
| `referrer_domain` | `{referrer_domain}` | String | Referring domain | Traffic source quality | Attribution |
| `remfeed` | `{remfeed}` | String | Remarketing feed | Retargeting signal | Warm vs cold messaging |
| `ga` | `{ga}` | String | Google Analytics ID | Cross-platform tracking | GA integration |
| `search_referrer_domain` | `{search_referrer_domain}` | String | Search referrer | Search engine source | SEO attribution |
| `search_ip` | `{search_ip}` | String | Search IP address | Bot detection, geo verification | Fraud prevention |
| `source_subid` | `{source_subid}` | String | Source sub ID | Multi-layer attribution | Campaign hierarchy |
| `State_Name` | `{State_Name}` | String | Full state name (⚠️ capitals!) | Legal disclaimers by state | "Licensed in {State_Name}" |
| `source` | `{source}` | String | Traffic source type | Organic vs paid patterns | Source-specific LP |
| `ip` | `{ip}` | String | IP address | Geo lookup, fraud detection | Bot filtering |
| `carrier` | `{carrier}` | String | Mobile carrier | Carrier = demographic proxy | Carrier-specific offers |
| `zip` | `{zip}` | String | ZIP/postal code | Hyper-local targeting | "Serving {zip} area" |
| `state` | `{state}` | String | State code (CA, NY, etc.) | State-level compliance | State offers |
| `country` | `{country}` | String | Country code (US, CA, UK, etc.) | International routing | Country-specific funnels |

**EPS Prediction Use:**
- `device_type + os + device_brand` = User affluence/sophistication score
- `city + region + country` = Geo conversion patterns
- `day_of_week + month` = Temporal patterns
- `publisher + pubzone + site_id` = Traffic quality score

---

## CATEGORY 3: Keitaro Routing (13 parameters)

**Purpose:** Traffic routing and sub ID tracking through Keitaro tracker.

**Source:** https://docs.keitaro.io/en/landing-pages-and-offers/placeholders.html

| Parameter | Placeholder | Type | Description | Routing Use |
|-----------|-------------|------|-------------|-------------|
| `subid` | `{subid}` | String | Main sub ID | Primary Keitaro routing identifier |
| `sub1` (or `sub_id_1`) | `{sub_id_1}` | String | Sub ID 1 | Campaign level tracking |
| `sub2` (or `sub_id_2`) | `{sub_id_2}` | String | Sub ID 2 | Ad group tracking |
| `sub3` (or `sub_id_3`) | `{sub_id_3}` | String | Sub ID 3 | Creative tracking |
| `sub4` (or `sub_id_4`) | `{sub_id_4}` | String | Sub ID 4 | Audience segment |
| `sub5` (or `sub_id_5`) | `{sub_id_5}` | String | Sub ID 5 | Landing page variant |
| `sub6` (or `sub_id_6`) | `{sub_id_6}` | String | Sub ID 6 | Offer variant |
| `sub7` (or `sub_id_7`) | `{sub_id_7}` | String | Sub ID 7 | Custom tracking 1 |
| `sub8` (or `sub_id_8`) | `{sub_id_8}` | String | Sub ID 8 | Custom tracking 2 |
| `sub9` (or `sub_id_9`) | `{sub_id_9}` | String | Sub ID 9 | Custom tracking 3 |
| `sub10` (or `sub_id_10`) | `{sub_id_10}` | String | Sub ID 10 | Custom tracking 4 |
| `_lp` | `{_lp}` | String | Landing page ID in Keitaro | Which LP variant user saw |
| `_offer_id` | `{_offer_id}` | String | Offer ID in Keitaro | Which offer was presented |

**Note:** Accept both formats (`sub1` and `sub_id_1`) for compatibility.

---

[File continues with all remaining categories...]


## CATEGORY 4: Creative DNA - Static Ads (Meta/Facebook) (21 parameters)

**Purpose:** Granular tracking of every component in static ad creatives for performance analysis and AI optimization.

**Source:** Meta_Static_Ad_Component_Variations_For__TPH_-_TrackingParameters.csv

| Parameter | Code | Type | Description | Options/Examples | AI Optimization Strategy |
|-----------|------|------|-------------|------------------|--------------------------|
| `ad_variation` | `av` | String | Unique ad variation ID | variation1, v2_optimizer, split_test_3a | Track winners, auto-pause losers, scale top performers |
| `media_buyer` | `mb` | String | Media buyer identifier | john_doe, maria_garcia, ai_optimizer | Performance by buyer, training data, skill assessment |
| `interruptor_image` | `ii` | String | Scroll-stopping image type | boldstatement, shocking, pattern_interrupt, face_reaction | Test what stops scroll in feed - bold wins cold traffic |
| `image_hero` | `ih` | String | Main image focal point | product, person, result, lifestyle, before_after | Product = feature, result = benefit, person = relatability |
| `image_callouts` | `ic` | String | Text overlays on image | problem_callout, benefit_highlight, urgency_timer | Pain callouts for cold, benefits for warm |
| `irresistible_offer` | `io` | String | Offer type presented | free_trial, discount_20, bonus_stack, guarantee | Free > discount > bonus for cold awareness stage |
| `body_copy` | `bc` | String | Ad copy structure | problem_solution, story_testimonial, question_answer, data_driven | Match to archetype: data for optimizers, story for explorers |
| `cta_type` | `ct` | String | Call-to-action style | learn_more, shop_now, sign_up, get_offer, book_call | Soft CTA (learn) for cold, hard CTA (buy) for hot |
| `image_narrative` | `in` | String | Story in image | before_after, struggle_breakthrough, celebration, transformation | Transformation stories sell, before/after builds belief |
| `solution_emphasis` | `se` | String | How solution highlighted | tested_proven, easy_simple, fast_quick, guaranteed | Tested = credibility, easy = low barrier, fast = urgency |
| `visual_element` | `ve` | String | Visual style/treatment | clean_minimal, busy_attention, bold_contrast, subtle_premium | Busy stops scroll, clean signals premium |
| `unquestionable_proof` | `up` | String | Credibility element | testimonial, data_stats, celebrity, certification, case_study | Data for optimizers, testimonials for social proof seekers |
| `problem_statement` | `ps` | String | Pain point addressed | struggling_with_x, frustrated_by_y, tired_of_z | Specific > generic, visceral > intellectual, relatable > abstract |
| `curiosity_angle` | `ca` | String | Curiosity mechanism | mystery_reveal, secret_exposed, contrarian_truth, forbidden_knowledge | Mystery = intrigue, contrarian = pattern interrupt |
| `wow_factor` | `wf` | String | Surprise/delight element | unexpected_twist, shocking_stat, bold_claim, unique_mechanism | Stops scroll, creates shares, builds memorability |
| `text_overlays` | `to` | String | Overlay text style | bold_callout, subtle_caption, highlighted_benefit, arrow_pointer | Bold for attention, subtle for premium feel |
| `social_proof` | `sp` | String | Social validation type | customer_count, testimonial_quote, ugc_photo, influencer_endorsement | Numbers for scale, faces for relatability |
| `headline` | `hl` | String | Primary headline approach | problem_solution, benefit_driven, question_hook, stat_data | Problem for awareness, benefit for consideration |
| `audience_targeting` | `at` | String | Target audience segment | warm_engaged, cold_lookalike, hot_retarget, abandoned_cart | Match creative temperature to audience temperature |
| `tracking_url` | `tu` | String | UTM/tracking params | utm_campaign=fb_test_3 | Attribution, variant tracking, performance analysis |
| `phase` | `phase` | String | Campaign phase | awareness, consideration, conversion | Awareness = educate, consideration = compare, conversion = NOW |

**Performance Pattern Library:**

```javascript
// COLD TRAFFIC - Awareness Stage (Optimizer Archetype)
{
  av: 'cold_optimizer_v2',
  ii: 'data_visualization',        // Charts/graphs stop scroll
  ih: 'result_metrics',              // Show the outcome
  bc: 'problem_data_solution',       // Logic-based copy
  up: 'case_study_stats',           // Proof through numbers
  cta_type: 'learn_more',           // Soft CTA
  at: 'cold_lookalike',
  phase: 'awareness'
}

// WARM TRAFFIC - Consideration Stage (All Archetypes)
{
  av: 'warm_retarget_v1',
  ii: 'boldstatement',              // Direct message
  io: 'bonus_stack',                // Added value
  bc: 'benefit_testimonial',        // Social proof + benefit
  up: 'testimonial',
  cta_type: 'get_offer',            // Moderate CTA
  at: 'warm_engaged',
  phase: 'consideration'
}

// HOT TRAFFIC - Conversion Stage (Abandoned Cart)
{
  av: 'hot_abandon_v1',
  ii: 'urgency_timer',              // Scarcity/urgency
  io: 'limited_discount',           // Price incentive
  bc: 'urgency_scarcity',           // Time-based copy
  cta_type: 'buy_now',              // Hard CTA
  sp: 'customer_count',             // Final push
  at: 'hot_abandoned_cart',
  phase: 'conversion'
}
```

---

## CATEGORY 5: Creative DNA - Video Ads (YouTube/VSL) (22 parameters)

**Purpose:** Track every component of video ads for performance optimization and AI-driven creative generation.

**Source:** Template__YouTube_Ad_Component_Variations_For__X_-_TrackingParameters.csv

| Parameter | Code | Type | Description | Options/Examples | AI Optimization Strategy |
|-----------|------|------|-------------|------------------|--------------------------|
| `ad_variation` | `av` | String | Video variation ID | vsl_v1, youtube_test_3, short_form_b | Track video performance, iterate on winners |
| `media_buyer` | `mb` | String | Media buyer/creator | john_doe, video_team_a | Performance by creator, skill tracking |
| `skip_stopper` | `ss` | String | First 5-second hook | boldstatement, shocking_visual, question_hook, pattern_interrupt | 5 seconds to stop skip - test aggressively |
| `hook_type` | `ht` | String | Opening hook approach | problem_statement, story_tease, data_stat, contrarian_claim | Match hook to audience awareness level |
| `main_pain_point` | `mpp` | String | Primary pain addressed | financial_stress, time_shortage, health_concern, relationship_struggle | Specific pain = higher engagement |
| `irresistible_offer` | `io` | String | Offer in video | free_trial, discount, bonus_stack, guarantee | Clear offer = higher conversion |
| `cta_type` | `ct` | String | Call-to-action | learn_more, sign_up, buy_now, book_call | Soft for cold, hard for hot |
| `narrative_tone_style` | `nts` | String | Narrative tone | emotional_relatable, logical_analytical, inspirational_uplifting, urgent_direct | Match tone to archetype |
| `voiceover_style` | `vs` | String | Voice characteristics | male_authoritative, female_warm, male_calm, female_energetic | Test voice for target demo |
| `solution_emphasis` | `se` | String | Solution positioning | tested_proven, easy_simple, fast_results, guaranteed_outcome | Benefits over features |
| `visual_element` | `ve` | String | Visual style | fast_cuts, slow_cinematic, talking_head, screen_recording, animation | Match pacing to message |
| `proof_type` | `up` | String | Credibility shown | customer_results, expert_authority, data_research, case_study | Show don't tell |
| `problem_statement` | `ps` | String | Problem articulation | struggling_with_x, frustrated_by_y, failing_at_z | Agitate before solving |
| `curiosity_angle` | `ca` | String | Curiosity driver | mystery_reveal, secret_method, contrarian_truth, insider_knowledge | Hook + hold attention |
| `wow_factor` | `wf` | String | Surprise element | unexpected_twist, shocking_reveal, bold_demonstration | Memorable = shareable |
| `background_music` | `bm` | String | Music style | upbeat_energetic, calm_focused, dramatic_intense, no_music | Music = emotion amplifier |
| `transition_style` | `ts` | String | Edit transitions | quick_cuts, smooth_fades, jump_cuts, slow_motion | Pacing affects retention |
| `graphics_text_usage` | `gtu` | String | On-screen text/graphics | heavy_text, minimal_text, callouts_only, graphics_heavy | Text = accessibility, reinforcement |
| `video_length` | `vl` | String | Video duration | short_15s, medium_60s, long_3min, vsl_30min | Shorter for cold, longer for warm |
| `audience_targeting` | `at` | String | Audience segment | cold_interest, warm_engaged, hot_retarget, lookalike | Match creative to temperature |
| `thumbnail_style` | `ths` | String | Video thumbnail | face_reaction, text_bold, result_visual, mystery | Thumbnail = first impression |
| `call_pattern` | `cp` | String | Storytelling framework | pap_framework, hero_journey, problem_agitate_solve | Proven structures convert |

**Video Performance Patterns:**

```javascript
// SHORT FORM - Cold YouTube Traffic (15-30 seconds)
{
  av: 'youtube_short_v1',
  ss: 'shocking_visual',           // Stop skip immediately
  ht: 'contrarian_claim',          // Pattern interrupt
  vl: 'short_15s',                 // Attention span
  ve: 'fast_cuts',                 // High energy
  bm: 'upbeat_energetic',
  cta_type: 'learn_more',          // Soft ask
  at: 'cold_interest'
}

// VSL - Warm Retargeting (3-10 minutes)
{
  av: 'vsl_warm_v2',
  ht: 'story_tease',               // Build connection
  nts: 'emotional_relatable',      // Personal tone
  vs: 'female_warm',               // Trustworthy voice
  ve: 'talking_head',              // Face-to-camera
  vl: 'long_3min',
  up: 'customer_results',          // Social proof
  cta_type: 'book_call',           // Direct conversion
  at: 'warm_engaged'
}
```

---


## CATEGORY 6: Echo Landing Page Personalization (27 parameters)

**Purpose:** Dynamic landing page customization via URL parameters. Override brand-config.json defaults for A/B testing, personalization, and traffic source bridging.

**All parameters controllable via URL:** `?hl=Custom+Headline&archetype=optimizer&scarcity=3`

| Parameter | Code | Type | Description | Example Values | Human & AI Use Case |
|-----------|------|------|-------------|----------------|---------------------|
| `funnel_intent` | `fi` | String | User's funnel awareness stage | awareness, consideration, decision | **AI:** Awareness = educational copy, decision = hard CTA. **Human:** Route messaging by stage. |
| `headline` | `hl` | String | Page headline text | Transform Your Business Today | **AI:** Personalize by traffic source, A/B test variants. **Human:** Match ad creative (bridge page). |
| `subheadline` | `sh` | String | Supporting headline | Join 10,000+ successful companies | **AI:** Reinforce value prop, add social proof. **Human:** Clarify offer, address objections. |
| `cta_text` | `cta` | String | Button text | Get Started Now, Book My Call, Learn More | **AI:** Test urgency vs specificity. **Human:** Soft CTA for cold, hard for hot traffic. |
| `cta_link` | `link` | String | Button destination URL | https://calendly.com/brand/call | **AI:** Route by segment, A/B test offers. **Human:** Change destination without code changes. |
| `background_image` | `img` | String | Hero image filename (from /public/) | hero-business.jpg, ad-creative-match.png | **AI:** Match ad creative for continuity. **Human:** Seasonal imagery, brand variants. |
| `font` | `font` | String | Font family override | roboto, opensans, arial, inter | **AI:** Test readability by demo. **Human:** Brand consistency, accessibility. |
| `button_color` | `btn_color` | String | CTA background color (hex) | #2563eb, #ff0000, #10b981 | **AI:** Test contrast, urgency colors. **Human:** Red/orange = urgency, blue = trust. |
| `button_text_color` | `btn_text` | String | CTA text color (hex) | #ffffff, #000000 | **AI:** Ensure readability. **Human:** Contrast with button_color. |
| `button_size` | `btn_size` | String | CTA button size | small, medium, large, xlarge | **AI:** Mobile = larger, desktop = medium. **Human:** Prominence testing. |
| `button_style` | `btn_style` | String | Button border style | square, rounded, pill | **AI:** Modern = rounded/pill. **Human:** Brand aesthetic matching. |
| `headline_size` | `hl_size` | String | Headline font size (CSS) | 3rem, 48px, 2.5rem | **AI:** Responsive sizing. **Human:** Mobile smaller, desktop larger. |
| `subheadline_size` | `sh_size` | String | Subheadline size (CSS) | 1.5rem, 24px | **AI:** 50-60% of headline size. **Human:** Visual hierarchy. |
| `headline_color` | `hl_color` | String | Headline color (hex) | #ffffff, #000000, #1f2937 | **AI:** Contrast with background. **Human:** Light bg = dark text, dark bg = light text. |
| `subheadline_color` | `sh_color` | String | Subheadline color (hex) | #ffffff, #666666 | **AI:** Slightly muted vs headline. **Human:** Hierarchy through color. |
| `overlay` | `overlay` | String | Background darkness | light, medium, dark, xdark | **AI:** Ensure text readability. **Human:** Light overlay for bright images, dark for busy. |
| `social_proof` | `social_proof` | String | Show trust badge | on, off | **AI:** Enable for warm traffic. **Human:** Reduce clutter for cold. |
| `social_proof_text` | `social_text` | String | Social proof message | Join 10,000+ customers, Trusted by 500 companies | **AI:** Build trust, create FOMO. **Human:** Update numbers regularly. |
| `scarcity` | `scarcity` | Number | Spots/items remaining | 3, 5, 10, 47 | **AI:** Create urgency. **Human:** Real-time inventory or artificial scarcity. |
| `scarcity_text` | `scarcity_text` | String | Scarcity message | Only {spots} left today!, {spots} spots remaining | **AI:** {spots} replaced with number. **Human:** Test urgency messaging. |
| `progress_bar` | `progress` | String | Show progress indicator | on, off | **AI:** Multi-step funnels. **Human:** Show advancement, reduce abandonment. |
| `micro_commitment` | `micro_yes` | String | Micro-yes element | on, off | **AI:** Pre-frame agreement. **Human:** "Yes, I want this" increases commitment. |
| `micro_yes_text` | `micro_text` | String | Micro-commitment copy | Yes, I'm ready to transform, I want to succeed | **AI:** Positive framing. **Human:** Align with user identity/goals. |
| `archetype` | `archetype` | String | User personality type | optimizer, disruptor, builder, explorer | **AI:** Optimizer = data, disruptor = speed. **Human:** Personalize tone, proof, offer. |
| `angle` | `angle` | String | Marketing message angle | data_driven, risk_averse, speed_focused, cost_savings | **AI:** data_driven = stats, risk_averse = guarantees. **Human:** Primary motivation alignment. |
| `variant` | `variant` | String | Split test variant ID | control, variant_a, variant_b, test_3 | **AI:** Track A/B assignment. **Human:** Consistent experience across sessions. |
| `phase` | `phase` | String | Customer journey stage | awareness, consideration, decision | **AI:** Awareness = educate, decision = convert NOW. **Human:** Match messaging to readiness. |

**Dynamic Personalization Examples:**

```
EXAMPLE 1: Archetype + Angle Personalization
?archetype=optimizer&angle=data_driven&hl=Increase+ROI+by+340%+with+Data&social_text=Join+50,000+data-driven+marketers

EXAMPLE 2: Traffic Source Bridge (Facebook ad continuity)
?img=facebook-ad-creative.jpg&hl=Yes!+I+want+to+scale&cta=Get+My+Custom+Plan&btn_color=#ff0000

EXAMPLE 3: Geo-Personalization (with AdKernel macros)
?hl=Transform+Your+{city}+Business&sh=Join+500+{city}+entrepreneurs&scarcity=3

EXAMPLE 4: Urgency Variant Testing
?scarcity=3&scarcity_text=Only+3+spots+left+in+{city}!&btn_color=#ff0000&overlay=dark&social_proof=on

EXAMPLE 5: Mobile-Optimized
?btn_size=xlarge&hl_size=2rem&sh_size=1.2rem&btn_style=pill
```

---

## CATEGORY 7: AdKernel Dynamic Personalization Macros (10 macros)

**Purpose:** Server-side dynamic content insertion using AdKernel macros in HTML. Personalize copy based on real user data.

**Reference:** https://media.amplifai.it.com/help-center/using-macros-in-direct-advertising-campaigns/#list-of-macros

**Implementation:** Place macros in HTML template, AdKernel replaces with actual values server-side.

| Macro | Parameter | Replaces With | Use Case | Example |
|-------|-----------|---------------|----------|---------|
| `{city}` | `city` | User's city name | Localize headlines, social proof | "Join 500+ **{city}** businesses" → "Join 500+ **San Francisco** businesses" |
| `{region}` | `region` | State/province | Regional offers, compliance | "Available in **{region}**" → "Available in **California**" |
| `{country_name}` | `country_name` | Full country name | International targeting | "Serving **{country_name}** since 2020" → "Serving **United States** since 2020" |
| `{State_Name}` | `State_Name` | Full state name (⚠️ capitals!) | Legal disclaimers | "Licensed in **{State_Name}**" → "Licensed in **California**" |
| `{zip}` | `zip` | ZIP/postal code | Hyper-local targeting | "Serving **{zip}** area" → "Serving **94105** area" |
| `{device_type}` | `device_type` | mobile/desktop/tablet | Device-specific messaging | "**Tap** here" (mobile) vs "**Click** here" (desktop) |
| `{os}` | `os` | Operating system | OS-specific instructions | "Download for **{os}**" → "Download for **iOS**" |
| `{browser}` | `browser` | Browser name | Compatibility notices | "Optimized for **{browser}**" → "Optimized for **Chrome**" |
| `{day_of_week}` | `day_of_week` | Day name | Time-based messaging | "Happy **{day_of_week}**! Limited Monday offer" |
| `{month}` | `month` | Month name | Seasonal campaigns | "**{month}** Special Pricing" → "**February** Special Pricing" |

**HTML Implementation Example:**

```html
<!-- Landing Page HTML Template -->
<h1>Transform Your <span class="city">{city}</span> Business</h1>
<p class="social-proof">Join 500+ successful businesses in <span class="region">{region}</span></p>
<div class="urgency">Only 3 spots left in <span class="city">{city}</span> today!</div>
<button class="cta">{device_type === 'mobile' ? 'Tap' : 'Click'} to Get Started</button>
```

**Rendered for San Francisco user on iPhone:**
```
Transform Your San Francisco Business
Join 500+ successful businesses in California
Only 3 spots left in San Francisco today!
[Tap to Get Started]
```

---

## CATEGORY 8: Keitaro Dynamic Personalization Placeholders (8 placeholders)

**Purpose:** Server-side personalization via Keitaro tracker. Insert in landing page HTML for dynamic content.

**Reference:** https://docs.keitaro.io/en/landing-pages-and-offers/placeholders.html

| Placeholder | Parameter | Replaces With | Use Case |
|-------------|-----------|---------------|----------|
| `{geo.city}` | `city` | City name | Local targeting: "Best service in {geo.city}" |
| `{geo.region}` | `region` | State/region | Regional offers: "Now available in {geo.region}" |
| `{geo.country}` | `country` | Country code | International routing: "Shipping to {geo.country}" |
| `{device}` | `device_type` | Device type | Responsive messaging: "{device} users save 20%" |
| `{os}` | `os` | Operating system | OS-specific CTAs: "Download for {os}" |
| `{browser}` | `browser` | Browser name | Compatibility: "Works perfectly in {browser}" |
| `{language}` | `language` | User language | Multi-language: Load content based on {language} |
| `{ip}` | `ip` | IP address | Compliance logging, fraud detection |

**Combined AdKernel + Keitaro + Echo Example:**

```
Full Personalization URL:
https://lp.brand.com/?hl=Scale+Your+Business+in+{city}&sh=Join+{geo.city}+entrepreneurs&archetype=optimizer&angle=data_driven&scarcity=3&img=ad-creative.jpg

For SF user on iPhone renders as:
Headline: Scale Your Business in San Francisco
Subheadline: Join San Francisco entrepreneurs
Archetype-matched messaging: Data-driven optimization strategies
Urgency: Only 3 spots left in San Francisco
```

---

## CATEGORY 9: Funnel Journey & Behavior Tracking (14 parameters)

**Purpose:** Track user journey through funnel, detect behavioral patterns, enable remarketing and resurrection campaigns. **Critical for APS updates.**

| Parameter | Code | Type | Description | Range | AI/System Use | Human Use |
|-----------|------|------|-------------|-------|---------------|-----------|
| `scroll_depth` | `scroll_depth` | Number | Max scroll percentage | 0-100 | Engagement signal: >75% = +5 APS | High scroll = interested, show exit intent |
| `time_on_page` | `time_on_page` | Number | Seconds on page | 0+ | >30s = +10 APS, <10s = bounce | Long time = processing, nurture needed |
| `return_visitor` | `return_visitor` | Boolean | Previously visited | true/false | true = warm lead, different messaging | Show "Welcome back" message |
| `session_count` | `session_count` | Number | Total visits | 1+ | 1=new, 2-3=warming, 4+=hot or stuck | 3+ visits without conversion = intervention |
| `entry_page` | `entry_page` | String | First page in funnel | /lp/offer-a, /fb-ad-lp | Track entry point, optimize top-of-funnel | A/B test landing pages |
| `funnel_step` | `funnel_step` | String | Current funnel position | step_1, step_2, step_3 | step_1=LP click, step_2=survey, step_3=booking | Progress tracking, abandonment detection |
| `exit_intent_triggered` | `exit_intent_triggered` | Boolean | Exit popup shown | true/false | Resurrection targeting signal | What made them leave? Fix friction. |
| `form_fields_filled` | `form_fields_filled` | Number | Form completion | 0+ | Partial = retarget, simplify form | Which fields cause abandonment? |
| `chat_messages_sent` | `chat_messages_sent` | Number | Chat interactions | 0+ | High engagement = prioritize | Human interest, fast follow-up |
| `lead_quality_score` | `lead_quality_score` | Number | Calculated quality | 0-100 | Route to sales vs nurture | Qualify leads automatically |
| `email_verified` | `email_verified` | Boolean | Email validated | true/false | true = +15 APS, real lead | Safe to email, reduce bounces |
| `phone_verified` | `phone_verified` | Boolean | Phone validated | true/false | true = +15 APS, enables SMS/calls | High intent signal |
| `appointment_confirmed` | `appointment_confirmed` | Boolean | Booking complete | true/false | true = APS set to 100 (main conversion) | Success! Prepare for call. |
| `predicted_show_rate` | `predicted_show_rate` | Number | Attendance likelihood | 0-100 | <60 = send reminders, >85 = VIP treatment | Reduce no-shows proactively |

**Funnel State Machine:**

```
step_1: Landing Page View
  User lands on page, parameters captured
  └─> CTA Click → funnel_step = step_1

step_2: Survey/Form Submit  
  Lead data captured (email, phone, answers)
  └─> Form submitted → funnel_step = step_2

step_3: Booking/Purchase Complete
  Main conversion achieved
  └─> Booking confirmed → funnel_step = step_3, APS = 100
```

**Return Visitor Resurrection Logic:**

```javascript
if (return_visitor === true && session_count >= 3) {
  // Multi-visit without conversion = resurrection needed
  
  if (funnel_step === 'step_2' && appointment_confirmed === false) {
    // Captured lead but didn't book
    message = "Complete your booking - special offer inside"
    offer_stack = "discount_10_percent + extended_guarantee"
    urgency_score = 90
  }
  
  if (funnel_step === 'step_1' && email_verified === false) {
    // Clicked CTA but didn't submit form
    message = "Get your free analysis - 2 minute form"
    cta_text = "Claim My Spot"
    scarcity = 3
  }
}
```

**Lead Quality Scoring Algorithm:**

```javascript
lead_quality_score = 0
+ (email_verified ? 25 : 0)        // Real email
+ (phone_verified ? 25 : 0)        // Real phone
+ (scroll_depth > 75 ? 15 : 0)     // Engaged reading
+ (time_on_page > 30 ? 15 : 0)     // Thoughtful consideration
+ (archetype_detected ? 10 : 0)    // Personality matched
+ (form_fields_filled > 3 ? 10 : 0) // Form engagement

// Route based on score:
if (lead_quality_score >= 80) route_to = "hot_leads_sales"
else if (lead_quality_score >= 50) route_to = "warm_leads_nurture"
else route_to = "cold_leads_education"
```

---


## AVALANCHE INFINITE TOKEN SYSTEM (100+ Parameters)

**The following 17 categories comprise the Avalanche Infinite Token System - AmplifAI's core competitive advantage for predictive marketing intelligence.**

---

## CATEGORY 10: Avalanche Fixed Tokens (8 parameters)

**Purpose:** Core non-negotiable identifiers that anchor every user session.

| Parameter | Type | Description | AI Use | Human Use |
|-----------|------|-------------|--------|-----------|
| `brand_id` | String | Brand identifier | Multi-brand tracking, routing | Separate brand analytics |
| `sku` | String | Product SKU | Product performance, inventory | Which products convert |
| `hook` | String | Primary hook text | Hook testing, mutation | Creative optimization |
| `msg` | String | Core message | Message resonance testing | Messaging A/B tests |
| `click_id` | String | Unique click ID (same as `conversion`) | Deduplication, attribution | Track click-to-conversion |
| `fingerprint_id` | String | User fingerprint hash | Anonymous user identity | Cross-device tracking |
| `checkout_url` | String | Checkout destination | Conversion routing | Dynamic checkout pages |
| `sku_price` | Number | Product price | Price testing, elasticity | Revenue tracking |

---

## CATEGORY 11: Avalanche Creative Tokens (AVID Format) (13 parameters)

**Purpose:** Ad creative component tracking for granular performance analysis.

| Parameter | Type | Description | Values | Optimization |
|-----------|------|-------------|--------|--------------|
| `a` | String | Audience segment | warm_abandoned, cold_lookalike | Match creative to temperature |
| `v` | String | Variation ID | v2, test_3a | Version control |
| `i` | String | Image/creative ID | img_hero_01, creative_b | Visual performance |
| `d` | String | Device target | mobile, desktop | Device optimization |
| `a2` | String | Secondary audience | lookalike_converters | Layered targeting |
| `hl` | String | Headline | Transform Your Business | Copy testing |
| `bc` | String | Body copy structure | problem_solution, story | Narrative testing |
| `cta` | String | Call-to-action | Get Started Now | CTA optimization |
| `img` | String | Image filename | hero-bg.jpg | Asset performance |
| `vid` | String | Video filename | explainer_v2.mp4 | Video testing |
| `tone` | String | Voice tone | authoritative, friendly | Tone matching |
| `voice` | String | Voice style | male_calm, female_energetic | Voice testing |
| `asset_type` | String | Asset category | image, video, cta, headline | Component analysis |

---

## CATEGORY 12: Avalanche Behavioral + Intent (7 parameters)

| Parameter | Type | Description | Range | AI Decision Logic |
|-----------|------|-------------|-------|-------------------|
| `intent_lvl` | String | Funnel stage | awareness, consideration, buying, rebuy | Awareness=educate, buying=convert |
| `urgency_score` | Number | Purchase urgency | 1-100 | >80 = hard CTA, <40 = nurture |
| `rltv` | Number | Relative lifetime value | 1-100 | >70 = premium offers |
| `seen_min` | Number | Minutes since last seen | 0+ | <60 = hot retarget |
| `seen_day` | String | Days since first seen | day0, day1, day7, day30 | day0 = new, day7+ = resurrection |
| `sku_clicks` | Number | Product interaction count | 0+ | >3 without purchase = objection |
| `visits` | Number | Session count | 1+ | >4 = stuck, needs intervention |

---

## CATEGORY 13: Avalanche Segmentation + Context (8 parameters)

| Parameter | Type | Description | Values | Routing Logic |
|-----------|------|-------------|--------|---------------|
| `paud` | String | Predictive audience | hot_buyer, warm_engaged, cold_curious | Match creative temperature |
| `taud` | String | Target audience | entrepreneurs_25_45 | Demo-specific messaging |
| `baud` | String | Behavior audience | abandoned_cart, survey_complete | Behavior-triggered flows |
| `paud_trajectory` | String | Audience evolution | cold→warm→hot | Track warming journey |
| `channel` | String | Traffic channel | push, email, sms, voice, social | Channel-specific content |
| `channel_pref` | String | Preferred channel | email, sms | Route to preferred channel |
| `geo` | String | Geographic location | US_CA_SF, UK_LON | Geo-specific offers |
| `devtype` | String | Device type | mobile, desktop, tablet | Device-optimized UX |

---

## CATEGORY 14: Avalanche Emotional/Psychological (12 parameters)

| Parameter | Type | Description | Values | Personalization Strategy |
|-----------|------|-------------|--------|--------------------------|
| `emotion` | String | Dominant emotion | fear, hope, anger, curiosity | Match copy to emotion |
| `trigger_type` | String | Persuasion trigger | scarcity, authority, social_proof | Activate appropriate trigger |
| `objection_class` | String | Primary objection | price, time, trust, need | Address specific objection |
| `storyline_id` | String | Narrative thread | hero_journey, transformation | Story arc alignment |
| `belief_pattern` | String | Core belief system | growth_mindset, fixed_mindset | Message framing |
| `self_view` | String | Self-perception | optimizer, disruptor, builder | Identity-based messaging |
| `psychbelief` | String | Psychological belief | deserve_success, fear_failure | Deep motivation |
| `archetype_signature_token` | String | Deep archetype DNA | optimizer_data_driven_cautious | Multi-dimensional personality |
| `mirror_moment_event` | String | Identity reflection | breakthrough_realization | Transformation trigger |
| `attention_root_token` | String | Core attention driver | problem_pain, solution_benefit | Hook selection |
| `shame_trigger` | String | Shame activation | not_good_enough, falling_behind | Pain point selection |
| `status_reversal` | String | Status change desire | rise_from_struggle | Aspiration messaging |

---

## CATEGORY 15: Avalanche Conversion/Offer Logic (9 parameters)

| Parameter | Type | Description | Values | Offer Construction |
|-----------|------|-------------|--------|---------------------|
| `proof_level` | String | Social proof intensity | testimonial, case_study, data | Credibility stacking |
| `offer_stack` | String | Offer components | core+bonus1+bonus2+guarantee | Value stack builder |
| `offer_density` | String | Offer complexity | simple, moderate, comprehensive | Complexity matching |
| `price_flex` | String | Pricing strategy | fixed, flexible, tiered | Dynamic pricing |
| `LTV_ramp_vector` | String | LTV growth path | frontend→backend→continuity | Upsell sequencing |
| `activation_path_code` | String | Activation sequence | welcome→onboard→engage | Journey mapping |
| `breakthrough_tag` | String | Breakthrough ID | aha_moment_triggered | Momentum capture |
| `differentiator_flag` | String | Unique value prop | only_solution, fastest, proven | Positioning |
| `headline_angle` | String | Headline approach | problem_agitate, solution_benefit | Hook strategy |

---

## CATEGORY 16: Avalanche Behavior Prediction (10 parameters)

| Parameter | Type | Description | Range | Predictive Use |
|-----------|------|-------------|-------|----------------|
| `intent_lvl` | String | Purchase intent | awareness, consideration, decision | Stage-appropriate messaging |
| `urgency_score` | Number | Action urgency | 1-100 | Scarcity/urgency triggers |
| `reopt_score` | Number | Re-engagement likelihood | 1-100 | Resurrection priority |
| `frequency` | Number | Interaction frequency | 1+ | Engagement pattern |
| `exit_trigger` | String | Exit cause | price_shock, confusion, distraction | Fix friction points |
| `checkout_depth` | String | Checkout progress | cart, info, payment, complete | Abandonment intervention |
| `seen_min` | Number | Recency minutes | 0+ | Hot retarget window |
| `seen_day` | String | Recency days | day0, day1, day30 | Lifecycle stage |
| `action_momentum_score` | Number | Action velocity | 1-100 | Strike while hot |
| `sequence_loyalty_vector` | String | Engagement pattern | high_open_low_click, engaged_buyer | Content preferences |

---

## CATEGORY 17: Avalanche Narrative/Story (6 parameters)

| Parameter | Type | Description | Values | Story Control |
|-----------|------|-------------|--------|---------------|
| `narrative_breach_flag` | Boolean | Story coherence broken | true, false | Maintain consistency |
| `truth_thread_index` | String | Truth revelation sequence | revelation_1, revelation_2 | Progressive disclosure |
| `fulfillment_seal_trigger` | String | Fulfillment promise | transformation_complete | Deliver on promise |
| `narrative_arc_position` | String | Story position | setup, confrontation, resolution | Story pacing |
| `order_restoration_path` | String | Chaos→order journey | disorder→breakthrough→mastery | Transformation arc |
| `intent_chain_integrity` | Boolean | Intent alignment intact | true, false | Message consistency |

---

## CATEGORY 18: Avalanche UX/Layout (5 parameters)

| Parameter | Type | Description | Values | UX Optimization |
|-----------|------|-------------|--------|-----------------|
| `load_speed` | Number | Page load time (ms) | 0+ | <3000ms target |
| `friction_zone` | String | UX friction point | checkout_form, payment_info | Remove friction |
| `conversion_temp` | String | Conversion temperature | hot, warm, cold | Match UX to readiness |
| `brand_tone` | String | Brand voice | authoritative, friendly, casual | Tone consistency |
| `tempo_signature` | String | Pacing rhythm | slow_build, fast_urgency | Match energy level |

---

## CATEGORY 19: Avalanche System Evolution (4 parameters)

| Parameter | Type | Description | Values | AI Learning |
|-----------|------|-------------|--------|-------------|
| `context_window_range` | String | Memory span | session, week, month, lifetime | Context awareness |
| `funnel_entropy_index` | Number | Complexity score | 1-100 | Simplification needed |
| `modularity_factor` | Number | Component swappability | 1-100 | A/B test ease |
| `voice_drift` | Number | Tone consistency | 0-100 | Brand coherence |

---

## CATEGORY 20: Avalanche Compliance (4 parameters)

| Parameter | Type | Description | Values | Legal Protection |
|-----------|------|-------------|--------|------------------|
| `label_compliance` | Boolean | Claim legality | true, false | FTC compliance |
| `brand_consistency_score` | Number | Brand alignment | 1-100 | Brand guidelines |
| `voice_drift` | Number | Voice consistency | 0-100 | Messaging coherence |
| `compliance_log_id` | String | Compliance version | v2_2024_01_15 | Audit trail |

---

## CATEGORY 21: Avalanche Signal Intelligence (4 parameters)

| Parameter | Type | Description | Range | Noise Reduction |
|-----------|------|-------------|-------|-----------------|
| `signal_noise` | Number | Information clarity | 0-100 | <30 = clean message |
| `micro_signal_matrix` | String | Small signal patterns | hover_hesitation, scroll_back | Micro-behavior tracking |
| `scale_stability_score` | Number | System stability | 1-100 | Performance consistency |
| `emergence_signal_score` | Number | New pattern detection | 1-100 | Emerging trends |

---

## CATEGORY 22: Avalanche Spiritual/Ethical (5 parameters)

| Parameter | Type | Description | Values | Purpose Alignment |
|-----------|------|-------------|--------|-------------------|
| `truth_signal` | String | Authenticity indicator | genuine, hype, manipulative | Ethical marketing |
| `service_layer` | String | Service orientation | serve, sell, manipulate | Intent checking |
| `spirit_match` | String | Values alignment | aligned, neutral, misaligned | Brand integrity |
| `spiritual_readiness_index` | Number | Transformation openness | 1-100 | Readiness matching |
| `faith_factor` | Number | Trust/belief level | 1-100 | Trust building |

---

## CATEGORY 23: Avalanche Retargeting/Virality (4 parameters)

| Parameter | Type | Description | Range | Expansion Strategy |
|-----------|------|-------------|-------|---------------------|
| `network_resonance_score` | Number | Viral potential | 1-100 | Share incentives |
| `moat_score` | Number | Competitive defense | 1-100 | Positioning strength |
| `disruption_trigger` | String | Market disruption | new_competitor, price_war | Competitive response |
| `resurrection_trigger_type` | String | Re-engagement catalyst | new_offer, price_drop, scarcity | Win-back strategy |

---

## CATEGORY 24: Avalanche Creative Reuse (6 parameters)

| Parameter | Type | Description | Values | Scaling Strategy |
|-----------|------|-------------|--------|------------------|
| `funnel_script_id` | String | Funnel template | vsl_pain_agitate_solve | Template library |
| `hook_stack` | String | Hook sequence | pain→solution→proof→cta | Hook framework |
| `tone` | String | Voice tone | authoritative, empathetic | Tone library |
| `asset_type` | String | Creative type | image, video, copy | Asset organization |
| `voice` | String | Voice style | male_deep, female_warm | Voice library |
| `variant_generation` | String | Evolution generation | gen_1, gen_2, gen_3 | Creative evolution |

---

## CATEGORY 25: Avalanche Advanced Conversion (8 parameters)

| Parameter | Type | Description | Range | Conversion Optimization |
|-----------|------|-------------|-------|-------------------------|
| `conversion_latency` | Number | Time to convert (hours) | 0+ | Speed optimization |
| `checkout_depth` | String | Checkout step reached | cart, info, payment, confirmed | Abandonment analysis |
| `cta_emotion_match` | Number | CTA-emotion alignment | 1-100 | Emotional resonance |
| `cta_delay_trigger` | Number | CTA timing (seconds) | 0+ | Optimal timing |
| `hesitation_grace_timer` | Number | Hesitation allowance (sec) | 0+ | Patience vs urgency |
| `session_emotion_vector` | String | Emotion journey | fear→hope→trust | Emotional progression |
| `mirror_activation_trigger` | String | Self-reflection catalyst | identity_realization | Transformation moment |
| `token_decay_score` | Number | Token effectiveness decay | 0-100 | Refresh signals |

---


## CATEGORY 26: User Identity (PII) (8 parameters)

**Purpose:** Personal identifiable information for lead capture, CRM integration, and personalized communication.

**⚠️ GDPR/Privacy Compliance:** Only collect with explicit consent. Encrypt in transit and at rest.

| Parameter | Code | Type | Description | Validation | Use Case |
|-----------|------|------|-------------|------------|----------|
| `email` | `email` | String | Email address | RFC 5322 format | Primary contact, verification required |
| `phone` | `phone` | String | Phone number | E.164 format preferred | SMS campaigns, call booking |
| `first_name` | `first_name` | String | First name | 1-50 chars | Personalization, greetings |
| `last_name` | `last_name` | String | Last name | 1-50 chars | Full name, formal communication |
| `company` | `company` | String | Company name | 1-100 chars | B2B targeting, firmographics |
| `job_title` | `job_title` | String | Job title/role | 1-100 chars | Decision-maker identification |
| `industry` | `industry` | String | Industry/vertical | SaaS, ecommerce, healthcare, etc. | Industry-specific messaging |
| `company_size` | `company_size` | String | Employee count | 1-10, 11-50, 51-200, 201-500, 500+ | Segment by company size |

**Data Collection Best Practices:**

```javascript
// Progressive profiling - collect over time, not all at once
Step 1: email only
Step 2: email + first_name
Step 3: email + first_name + phone
Step 4: Full profile

// Validation rules
email: /^[^\s@]+@[^\s@]+\.[^\s@]+$/
phone: /^\+?[1-9]\d{1,14}$/  // E.164 format
first_name: /^[a-zA-Z\s\-']{1,50}$/
```

---

## CATEGORY 27: System Conversion Events (6 parameters)

**Purpose:** System-generated tracking for conversions, attribution, and technical debugging.

| Parameter | Code | Type | Description | Auto-Generated | Use |
|-----------|------|------|-------------|----------------|-----|
| `conversion_value` | `conversion_value` | Number | Monetary value in dollars | Set by offer/SKU | Revenue tracking, ROI |
| `conversion_type` | `conversion_type` | String | Type of conversion | lead, sale, booking, signup, download | Goal segmentation |
| `timestamp` | `timestamp` | String | Event timestamp (ISO 8601) | Auto: new Date().toISOString() | Time-based analysis |
| `page_url` | `page_url` | String | Current page URL | Auto: window.location.href | Funnel path tracking |
| `referrer` | `referrer` | String | HTTP referrer | Auto: document.referrer | Traffic source |
| `user_agent` | `user_agent` | String | Browser user agent | Auto: navigator.userAgent | Device/browser detection |

**Auto-Capture Example:**

```javascript
// Automatically captured on page load
const systemEvents = {
  timestamp: new Date().toISOString(),          // "2024-02-19T15:30:00.000Z"
  page_url: window.location.href,               // Full URL
  referrer: document.referrer,                  // Where they came from
  user_agent: navigator.userAgent,              // Browser/device string
  conversion_value: parseFloat(getParam('cv', '0')),
  conversion_type: getParam('conversion_type', 'lead')
};
```

---

## EPS vs APS PREDICTIVE INTELLIGENCE SYSTEM

### **THE COMPETITIVE ADVANTAGE**

This is the heart of AmplifAI's system: **Estimated Predictive Score (EPS) vs Actual Predictive Score (APS)**

---

### **EPS - Estimated Predictive Score (Click-Time Prediction)**

**When:** Calculated the moment user clicks ad (before landing on page)

**Input Parameters (200+ data points):**

```javascript
// Traffic Quality Signals
- publisher, pubzone, site_id
- channel (push, email, native, social)
- device_type, os, device_brand, browser
- geo: country, region, city, zip
- time: day_of_week, month, date, hour

// Creative Performance Signals  
- av (ad_variation)
- mb (media_buyer)
- ss (skip_stopper), ht (hook_type), mpp (main_pain_point)
- ii (interruptor_image), ih (image_hero), bc (body_copy)
- All 43 creative DNA parameters

// Historical Performance Data
- Past conversion rate by publisher + geo + device
- Creative variant historical performance
- Time-of-day conversion patterns
- Media buyer track record

// Audience Signals
- paud (predictive audience)
- archetype_signature_token
- psychbelief, belief_pattern
- Previous interaction history (if known)
```

**Output:** EPS score from 1-100

```
EPS Ranges:
90-100: HOT - Very likely to convert
70-89:  WARM - Good conversion potential  
50-69:  LUKEWARM - Moderate potential
30-49:  COOL - Low potential
1-29:   COLD - Very unlikely to convert
```

**EPS Calculation Logic:**

```javascript
// Simplified example (actual uses ML model)
let eps = 50; // Baseline

// Traffic quality adjustment
if (publisher === 'premium_source') eps += 15;
if (device_type === 'mobile' && device_brand === 'Apple') eps += 10;
if (city === 'San Francisco' && industry === 'SaaS') eps += 8;

// Creative performance
if (creative_variant_cvr > 5%) eps += 12;
if (archetype_match === true) eps += 10;

// Time signals
if (day_of_week === 'Tuesday' && hour >= 10 && hour <= 14) eps += 5;

// Cap at 100
eps = Math.min(eps, 100);
```

---

### **APS - Actual Predictive Score (Behavior-Updated Score)**

**When:** Updates in real-time as user behaves on site

**Starting Point:** APS = EPS (score starts equal to prediction)

**Behavior Modifiers:**

| Behavior | APS Impact | Logic |
|----------|-----------|-------|
| **Landing Page (step_1):** | | |
| Scroll depth >75% | +5 | High engagement |
| Time on page >30 seconds | +10 | Thoughtful consideration |
| CTA click | +15 | Intent signal |
| Exit intent triggered | -10 | Losing interest |
| **Survey/Form (step_2):** | | |
| Email provided | +15 | Real contact info |
| Phone provided | +15 | High intent |
| All form fields completed | +10 | Serious interest |
| Archetype detected | +10 | Personality matched |
| Survey answers aligned | +5 each | Message resonance |
| **Booking/Purchase (step_3):** | | |
| Appointment confirmed | Set to 100 | MAIN CONVERSION |
| Payment completed | Set to 100 | SALE COMPLETE |

**APS Update Example:**

```javascript
// User clicks ad
EPS = 84  // AI predicted 84% likelihood

// Step 1: Landing page behavior
scrollDepth = 82%     → APS = 84 + 5 = 89
timeOnPage = 45s      → APS = 89 + 10 = 99
ctaClick = true       → Still 99 (already high)

// Step 2: Survey submission  
emailVerified = true  → APS = 99 (can't exceed 99 pre-conversion)
phoneVerified = true  → APS = 99
archetypeDetected = true → APS = 99

// Step 3: Booking confirmed
appointmentConfirmed = true → APS = 100 (MAIN CONVERSION)

// Final Delta
EPS = 84
APS = 100
Delta = +16 (Traffic source UNDERVALUED by 16 points!)
```

---

### **THE LEARNING LOOP - Delta Analysis**

**Delta = APS - EPS**

This is the **learning signal** that trains the AI.

**Positive Delta (APS > EPS):**
```
Traffic source performed BETTER than predicted
→ AI learns to predict higher for similar patterns
→ Increase bids, scale this source
→ Replicate winning combinations

Example:
EPS = 84, APS = 100, Delta = +16
"iOS users from San Francisco convert 16 points higher than expected"
```

**Negative Delta (APS < EPS):**
```
Traffic source performed WORSE than predicted  
→ AI learns to predict lower for similar patterns
→ Decrease bids, cut this source
→ Identify losing patterns

Example:
EPS = 84, APS = 31, Delta = -53
"Android users from this publisher convert 53 points lower than expected"
```

**Learning Payload Sent to ML:**

```javascript
{
  // IDs
  conversion_id: "conv_abc123",
  timestamp: "2024-02-19T15:30:00Z",
  
  // Scores
  eps_initial: 84,
  aps_final: 100,
  eps_aps_delta: 16,
  
  // All 350+ parameters
  publisher: "premium_source",
  device_type: "mobile",
  device_brand: "Apple",
  city: "San Francisco",
  archetype: "optimizer",
  angle: "data_driven",
  av: "v2_optimizer",
  ss: "boldstatement",
  ht: "data_stat",
  // ... all parameters
  
  // Outcome
  conversion_type: "booking",
  conversion_value: 1997.00,
  funnel_step: "step_3"
}
```

**AI Training:**
1. Collects 1000s of conversion events with EPS/APS/Delta
2. Identifies patterns: "iOS + SF + optimizer + data_driven = +16 average delta"
3. Updates prediction model
4. Next similar user gets EPS = 100 instead of 84
5. Continuous improvement loop

---

## PARAMETER READING STRATEGY

**Priority Order:**

```javascript
function getParam(primaryKey, aliases, defaultValue) {
  // 1. Try URL with primary key (AdKernel official name)
  let value = urlParams.get(primaryKey);
  if (value) return value;
  
  // 2. Try URL with aliases (Keitaro, compatibility)
  if (aliases && aliases.length) {
    for (let i = 0; i < aliases.length; i++) {
      value = urlParams.get(aliases[i]);
      if (value) return value;
    }
  }
  
  // 3. Try cookie with primary key
  value = getCookie(primaryKey);
  if (value) return value;
  
  // 4. Try cookie with aliases
  if (aliases && aliases.length) {
    for (let j = 0; j < aliases.length; j++) {
      value = getCookie(aliases[j]);
      if (value) return value;
    }
  }
  
  // 5. Return default
  return defaultValue || '';
}

// Usage examples
const tracking = {
  // AdKernel (primary names, with aliases)
  conversion: getParam('conversion', ['trck', 'click_id']),
  campaign: getParam('campaign', ['campaign_id']),
  banner: getParam('banner', ['creative_id', 'banner_id']),
  publisher: getParam('publisher', ['publisher_id']),
  
  // Creative DNA (no aliases needed)
  ad_variation: getParam('av'),
  media_buyer: getParam('mb'),
  skip_stopper: getParam('ss'),
  hook_type: getParam('ht'),
  
  // Avalanche
  eps_score: parseInt(getParam('eps_score', ['eps'], '50')),
  aps_score: parseInt(getParam('aps_score', ['aps'], '50')),
  archetype: getParam('archetype'),
  angle: getParam('angle'),
  
  // Echo
  headline: getParam('hl'),
  cta_text: getParam('cta'),
  archetype: getParam('archetype'),
  phase: getParam('phase')
};
```

---

## COOKIE STORAGE RULES

**CRITICAL:** Store using PRIMARY AdKernel/official names

```javascript
// ✅ CORRECT - Use official names
setCookie('conversion', value);    // NOT conversion_id
setCookie('campaign', value);      // NOT campaign_id  
setCookie('banner', value);        // NOT banner_id
setCookie('publisher', value);     // NOT publisher_id
setCookie('eps_score', value);     // NOT eps
setCookie('aps_score', value);     // NOT aps

// Store ALL parameters
Object.keys(tracking).forEach(function(key) {
  setCookie(key, tracking[key]);
});
```

---

## GTM DATA LAYER STRUCTURE

**Use official names in dataLayer:**

```javascript
window.dataLayer.push({
  event: 'lead_conversion',
  
  // AdKernel Core (official names)
  conversion: 'conv_abc123',     // NOT conversion_id
  campaign: 'campaign_456',      // NOT campaign_id
  banner: 'creative_789',        // NOT banner_id
  publisher: 'pub_premium',      // NOT publisher_id
  
  // AdKernel Native
  city: 'San Francisco',
  device_type: 'mobile',
  device_brand: 'Apple',
  
  // Creative DNA
  ad_variation: 'v2_optimizer',
  media_buyer: 'john_doe',
  skip_stopper: 'boldstatement',
  hook_type: 'data_stat',
  
  // Avalanche
  eps_score: 84,
  aps_score: 92,
  eps_aps_delta: 8,
  archetype: 'optimizer',
  angle: 'data_driven',
  belief_pattern: 'growth_mindset',
  
  // Echo
  headline: 'Transform Your Business',
  cta_text: 'Get Started',
  funnel_intent: 'consideration',
  
  // Behavior
  scroll_depth: 82,
  time_on_page: 45,
  funnel_step: 'step_2',
  
  // User Identity
  email_verified: true,
  phone_verified: true,
  
  // Conversion
  conversion_type: 'booking',
  conversion_value: 1997.00
});
```

---

## VALIDATION CHECKLIST

Before deployment, verify:

- [ ] **No `_id` suffixes** on AdKernel params (use `conversion` not `conversion_id`)
- [ ] **Correct capitalization**: `Keyword`, `Query`, `State_Name` (capital letters)
- [ ] **All Creative DNA params** captured (av, mb, ss, ht, mpp, etc.)
- [ ] **All Avalanche params** captured (eps_score, aps_score, archetype, etc.)
- [ ] **Echo params** captured (hl, sh, cta, angle, archetype, phase)
- [ ] **Funnel journey params** tracked (funnel_step, return_visitor, scroll_depth)
- [ ] **Cookies stored** with official primary names
- [ ] **GTM dataLayer** uses official names
- [ ] **EPS/APS delta** calculated and logged
- [ ] **All 350+ parameters** feeding ML endpoint

---

## TOTAL PARAMETER COUNT: 350+

**Breakdown:**
- AdKernel Core: 6
- AdKernel Native: 38  
- Keitaro: 13
- Creative DNA Static: 21
- Creative DNA Video: 22
- Echo Landing Page: 27
- AdKernel Dynamic Macros: 10
- Keitaro Placeholders: 8
- Funnel Journey: 14
- Avalanche (17 categories): 100+
- User Identity: 8
- System Events: 6

**Total: 350+ parameters**

---

## OFFICIAL REFERENCES

- **AdKernel Macros:** https://media.amplifai.it.com/help-center/using-macros-in-direct-advertising-campaigns/
- **Keitaro Placeholders:** https://docs.keitaro.io/en/landing-pages-and-offers/placeholders.html
- **Creative DNA Static:** Meta_Static_Ad_Component_Variations_For__TPH_-_TrackingParameters.csv
- **Creative DNA Video:** Template__YouTube_Ad_Component_Variations_For__X_-_TrackingParameters.csv
- **Avalanche Master:** FINAL_AVALANCHE_MASTER_PKD___AMPLIFAI_INFINITE_TOKEN_SYSTEM
- **Avalanche Appendix:** Avalanche_Appendix_PKD
- **Intelligence Multiplier:** AVALANCHE_INTELLIGENCE_MULTIPLIER_ADDENDUM

---

**Document Version:** 2.0  
**Last Updated:** 2024-02-19  
**Status:** COMPLETE - Source of Truth  
**Total Parameters:** 350+  
**Core System:** EPS→APS Predictive Intelligence Loop

---

## END OF DOCUMENT

This is the complete parameter master reference. Every parameter feeds the competitive advantage: **EPS vs APS predictive intelligence.**

No shortcuts. No guessing. Just data-driven marketing at scale.

