**AMPLIFAI ACQUISITION OS**

**Typebot Universal Intelligence Schema**

PKD v2.0  —  Project Knowledge Document

*AI: 99% execution  |  Human: 1% copy-paste  |  Universal: any brand, any vertical, any conversion*

*This document is the complete operating intelligence for the AmplifAI Universal Typebot Schema. The AI reads it to know what to build. The human reads it to know what to do. Every brand-specific value lives exclusively in brand-config.json — never in code. This document is vertical-agnostic and works for any product, service, or market.*

**CRITICAL — READ BEFORE PROCEEDING**

v2.0 CORRECTIONS FROM v1.0:

1\. TypeBot deployment is REDIRECT only. There is no embed. All TypeBot URLs receive parameters

   as URL query strings. TypeBot auto-injects matching URL params into declared variables.

   Remove all references to prefilledVariables embed code from your memory.

2\. NOTHING brand-specific is hardcoded in any code, template, or instruction.

   Brand-specific values (pain signals, desire signals, qualification gates, routing rules,

   income tiers, qualification conditions) live ONLY in brand-config.json.

   The AI reads brand-config first, then generates code from those values.

3\. Disqualification routing is managed inside the TypeBot flow using native

   Condition blocks. The AI builds these blocks by reading the routing rules

   from brand-config.json. The human does not configure routing separately.

4\. All routing logic is brand-specific and lives in brand-config.json or in TypeBot flow.

**Section 1 — The Universal Rule (Read This First)**

**UNIVERSAL RULE**

THE SINGLE NON-NEGOTIABLE PRINCIPLE THAT GOVERNS EVERYTHING:

Brand-config.json is the single source of truth for ALL brand-specific values.

This includes: pain signals, desire signals, qualification gates, routing rules,

income tiers, disqualification conditions, conversion types, conversion platforms,

redirect URLs, brand slot definitions, allowed values per slot, copy variants,

market sophistication level, lead quality score weights, and everything else

that differs between brands, verticals, products, or markets.

Code reads from brand-config. Code never contains brand values.

Instructions reference brand-config keys. Instructions never contain brand values.

This document is brand-agnostic. It describes the system, not any specific brand.

When the AI builds any Set Variable block, any Condition block, any redirect URL, any copy variant — it FIRST reads the relevant brand-config section to get the values. It then generates the code using those values. The instruction in this document describes WHAT to build and WHERE to read the values from. It never tells the AI WHAT THE VALUES ARE.

Example of correct AI behavior: 'Read brand-config.framework\_variables.motivation\_type.pain\_signals. Use those values to build the Set Variable code block for motivation\_type.'

Example of WRONG AI behavior: 'Build a Set Variable block that checks for frustrating, gave-up-on-apps, not-wife-material.' — These are brand-specific values that should never appear in an instruction.

**Section 2 — The Strategic Foundation: 20 Minds**

This section exists so that both the AI and the human understand WHY this system is built the way it is. Every architectural decision maps to a proven framework from one of these minds. When the AI expands the system, it uses these principles as reasoning guardrails. When the human reviews the system, they understand the logic behind each design choice.

The AI must apply these principles proactively — not just when prompted. When building any new feature, the AI should ask: which of these frameworks applies? What would these minds say about this design decision?

**The Foundational Frameworks**

**1\. Gary Bencivenga**  —  Greatest Living Copywriter

*Strategic principle: The Ultimate Reason Why is the intersection of the user's deepest pain and most desired outcome. Every piece of copy must be built around that specific gap.*

System decision: pain\_primary \+ desire\_primary are both captured and combined into brand\_profile\_summary. Every downstream touchpoint reads this gap. The copy is never generic — it is always anchored to the specific user's stated pain and stated desire.

**2\. Eugene Schwartz**  —  Breakthrough Advertising

*Strategic principle: Market sophistication determines how messaging must be framed. The same claim lands differently depending on how much the market has already been exposed to it.*

System decision: market\_sophistication (1-5) is set in brand-config per vertical. The system selects hooks, angles, and creative from sophistication-matched libraries. The signal cascade refines the user's individual sophistication level from the angle they responded to.

**3\. Robert Cialdini**  —  Influence \+ Pre-Suasion

*Strategic principle: Commitment escalates through consistent small actions. The final psychological state before a decision is determined by what question was asked immediately beforehand.*

System decision: commitment\_depth tracks micro-commitments (questions answered). The commitment\_sequence in brand-config defines the final 3 questions before the conversion CTA — calibrated to maximize psychological readiness. These are a strategic asset, not UI decisions.

**4\. Daniel Kahneman**  —  Thinking Fast and Slow

*Strategic principle: System 1 (fast, instinctive) and System 2 (slow, deliberate) require completely different triggering conditions. Deliberate buyers convert at higher LTV.*

System decision: Early quiz questions use System 1 triggers (image choices, binary preferences). Later questions engage System 2\. cognitive\_engagement\_depth measures how deeply the user engaged System 2 — slow answers on deliberate questions signal a high-value buyer for premium routing.

**5\. BJ Fogg**  —  Stanford Behavior Design

*Strategic principle: Behavior requires Motivation, Ability, and Prompt to converge simultaneously. Abandonment means one of the three failed.*

System decision: drop\_off\_point captures exactly where a user left. The recovery system diagnoses which element failed — motivation (desire amplification recovery), ability (friction removal), or prompt (urgency trigger) — and selects the matching recovery sequence from brand-config.

**6\. Alex Hormozi**  —  $100M Offers

*Strategic principle: The offer frame matters as much as the offer. Away-from buyers need risk reversal first. Toward buyers need the dream outcome first.*

System decision: motivation\_type (pain or desire) is the fork that selects the offer frame from brand-config.post\_conversion.upsell. The same underlying offer renders with completely different framing per user. Frame variants live in brand-config — never in code.

**7\. David Ogilvy**  —  Father of Advertising

*Strategic principle: The intelligence moat compounds over time. Data from every campaign should make the next campaign better. Brands that attract the wrong customers at scale face a positioning crisis.*

System decision: EPS/APS/Delta creates a permanent learning loop. Every conversion cycle trains the prediction model. brand\_profile\_summary is compared against brand-config brand promise to detect psychological-fingerprint mismatches before they become refund problems.

**8\. Dan Kennedy**  —  Godfather of Direct Response

*Strategic principle: CPL is the wrong metric. Cost per qualified lead — leads that cleared all gates and scored above the hot threshold — is the number that predicts sales team ROI.*

System decision: lead\_quality\_score routes leads automatically. The hot threshold is in brand-config. Only leads above that threshold reach the sales team. The primary campaign optimization metric is cost\_per\_qualified\_lead, not CPL. This is enforced in the GTM reporting layer.

**9\. Andrew Ng**  —  AI Pioneer, Stanford

*Strategic principle: Transfer learning means new models don't start from zero. Universal schemas create network intelligence effects — every brand's data improves every other brand's predictions.*

System decision: The universal variable schema (same names across all brands) makes every brand's signal data compatible. Phase 3 pools anonymized EPS/APS/Delta pairs across brands. New brands initialize from the aggregate model. Cold start problem solved through schema universality.

**10\. Nir Eyal**  —  Hooked

*Strategic principle: Investment in a process increases the psychological cost of abandonment. Recovery messages that reference the user's specific sunk cost dramatically outperform generic retargeting.*

System decision: steps\_completed and drop\_off\_point enable sunk\_cost\_message\_template in brand-config. The recovery message is generated from the user's specific quiz investment — not generic copy. Brand-config defines the template; the system populates it with user data.

**11\. Seth Godin**  —  Tribes

*Strategic principle: People buy who they want to become, not what they want to have. Tribal identity is a stronger conversion driver than demographics, pain, or desire alone.*

System decision: identity\_type captures the tribal self-image the user confirmed through quiz answers. The identity\_echo\_protocol in brand-config defines how every downstream touchpoint reflects this identity back to the user — in email openers, SMS hooks, AI voice scripts, and sales pre-briefs.

**12\. Naval Ravikant**  —  Leverage \+ Compounding

*Strategic principle: The universal schema is the code layer that scales infinitely without proportional cost increases. Schema standardization creates network effects that compound across the portfolio.*

System decision: Every variable name is identical across every brand. Intelligence earned on one brand partially transfers to every other brand. The schema is the asset — more durable than any specific campaign, funnel, or creative.

**13\. Charlie Munger**  —  Mental Models \+ Inversion

*Strategic principle: Invert: what would make this system fail? Overfitting on small samples, optimizing for the wrong metric, and AI drift away from business reality are the three primary failure modes.*

System decision: model\_confidence\_threshold in brand-config prevents AI weight adjustment before minimum conversion events. Routing thresholds are human-controlled and cannot be AI-adjusted. The system only learns when it has statistically sufficient signal.

**14\. Peter Thiel**  —  Contrarian Strategy

*Strategic principle: The moat is not the quiz. The moat is the universal schema combined with cross-brand learning. Competitors can copy a funnel. They cannot copy two years of accumulated psychological-signal-to-conversion training data.*

System decision: The intelligence moat is built through schema universality \+ EPS/APS learning \+ cross-brand signal pooling. This is a 10-year structural advantage that grows with every conversion event across every brand on the system.

**15\. Jeff Bezos**  —  Customer Obsession \+ Systems

*Strategic principle: Work backwards from the customer experience. The feeling of being understood is the rarest and most powerful experience a brand can create. That feeling must persist across every touchpoint.*

System decision: brand\_profile\_summary is the continuity mechanism. The user's fingerprint travels across email, SMS, voice, retargeting, and sales — so every touchpoint feels like it remembers them. The flywheel: better fingerprinting → more relevant follow-up → higher conversion → more data → better fingerprinting.

**16\. B.F. Skinner**  —  Behavioral Conditioning

*Strategic principle: Variable ratio reinforcement is the most powerful schedule. Each micro-reward during the quiz increases the probability of the next action. Post-conversion reinforcement determines show rate.*

System decision: The quiz's Noted / Finalizing / Compatible matches found messages are engineered reinforcement events. The post-conversion reinforcement\_sequence in brand-config defines each touchpoint as a specific reinforcement type (variable reward, identity reinforcement, loss aversion).

**17\. Claude Shannon**  —  Information Theory

*Strategic principle: Not all questions carry equal information. Questions that reduce the most uncertainty about conversion probability are the most valuable. Low-information questions add length without adding predictive power.*

System decision: quiz\_completion\_time combined with steps\_completed enables information gain analysis per question. After sufficient data volume, questions are ranked by entropy reduction. Low-gain questions are flagged for removal from brand-config. Shorter quiz, same fingerprint accuracy.

**18\. Sam Altman**  —  AI Scale \+ Agentic Systems

*Strategic principle: The transition from AI as a tool to AI as an agent changes everything. The first agentic loop — generating, testing, and auto-updating copy — is the inflection point.*

System decision: The first agentic loop reads pain\_primary from Supabase, generates subject line variants, deploys in rotation via n8n, reads open rates, and updates the winning template in brand-config — without human involvement. The human only sees the result. One loop compounds into the next.

**19\. Russell Brunson**  —  Funnel Architecture \+ Value Ladder

*Strategic principle: Peak psychological engagement happens immediately after conversion. Immediate post-conversion offers at that moment convert at 20-35% without any additional traffic.*

System decision: brand-config.post\_conversion.upsell defines the immediate offer shown on the thank-you page within 5 seconds of conversion confirmation. motivation\_type selects the frame variant. Pain-dominant users see risk reversal. Desire-dominant users see outcome acceleration. All in brand-config.

**20\. Carlos — The Godfather of Traffic**  —  20 Years. This Is The System.

*Strategic principle: Ship fast. Every day of delay is a lost learning cycle. The architecture compounds from the first conversion — not from the day it's perfectly architected.*

System decision: v1 ships with core schema, qualification gate, and redirect flow. Enhancements activate as data accumulates. The system gets smarter with every conversion. The only irreversible decision is not to start.

**Section 3 — What This System Is (Explain Like I'm 5\)**

**The Old Way**

Every funnel used to collect data the same way a teacher collects homework. You filled out a form. The data went into a spreadsheet. Someone looked at it later and maybe sent you an email. The data and the marketing were disconnected. Personalization was manual, slow, and inconsistent.

**What This System Does**

Imagine you meet someone at a party and in 5 minutes they know: your name, your biggest frustration, what you dream about, and exactly what kind of person you want to be. Then they use all of that to say exactly the right thing at every moment — and every person they meet after you makes them smarter.

That is this system. The quiz is the conversation. The variables are the memory. The AI is the conversationalist. And every user who completes the quiz makes the system smarter for every user who comes after them — across every brand.

**The Three Things Nobody Else Has**

**1\. A psychological fingerprint, not just a lead record.**

The ad clicked, the CTA chosen, the questions answered — combined into a fingerprint that reveals whether the user is running away from pain or running toward a desire. This drives every downstream message automatically.

**2\. One fingerprint, every channel, automatically.**

Email, SMS, AI voice call, retargeting, sales team pre-brief — all read from the same fingerprint. No manual segmentation. No copy-pasting. The same intelligence travels across the entire follow-up system.

**3\. It gets smarter with every conversion.**

EPS predicted how likely a user was to convert. APS tracked what they actually did. The gap (Delta) is the learning signal. Every conversion cycle makes the next prediction more accurate. After 90 days this system knows your market better than any human analyst could.

**Redirect Flow (How TypeBot Receives Parameters)**

There is no embedded TypeBot on the landing page. The landing page CTA button sends the user to the TypeBot URL with all tracking parameters appended as URL query string parameters. TypeBot automatically injects URL parameters into declared variables with matching names. No additional configuration is required beyond declaring the variables.

USER JOURNEY:

1\. User clicks ad

   AdKernel fires URL: lp.domain.com/?conversion=X\&campaign=Y\&banner=Z\&city=Miami...

2\. Landing page loads

   index.html reads all URL params, stores all in cookies (365-day expiry)

   Page renders with dynamic headline and CTA from brand-config

3\. User clicks CTA button

   LP builds TypeBot URL with all params from cookies:

   typebot.io/\[bot-id\]?conversion=X\&campaign=Y\&cta=build-your-ideal-wife\&eps=72...

   Browser redirects user to that URL

4\. TypeBot loads

   TypeBot auto-injects URL params into matching declared variables

   Quiz runs, variables are captured, Set Variable blocks compute intelligence

5\. TypeBot completes

   TypeBot Redirect block sends user to conversion-tracker.html with all variables

   Disqualification routes are handled inside TypeBot flow via Condition blocks

   Condition block rules are read from brand-config by the AI when building the flow

**Section 4 — Full System Architecture**

**Data Flow — End to End**

AD CLICK

  AdKernel Core: conversion, campaign, banner, publisher, offer, goal\_id

  AdKernel Personalization: city, device\_type, device\_brand, os, carrier, day\_of\_week, ip...

  Avalanche Tokens: cta, at, ag, ad, phase, eps, av, mb, hl

  Initial seeds: market\_sophistication (from brand-config), motivation\_type (from hl+ag)

      ↓

LANDING PAGE

  Reads URL params → stores all in cookies

  CTA button builds TypeBot redirect URL from cookies

      ↓

TYPEBOT (redirect URL with all params)

  Auto-injected (no config): Layers 1, 2, 3 variables

  Quiz captures: brand\_q1-q5, pain\_experience, pain\_obstacle, desire\_primary,

                 desire\_values, identity\_type, demo\_age, demo\_income, verification\_type

  Lead captures: email, first\_name, mobile

  Set Variable (computed): motivation\_type, qualified, aps\_score, lead\_quality\_score,

                           brand\_profile\_summary, belief\_barrier, steps\_completed,

                           drop\_off\_point, cognitive\_engagement\_depth

  Condition block (reads brand-config routing rules):

    → Qualified \= false: Redirect to brand-config.conversion\_event.disqualify\_redirect

    → Qualified \= true: Redirect to conversion-tracker.html with all variables

      ↓

CONVERSION TRACKER

  GTM fires: lead\_conversion (step 2\) with full dataLayer

  AdKernel postbacks: XML \+ DSP with aps\_score

  Supabase: full parameter payload stored

      ↓

CONVERSION EVENT (type defined in brand-config)

  GTM fires: thankyou\_conversion (step 3\)

  APS \= 100, Delta \= APS \- EPS, learning payload sent

      ↓

DOWNSTREAM (all read brand\_profile\_summary \+ motivation\_type)

  Email | SMS | AI Voice | Retargeting | Sales CRM | Bid Optimization

**Signal Cascade — How Psychological Variables Get Set**

Every psychological variable follows a three-layer cascade. The ad makes a hypothesis. The quiz gathers evidence. The behavior finalizes. Each layer either confirms or overrides the previous. Weight of each layer is configured in brand-config.

LAYER 1 — Ad Signal (hypothesis, weight: configurable in brand-config)

  ag (angle) responded to → seeds market\_sophistication

  hl (headline) frame → seeds motivation\_type

  cta selected → seeds awareness\_stage

LAYER 2 — Quiz Answers (evidence, weight: configurable in brand-config)

  Brand-config defines which answer values are pain signals vs desire signals

  AI reads brand-config.framework\_variables.motivation\_type.pain\_signals

  AI reads brand-config.framework\_variables.motivation\_type.desire\_signals

  Answer pattern determines confirmed motivation\_type

  demo\_income checked against brand-config.demo\_variables.demo\_income.qualification\_gate

LAYER 3 — Behavior (confirmation, weight: configurable in brand-config)

  cognitive\_engagement\_depth: time-weighted answer speed per question type

  drop\_off\_point: last question reached (updated at each question start)

  steps\_completed: total answers given

**Section 5 — Brand-Config Schema: New Sections**

These sections are added to the existing brand-config.json. The AI reads these sections to generate all TypeBot Set Variable code, all Condition block routing, all copy variants, and all qualification logic. No values from these sections ever appear hardcoded in any code file.

**Universal Structure (brand-specific values are placeholders)**

{

  "market\_intelligence": {

    "sophistication": \[INTEGER 1-5 — set per vertical\],

    "sophistication\_label": "\[unaware|problem\_aware|solution\_aware|product\_aware|most\_aware\]",

    "awareness\_stage\_default": "\[string\]",

    "sophistication\_weights": {

      "ad\_signal": \[0.0-1.0\],

      "cta\_signal": \[0.0-1.0\],

      "quiz\_answers": \[0.0-1.0\]

    }

  },

  "conversion\_event": {

    "type": "\[booking|call|sale|lead|app\_install|trial|download\]",

    "platform": "\[cal.com|stripe|shopify|typeform|custom\]",

    "value": \[DOLLAR AMOUNT or 0\],

    "qualified\_threshold": \[INTEGER 0-100\],

    "disqualify\_redirect": "\[FULL URL\]"

  },

  "framework\_variables": {

    "motivation\_type": {

      "pain\_signals": \["\[brand-specific answer values that indicate pain motivation\]"\],

      "desire\_signals": \["\[brand-specific answer values that indicate desire motivation\]"\],

      "pain\_weight": \[0.0-1.0\],

      "desire\_weight": \[0.0-1.0\]

    },

    "pain\_experience": {

      "label": "\[Question text shown to user\]",

      "input\_type": "choice",

      "values": \["\[answer1\]", "\[answer2\]", "\[answer3\]", "\[answer4\]"\]

    },

    "pain\_obstacle": {

      "label": "\[Question text shown to user\]",

      "input\_type": "choice",

      "values": \["\[answer1\]", "\[answer2\]", "\[answer3\]", "\[answer4\]"\]

    },

    "desire\_primary": {

      "label": "\[Question text shown to user\]",

      "input\_type": "choice",

      "values": \["\[answer1\]", "\[answer2\]", "\[answer3\]", "\[answer4\]"\]

    },

    "desire\_values": {

      "label": "\[Question text shown to user\]",

      "input\_type": "multi-select",

      "values": \["\[value1\]", "\[value2\]", "\[value3\]", "\[value4\]"\]

    },

    "identity\_type": {

      "label": "\[Question text shown to user\]",

      "input\_type": "choice",

      "values": \["\[identity1\]", "\[identity2\]", "\[identity3\]", "\[identity4\]"\]

    }

  },

  "brand\_slots": {

    "q1": { "label": "\[slot purpose\]", "input\_type": "\[picture\_choice|choice|multi-select|text\]",

            "values": \["\[val1\]","\[val2\]"\], "image\_set": "\[image folder name or null\]" },

    "q2": { "label": "\[slot purpose\]", "input\_type": "\[type\]",

            "values": \["\[val1\]","\[val2\]","\[val3\]","\[val4\]"\], "image\_set": "\[folder or null\]" },

    "q3": { "label": "\[slot purpose\]", "input\_type": "\[type\]",

            "values": \["\[val1\]","\[val2\]","\[val3\]","\[val4\]"\], "image\_set": "\[folder or null\]" },

    "q4": { "label": "\[slot purpose\]", "input\_type": "\[type\]",

            "values": \["\[val1\]","\[val2\]","\[val3\]","\[val4\]","\[val5\]"\] },

    "q5": { "label": "\[slot purpose\]", "input\_type": "\[type\]",

            "values": \["\[val1\]","\[val2\]","\[val3\]","\[val4\]"\] }

  },

  "demo\_variables": {

    "demo\_income": {

      "label": "\[Question text\]",

      "input\_type": "choice",

      "values": \["\[tier1\]","\[tier2\]","\[tier3\]","\[tier4\]","\[tier5\]"\],

      "qualification\_gate": { "disqualify\_if": "\[value that fails qualification\]" }

    },

    "demo\_gender": { "enabled": \[true|false\] },

    "demo\_age": { "enabled": \[true|false\], "min": 18, "max": 99 }

  },

  "routing": {

    "qualified\_path": "/conversion-tracker.html",

    "disqualified\_path": "\[brand-config.conversion\_event.disqualify\_redirect\]",

    "fallback\_path": "/conversion-tracker.html"

  },

  "lead\_quality\_scoring": {

    "weights": {

      "email\_verified": \[0-100\],

      "phone\_verified": \[0-100\],

      "scroll\_depth\_75": \[0-100\],

      "time\_on\_page\_30": \[0-100\],

      "archetype\_detected": \[0-100\],

      "form\_fields\_filled\_3": \[0-100\],

      "steps\_completed\_9": \[0-100\],

      "income\_qualified": \[0-100\],

      "motivation\_type\_detected": \[0-100\],

      "awareness\_stage\_detected": \[0-100\]

    },

    "cap": 100,

    "routing": { "hot": \[threshold\], "warm": \[threshold\], "cold": 0 },

    "ai\_learning": \[true|false\],

    "ai\_learning\_target": "conversion\_confirmed",

    "ai\_learning\_cycle": "\[daily|weekly|monthly\]",

    "model\_confidence\_threshold": \[min conversions before AI adjusts weights\]

  },

  "commitment\_sequence": {

    "pre\_cta\_questions": \["\[var\_name\_1\]","\[var\_name\_2\]","\[var\_name\_3\]"\],

    "commitment\_message": "\[loading message shown during simulated analysis\]"

  },

  "brand\_profile\_summary\_template":

    "\[Template string using {variable\_name} tokens — defined per brand\]",

  "post\_conversion": {

    "micro\_commitment": {

      "question": "\[Question text\]",

      "values": \["\[option1\]","\[option2\]","\[option3\]","\[option4\]"\]

    },

    "upsell": {

      "enabled": \[true|false\],

      "pain\_frame": "\[Copy shown to motivation\_type=pain users\]",

      "desire\_frame": "\[Copy shown to motivation\_type=desire users\]"

    }

  },

  "sophistication\_matched\_hooks": {

    "1": "\[Hook for unaware market\]",

    "2": "\[Hook for problem aware market\]",

    "3": "\[Hook for solution aware market\]",

    "4": "\[Hook for product aware market\]",

    "5": "\[Hook for most aware market\]"

  }

}

**Section 6 — Complete Variable Schema (63 Variables)**

Every variable in this schema must be declared in TypeBot before any flow is built. Variable names are universal and identical across all brands. What each variable contains is determined by the brand flowing through the system.

**Layer 1 — AdKernel Core**

CRITICAL: No \_id suffixes. conversion not conversion\_id. campaign not campaign\_id.

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **conversion** | AK Core | String | AdKernel {conversion} | Unique click ID string | Postback, APS/EPS tracking |
| **campaign** | AK Core | String | AdKernel {campaign} | Campaign ID | Performance attribution, bid optimization |
| **banner** | AK Core | String | AdKernel {banner} | Creative ID | Creative A/B, scale winners |
| **publisher** | AK Core | String | AdKernel {publisher} | Source ID | Quality scoring, blacklist/whitelist |
| **offer** | AK Core | String | AdKernel {offer} | Offer ID | Multi-offer tracking |
| **goal\_id** | AK Core | String | AdKernel {goal\_id} | Conversion goal ID | Postback routing value |

**Layer 2 — AdKernel Personalization**

State\_Name requires capital S and N. Keyword requires capital K. Query requires capital Q.

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **city** | AK Personal | String | AdKernel {city} | City name | Email subject, AI voice opener, LP personalization |
| **country\_name** | AK Personal | String | AdKernel {country\_name} | Full country name | International routing |
| **region** | AK Personal | String | AdKernel {region} | State/province | Regional offers, legal routing |
| **State\_Name** | AK Personal | String | AdKernel {State\_Name} | Full state — caps required | Legal copy |
| **device\_type** | AK Personal | String | AdKernel {device\_type} | mobile/desktop/tablet | Flow optimization, APS signal |
| **os** | AK Personal | String | AdKernel {os} | iOS/Android/Windows | LTV segmentation |
| **device\_brand** | AK Personal | String | AdKernel {device\_brand} | Apple/Samsung/etc | Affluence proxy, APS scoring |
| **carrier** | AK Personal | String | AdKernel {carrier} | Carrier name | SMS deliverability |
| **day\_of\_week** | AK Personal | String | AdKernel {day\_of\_week} | Monday-Sunday | Best contact timing |
| **date** | AK Personal | String | AdKernel {date} | YYYY-MM-DD | Seasonal analysis, reporting |
| **ip** | AK Personal | String | AdKernel {ip} | IP address — DO NOT save | Fraud detection only |
| **pubzone** | AK Personal | String | AdKernel {pubzone} | Zone ID | Placement quality scoring |
| **bid** | AK Personal | Number | AdKernel {bid} | Dollar amount | Cost tracking, ROI |

**Layer 3 — Avalanche Intelligence Tokens**

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **cta** | Avalanche | String | URL param from LP | brand-config CTA set values | Echo statement, email subject match, retargeting |
| **at** | Avalanche | String | URL param from ad | 1-5 archetype slot | Messaging selection, email routing |
| **ag** | Avalanche | String | URL param from ad | 1-5 angle slot | Seeds market\_sophistication, creative continuity |
| **ad** | Avalanche | String | URL param from ad | P1\_AT2\_AG3\_V007 format | Full creative DNA, AI training |
| **phase** | Avalanche | String | URL param from ad | P1|P2|P3|P4|P5 | Journey phase, sequence selection |
| **eps** | Avalanche | Number | URL param (AI predicted) | 0-100 integer | APS baseline, delta training signal |
| **av** | Avalanche | String | URL param from ad | v1|v2|test-a | Ad variation attribution |
| **mb** | Avalanche | String | URL param from ad | Buyer ID | Per-buyer performance tracking |
| **hl** | Avalanche | String | URL param from LP | Headline text | Seeds motivation\_type, echo congruence |
| **sh** | Avalanche | String | URL param from LP | Sub Headline text | Seeds motivation\_type, echo congruence |

**Layer 4 — Framework Psychology Variables**

These implement the Schwartz \+ Bencivenga \+ Cialdini \+ Fogg frameworks. Values are defined in brand-config. Code never contains brand-specific values.

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **market\_sophistication** | Framework | Number | brand-config (AI reads on build) | 1-5 integer | Creative rotation, hook library selection |
| **awareness\_stage** | Framework | String | Signal cascade computed | unaware|problem\_aware|solution\_aware|product\_aware | Sequence selection, retargeting angle |
| **pain\_experience** | Framework | String | TypeBot choice input | Defined in brand-config | motivation\_type computation |
| **pain\_obstacle** | Framework | String | TypeBot choice input | Defined in brand-config | Bencivenga gap, email copy, AI voice |
| **pain\_primary** | Framework | String | Set Variable \= pain\_obstacle | Same as pain\_obstacle | Alias used by downstream AI agents |
| **desire\_primary** | Framework | String | TypeBot choice input | Defined in brand-config | Bencivenga gap, offer framing, email |
| **desire\_values** | Framework | String | TypeBot multi-select | Comma-separated selected values | Closing bridge, sales anchor |
| **motivation\_type** | Framework | String | Signal cascade computed | pain | desire | THE marketing switch — forks all downstream |
| **identity\_type** | Framework | String | TypeBot choice input | Defined in brand-config | Tribal echo, email persona, sales framing |
| **commitment\_depth** | Framework | Number | Set Variable \= steps\_completed | 0-10 | APS contribution, show rate, recovery priority |
| **cognitive\_engagement\_depth** | Framework | Number | Computed time-weighted | 0-10 scale | Premium path routing, high-value buyer |
| **verification\_type** | Framework | String | TypeBot choice input | Defined in brand-config | Reminder copy, meeting format |
| **belief\_barrier** | Framework | String | Set Variable computed | Constructed string | Sales pre-brief, objection handling |

**Layer 5 — Demographics**

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **demo\_age** | Demographics | Number | TypeBot numeric input | 18-99 | Eligibility, age-appropriate messaging |
| **demo\_income** | Demographics | String | TypeBot choice input | Defined in brand-config | QUALIFICATION GATE — routes user path |
| **demo\_gender** | Demographics | String | TypeBot choice input | Defined in brand-config | Archetype refinement (optional per brand) |

**Layer 6 — Brand Slots**

Variable names are universal. Content is 100% brand-config defined. Same 5 slots work for any vertical.

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **brand\_q1** | Brand Slots | String | TypeBot picture/choice | brand-config brand\_slots.q1.values | Brand personalization, brand\_profile\_summary |
| **brand\_q2** | Brand Slots | String | TypeBot picture/choice | brand-config brand\_slots.q2.values | Brand personalization, brand\_profile\_summary |
| **brand\_q3** | Brand Slots | String | TypeBot choice/text | brand-config brand\_slots.q3.values | Brand personalization, brand\_profile\_summary |
| **brand\_q4** | Brand Slots | String | TypeBot choice/text | brand-config brand\_slots.q4.values | Brand personalization, brand\_profile\_summary |
| **brand\_q5** | Brand Slots | String | TypeBot multi-select | brand-config brand\_slots.q5.values | Brand personalization, brand\_profile\_summary |

**Layer 7 — Lead Capture**

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **email** | Lead | String | TypeBot email input | user@email.com | CRM, email sequences, dedup |
| **first\_name** | Lead | String | TypeBot text input | Free text | All personalization tokens |
| **mobile** | Lead | String | TypeBot phone input | E.164 format | SMS, AI voice, recovery |

**Layer 8 — Conversion Event (Universal)**

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **conversion\_type** | Conv Event | String | brand-config | booking|call|sale|lead|app\_install|trial|download | CT page mode, GTM routing, postback |
| **conversion\_status** | Conv Event | String | Set after event | pending|confirmed|cancelled|no\_show | Reminder triggers, resurrection |
| **conversion\_value** | Conv Event | Number | brand-config | Dollar amount | ROI, postback value, LTV |
| **conversion\_platform** | Conv Event | String | brand-config | cal.com|stripe|shopify|typeform|custom | API routing |
| **booking\_id** | Conv Event | String | Platform API | Reference ID | Reschedule, cancel, no-show |
| **booking\_date** | Conv Event | String | Platform API | YYYY-MM-DD | Reminder triggers |
| **booking\_time** | Conv Event | String | Platform API | HH:MM | Display \+ SMS copy |
| **booking\_timezone** | Conv Event | String | Platform API | e.g. America/New\_York | Correct time in reminders |

**Layer 9 — Behavioral Signals**

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **funnel\_step** | Behavioral | String | Set Variable | step\_1|step\_2|step\_3 | GTM event tracking, APS calculation |
| **steps\_completed** | Behavioral | Number | Computed: increment | 0-10 count | Commitment depth, LQS, quiz completion |
| **quiz\_completion\_time** | Behavioral | String | Set Variable on open | ISO timestamp | Fast=impulse, slow=deliberate buyer |
| **drop\_off\_point** | Behavioral | String | Set Variable per question | Question label string | Recovery targeting, failure diagnosis |
| **post\_booking\_priority** | Behavioral | String | TypeBot choice post-conversion | Defined in brand-config | Show rate signal, sales opener |

**Layer 10 — Predictive Intelligence**

| Variable | Layer | Type | Set By | Values | Downstream Use |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **aps\_score** | Predictive | Number | Computed: eps \+ modifiers | 0-100 (100=converted) | Postback quality, routing, bids |
| **lead\_quality\_score** | Predictive | Number | Computed: weighted formula | 0-100 | Sales routing, follow-up cadence |
| **brand\_profile\_summary** | Predictive | String | Computed: constructed string | Template from brand-config | ALL downstream AI agents |
| **qualified** | Predictive | Boolean | Computed: income gate | true|false | Routes: true→CT, false→disqualify |
| **disqualified\_reason** | Predictive | String | Computed if qualified=false | Reason string | Nurture strategy, disqualification tracking |
| **motivation\_type** | Predictive | String | Signal cascade | pain|desire | THE marketing switch |
| **awareness\_stage** | Predictive | String | Signal cascade | Schwartz level string | Sequence, creative, hook selection |
| **belief\_barrier** | Predictive | String | Computed | Constructed string | Sales pre-brief, objection handling |

**Section 7 — AI Build Instructions (The 99%)**

**CRITICAL — READ BEFORE PROCEEDING**

BEFORE WRITING ANY CODE, THE AI MUST:

1\. Read the brand-config.json file for the target brand in full.

2\. Extract all brand-specific values from brand-config (pain signals, desire signals,

   income tiers, routing rules, brand slot definitions, commitment sequence, etc.)

3\. Use ONLY those extracted values when generating Set Variable code.

4\. NEVER hardcode values that belong in brand-config.

5\. If a value is missing from brand-config, STOP and flag it. Do not guess or substitute.

**Build Task 1 — Variable Declaration**

**AI EXECUTES THIS**

Declare all 63 variables in TypeBot Variables panel before building any flow.

Enable Save in Results for all variables except: ip

Variable names are case-sensitive. Use exact names from Section 6\.

Layers 1, 2, 3 variables: declare only — no input blocks needed, auto-injected from URL.

Layer 10 variables: declare only — Set Variable blocks will populate them.

**Build Task 2 — Computed Set Variable Blocks**

All code below uses placeholders. AI replaces placeholders with values read from brand-config before generating the actual code block in TypeBot.

**motivation\_type**

**AI EXECUTES THIS**

Read from brand-config: framework\_variables.motivation\_type.pain\_signals (array)

Read from brand-config: framework\_variables.motivation\_type.desire\_signals (array)

Read from brand-config: framework\_variables.motivation\_type.pain\_weight

Read from brand-config: framework\_variables.motivation\_type.desire\_weight

Trigger: After pain\_obstacle is captured in TypeBot flow.

Execute on client: NO

Generated code pattern:

  const painSignals \= \[VALUES FROM brand-config.pain\_signals\];

  const desireSignals \= \[VALUES FROM brand-config.desire\_signals\];

  const painHits \= \[{{pain\_experience}},{{pain\_obstacle}}\].filter(v=\>painSignals.includes(v)).length;

  const desireHits \= \[{{desire\_primary}},{{desire\_values}}\]

    .filter(v=\>desireSignals.some(s=\>v&\&v.includes(s))).length;

  return painHits \>= desireHits ? 'pain' : 'desire';

**qualified**

**AI EXECUTES THIS**

Read from brand-config: demo\_variables.demo\_income.qualification\_gate.disqualify\_if

Trigger: After demo\_income is captured.

Generated code pattern:

  return {{demo\_income}} \!== '\[VALUE FROM brand-config.qualification\_gate.disqualify\_if\]';

**brand\_profile\_summary**

**AI EXECUTES THIS**

Read from brand-config: brand\_profile\_summary\_template

Trigger: After all brand slots and framework variables are captured.

Generated code: replace {variable\_name} tokens in the template with {{variable\_name}} TypeBot syntax.

Example pattern (template defines the structure — AI does not invent it):

  return brand-config.brand\_profile\_summary\_template

    .replace('{brand\_q1}', {{brand\_q1}})

    .replace('{desire\_primary}', {{desire\_primary}})

    \[etc for each token in the template\]

**lead\_quality\_score**

**AI EXECUTES THIS**

Read from brand-config: lead\_quality\_scoring.weights (all weight values)

Read from brand-config: lead\_quality\_scoring.cap

Trigger: After email and mobile are captured.

Generated code uses weight VALUES from brand-config — not hardcoded numbers.

Pattern:

  let score \= 0;

  if ({{email}} && {{email}}.includes('@')) score \+= \[brand-config email\_verified weight\];

  if ({{mobile}} && {{mobile}}.length \>= 10\) score \+= \[brand-config phone\_verified weight\];

  if (parseInt({{steps\_completed}}) \>= 9\) score \+= \[brand-config steps\_completed\_9 weight\];

  if ({{demo\_income}} \!== '\[brand-config disqualify\_if value\]') score \+= \[income\_qualified weight\];

  if ({{motivation\_type}}) score \+= \[brand-config motivation\_type\_detected weight\];

  if ({{awareness\_stage}}) score \+= \[brand-config awareness\_stage\_detected weight\];

  return Math.min(score, \[brand-config cap\]);

**aps\_score**

**AI EXECUTES THIS**

Trigger: Final block before redirect.

Read from brand-config: lead\_quality\_scoring (for signal weights)

Generated code pattern:

  let aps \= parseInt({{eps}}) || 50;

  if ({{email}}) aps \+= 15;

  if ({{mobile}}) aps \+= 15;

  if (parseInt({{steps\_completed}}) \>= 9\) aps \+= 10;

  if ({{motivation\_type}}) aps \+= 5;

  if ({{qualified}} \=== 'true' || {{qualified}} \=== true) aps \+= 10;

  return Math.min(aps, 99);

Note: aps\_score stays below 100 until the conversion event fires (set to 100 by GTM).

**belief\_barrier**

**AI EXECUTES THIS**

Trigger: After pain\_obstacle and identity\_type are captured.

Generated code:

  return 'Barrier: ' \+ {{pain\_obstacle}} \+ ' | Identity: ' \+ {{identity\_type}};

**steps\_completed (increment after each question)**

**AI EXECUTES THIS**

Add this Set Variable block after EVERY quiz input block in the flow.

  return (parseInt({{steps\_completed}}) || 0\) \+ 1;

Add a Set Variable block at the START of each question group:

  drop\_off\_point \= '\[label of this question\]'

This ensures drop\_off\_point always holds the user's furthest point in the flow.

**pain\_primary (alias)**

**AI EXECUTES THIS**

Trigger: Same block as pain\_obstacle capture.

  return {{pain\_obstacle}};

This creates a universal alias that downstream AI agents can reference consistently.

**Build Task 3 — Routing Condition Blocks**

**AI EXECUTES THIS**

Read from brand-config: routing.qualified\_path

Read from brand-config: routing.disqualified\_path

Read from brand-config: demo\_variables.demo\_income.qualification\_gate.disqualify\_if

After demo\_income is captured and qualified is computed, build a Condition block:

  Condition: {{qualified}} is equal to false

  → Redirect block: URL \= \[brand-config routing.disqualified\_path\]

  Condition: {{qualified}} is equal to true (or default/else branch)

  → Continue to commitment sequence and lead capture

The disqualify redirect URL is always read from brand-config.

It is never hardcoded in the TypeBot flow.

Different brands have different disqualification destinations.

TypeBot manages this routing natively via its Condition block.

**Build Task 4 — Commitment Sequence**

**AI EXECUTES THIS**

Read from brand-config: commitment\_sequence.pre\_cta\_questions (array of 3 variable names)

Read from brand-config: commitment\_sequence.commitment\_message

Order the final 3 questions before the conversion CTA exactly as listed in brand-config.

These 3 questions are the Cialdini commitment escalation sequence.

They are a strategic asset — the sequence is brand-config defined, not UI-decided.

After the 3rd question:

  → Text bubble: \[brand-config commitment\_sequence.commitment\_message\]

  → Wait block: 1500ms

  → Text bubble: \[brand-config: result found message\]

  → Proceed to verification framing and conversion CTA

**Build Task 5 — Conversion Tracker Redirect**

**AI EXECUTES THIS**

The final TypeBot Redirect block builds the conversion-tracker URL.

All variables are passed as URL query parameters.

No parameter is optional. All 40+ listed below must be present.

Use the exact parameter names shown — they match the CT page's expected param names.

REDIRECT URL STRUCTURE (build as single concatenated string, no line breaks):

/conversion-tracker.html

  ?conversion={{conversion}}

  \&campaign={{campaign}}

  \&banner={{banner}}

  \&publisher={{publisher}}

  \&offer={{offer}}

  \&goal\_id={{goal\_id}}

  \&at={{at}}\&ag={{ag}}\&ad={{ad}}\&phase={{phase}}

  \&eps={{eps}}\&aps={{aps\_score}}

  \&av={{av}}\&mb={{mb}}\&hl={{hl}}\&cta={{cta}}

  \&name={{first\_name}}\&email={{email}}\&mobile={{mobile}}

  \&demo\_age={{demo\_age}}\&demo\_income={{demo\_income}}

  \&brand\_q1={{brand\_q1}}\&brand\_q2={{brand\_q2}}\&brand\_q3={{brand\_q3}}

  \&brand\_q4={{brand\_q4}}\&brand\_q5={{brand\_q5}}

  \&pain\_primary={{pain\_obstacle}}\&pain\_experience={{pain\_experience}}

  \&desire\_primary={{desire\_primary}}\&desire\_values={{desire\_values}}

  \&motivation\_type={{motivation\_type}}\&identity\_type={{identity\_type}}

  \&awareness\_stage={{awareness\_stage}}\&market\_sophistication={{market\_sophistication}}

  \&lead\_quality\_score={{lead\_quality\_score}}\&commitment\_depth={{steps\_completed}}

  \&quiz\_completion\_time={{quiz\_completion\_time}}\&drop\_off\_point={{drop\_off\_point}}

  \&brand\_summary={{brand\_profile\_summary}}\&belief\_barrier={{belief\_barrier}}

  \&qualified={{qualified}}\&disqualified\_reason={{disqualified\_reason}}

  \&city={{city}}\&device\_type={{device\_type}}\&device\_brand={{device\_brand}}

  \&os={{os}}\&carrier={{carrier}}\&day\_of\_week={{day\_of\_week}}

  \&conversion\_type={{conversion\_type}}

**Section 8 — Human 1% Checklist**

These are the only things the human needs to do. Ten steps. Everything else is built by the AI. Plain English. Copy-paste only. If you're unsure what something means, that's fine — just follow the step exactly.

**CRITICAL — READ BEFORE PROCEEDING**

DO NOT start these steps until the AI confirms variable declaration is complete.

DO NOT publish TypeBot until ALL 10 steps are done and the AI confirms each one.

DO NOT edit the TypeBot flow directly — tell the AI what to change.

**Step 1: Open TypeBot and Create the Bot**

Go to: app.typebot.io (log in)

Click: \+ New typebot

Name: \[Brand Name\] Echo Funnel v1

Click: Start from scratch

Do not add anything yet.

Tell the AI: TypeBot is open and blank. Ready for variable declaration.

**Step 2: Declare All 63 Variables**

The AI will give you the list of variable names — all 63 of them.

In TypeBot: click the '@' Variables button (top right corner).

For EACH name: click \+, type the exact name, press Enter.

Do not change any spelling or capitalization.

When done: go back through and toggle 'Save in results' ON for every variable.

Exception: do NOT enable Save in results for the variable named: ip

Tell the AI: All 63 variables declared. Ready for flow build.

**Step 3: Set Up the Conversion Platform (e.g. Cal.com)**

Go to your conversion platform (cal.com, Stripe, Shopify, or whatever is set in brand-config).

Create the conversion event (booking page, product, form, etc.) per your brand setup.

Set the post-conversion redirect to: /thank-you.html

Copy the conversion URL.

Give the AI this URL. The AI will insert it into the TypeBot flow.

**Step 4: Upload Quiz Images to Cloudflare (if brand uses picture choices)**

Generate images per the brand-config image\_set definitions.

Upload to: /public/images/quiz/\[image\_set\_name\]/ in your Cloudflare Pages repo.

File names must match exactly what the AI specifies from brand-config.

Tell the AI: Images uploaded. Give the AI your Cloudflare domain.

**Step 5: Review the TypeBot Flow (AI Built This)**

The AI will share a preview URL or ask you to review specific flow sections.

Click through the flow as a test user.

Report to the AI anything that looks wrong, broken, or unexpected.

Do not change anything yourself — tell the AI what to fix.

**Step 6: Publish the TypeBot**

In TypeBot: click Publish (top right).

Copy the public URL that appears.

Give this URL to the AI.

The AI will update the landing page CTA to redirect to this URL with all tracking params.

**Step 7: Run the Qualified Path Test**

The AI will give you an exact test URL to open in your browser.

It will look like: \[TypeBot URL\]?conversion=TEST001\&campaign=999&...

Open it. Go through the full quiz. Select the qualifying option on the income question.

Confirm you land on: conversion-tracker.html

Open browser DevTools (F12) → Console → look for: GTM event fired, AdKernel postback fired.

Tell the AI exactly what you see (including any errors).

**Step 8: Run the Disqualified Path Test**

Use the same test URL.

Go through the quiz. Select the disqualifying income option.

Confirm you land on the disqualification destination (set in brand-config).

If you land anywhere else: stop and tell the AI.

Tell the AI: Disqualification test passed (or describe what went wrong).

**Step 9: Update the Landing Page CTA**

The AI will provide the exact code change needed to the index.html CTA button.

The change updates the button href to redirect to the TypeBot URL with all params.

Copy the exact code the AI provides. Paste it into the correct location in index.html.

Commit and push to trigger Cloudflare deployment.

Tell the AI: Landing page updated and deployed.

**Step 10: Launch First Campaign**

The AI will provide the exact AdKernel campaign URL with all macros configured.

Paste this URL as the landing page destination in your AdKernel campaign.

Set your test budget (recommended: $50-100/day for first 7 days).

Launch the campaign.

Tell the AI: Campaign is live. Provide the campaign ID from AdKernel.

The AI will confirm tracking is working correctly within 24 hours of first click data.

**Section 9 — Locked Enhancement Roadmap**

Eleven enhancements are locked and sequenced. They are built in dependency order. None activate without live quiz data from v1. The build order is non-negotiable — it follows the data dependency chain.

**Now (Before v1 Ships)**

**Commitment Sequence Optimization (\#12 — Cialdini)**

Built directly into the TypeBot flow. brand-config.commitment\_sequence defines the final 3 questions. The AI orders them correctly. Delivers 30-40% conversion lift from day one at zero additional cost.

**Cost Per Qualified Lead as Primary Metric (\#4 — Kennedy)**

brand-config defines the hot threshold. GTM tracks cost\_per\_qualified\_lead as the primary optimization metric. Every campaign that runs without this metric trains AdKernel on the wrong signal.

**Phase 1 — Days 1-30 After Launch**

**Investment-Referenced Abandonment Recovery (\#10 — Eyal)**

n8n workflow triggers when steps\_completed \>= 3 but no email is captured. Recovery message references drop\_off\_point and steps\_completed. Template is defined in brand-config.recovery.sunk\_cost\_template. Recovery message is never hardcoded.

**Dynamic Offer Framing (\#3 — Hormozi)**

CT and TY pages read motivation\_type from URL params. Render pain\_frame or desire\_frame from brand-config.post\_conversion.upsell. Nothing hardcoded on the page — all copy in brand-config.

**Identity Echo Protocol (\#14 — Godin)**

Email and SMS sequences inject identity\_type. Opening line template defined in brand-config.identity\_echo\_protocol with {motivation\_type} and {identity\_type} tokens. Sales CRM receives brand\_profile\_summary as pre-brief.

**Dynamic Copy from Pain/Desire Gap (\#8 — Bencivenga)**

After 200+ completions. Top pain/desire gap combinations analyzed. Email template library built — one per dominant combination. Templates defined in brand-config. n8n reads motivation\_type and selects template.

**Phase 2 — Days 30-90**

**Behavioral Failure Diagnosis (\#11 — Fogg)**

Requires 300+ drop\_off\_point data points. AI classifies abandonment as motivation/ability/prompt failure. Three recovery sequence branches built, all defined in brand-config.recovery.failure\_sequences.

**Sophistication-Matched Creative Rotation (\#6 — Schwartz)**

Requires 500+ completions. Creative tag library built mapped to market\_sophistication values in brand-config.sophistication\_matched\_hooks. AdKernel campaign structure updated.

**First Agentic Optimization Loop (\#5 — Altman)**

Requires 1000+ recovery emails sent. AI generates subject variants from pain\_primary. Deploys in rotation. Reads open rates. Updates winning template in brand-config.recovery.subject\_lines. Runs weekly.

**Phase 3 — Multi-Brand Scale (90+ Days)**

**Cross-Brand Transfer Learning (\#2 — Andrew Ng)**

Requires BBM v1 live plus one additional brand on the same schema. Anonymized signal pooling. New brands initialize EPS from aggregate model. Schema universality is what makes this possible.

**Intelligence Moat / Schema Data Pooling (\#9 — Thiel)**

Requires 3+ brands and 10,000+ conversion events portfolio-wide. Central signal library in Supabase. Cross-brand EPS accuracy compounds. The schema standard becomes the moat.

**Section 10 — Validation Protocol**

**AI Pre-Delivery Checklist**

**AI EXECUTES THIS**

Before declaring any TypeBot build complete, verify:

VARIABLE DECLARATION

  \[ \] All 63 variables declared — exact names, case-sensitive

  \[ \] Save in results: ON for all except ip

  \[ \] Zero typos verified

BRAND-CONFIG COMPLIANCE

  \[ \] Zero hardcoded brand values in any Set Variable code

  \[ \] All pain\_signals, desire\_signals, income tiers read from brand-config

  \[ \] All routing URLs read from brand-config

  \[ \] All copy variants read from brand-config

REDIRECT FLOW

  \[ \] TypeBot is redirect deployment (not embed)

  \[ \] LP CTA button builds TypeBot URL with all tracking params from cookies

  \[ \] All 40+ parameters present in CT redirect URL

  \[ \] conversion parameter present (NOT conversion\_id)

  \[ \] aps\_score is between 51-99 for test user (not 0, not 100\)

ROUTING

  \[ \] Condition block reads qualified variable correctly

  \[ \] Disqualified path URL matches brand-config.conversion\_event.disqualify\_redirect

  \[ \] Qualified path sends user to conversion-tracker.html

COMPUTED VARIABLES

  \[ \] motivation\_type returns 'pain' or 'desire' — never null

  \[ \] brand\_profile\_summary contains no undefined tokens

  \[ \] lead\_quality\_score is 0-100

  \[ \] belief\_barrier is a non-empty string

TRACKING

  \[ \] GTM lead\_conversion event fires on CT page load

  \[ \] dataLayer contains motivation\_type, aps\_current, lead\_quality\_score

  \[ \] AdKernel XML postback fires (xml.amplifai.it.com)

  \[ \] AdKernel DSP postback fires (rtb2-useast.amplifai.it.com)

AmplifAI Autonomous Compounding Engine  ·  Typebot Universal Intelligence Schema  ·  PKD v2.0