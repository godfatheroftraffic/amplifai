# Lead Engine Reporting System
## Documentation & Implementation Guide — v1.0

> **For:** Development team and AI agents working on this project.
> **Purpose:** Build the lead reactivation and reporting system described below.

---

## Table of Contents

1. [What is this?](#1-what-is-this)
2. [Business model](#2-business-model)
3. [Infrastructure stack](#3-infrastructure-stack)
4. [The lead flow](#4-the-lead-flow)
5. [Contact status framework](#5-contact-status-framework)
6. [Data attribution chain](#6-data-attribution-chain)
7. [Database schema](#7-database-schema)
8. [Reporting dashboard](#8-reporting-dashboard)
9. [Sequence optimizer](#9-sequence-optimizer)
10. [Implementation checklist](#10-implementation-checklist)
11. [Rules for AI agents and developers](#11-rules-for-ai-agents-and-developers)
12. [Demo guide](#12-demo-guide)

---

## 1. What is this?

### Plain language

Imagine a business that spends money on ads every day. People click those ads, fill out a form, and then nothing happens. They sit in a database going cold while the business keeps buying more ads. That is the single biggest revenue leak in performance marketing.

This system contacts every one of those leads automatically — using an AI voice agent, SMS, and email — within seconds of them submitting the form. When someone says yes, a checkout or booking link goes to their phone instantly. Every step is tracked so you know exactly where people are dropping off and exactly what is making them convert.

The reporting dashboard is the command center. It shows how much revenue was recovered, which messages are working, which channels are winning, and what to focus on first every day.

### What makes it work

- **Zero manual work.** Runs 24/7 without human intervention.
- **Instant contact.** New leads are dialed within 60 seconds. Speed is the highest-leverage variable.
- **Full attribution.** Every conversion traces back to the original lead and the channel that closed it.
- **Universal.** Works for any conversion event — purchase, booking, install, sign-up, lead gen.
- **Replicable.** One master config per client. New client live in minutes.

---

## 2. Business model

| Component | Description |
|-----------|-------------|
| What we do | Work uncontacted leads from existing campaigns using AI voice, SMS, and email |
| What we charge | Performance fee per confirmed conversion — client pays nothing unless we produce results |
| Our infrastructure | AI voice agent, messaging system, workflow engine, database, hosting — all owned by us |
| Attribution | Every conversion tagged by our workflow and matched to the original lead via `email` join key |
| Scale | One master template, client config file per deployment |

---

## 3. Infrastructure stack

### Our owned infrastructure

| System | Role |
|--------|------|
| **AI voice agent** (Retell AI) | Dials leads, handles conversations, collects verbal commitment |
| **AI messaging** (Closebot) | SMS and email — checkout/booking links, follow-up sequences, nurture |
| **Workflow engine** (n8n on Digital Ocean) | Orchestrates everything — triggers dials, fires messages, receives webhooks, logs data |
| **Database** (Supabase) | Lead records, conversion records, message performance data |
| **Hosting** (Cloudflare Pages) | Dashboard and landing pages |
| **Version control** (GitHub) | All code and documentation |

### Client-provided systems

| System | Role |
|--------|------|
| **CRM** | Holds lead records — we read from and write status back to this |
| **Backend / conversion system** | Confirms conversions and fires conversion webhooks to us |
| **Tracking system** | Ad attribution — client manages this independently |

---

## 4. The lead flow

### Mode A — Real-time (new leads)

```
Lead submits form
  → Webhook fires to our system instantly
  → Exclusion check: existing customers are skipped
  → AI voice agent dials within 60 seconds
  → No answer → SMS fires 15 minutes later
  → No response after N attempts → email sequence activates
  → Verbal yes → checkout/booking link sent via SMS immediately
  → Conversion confirmed → webhook received → logged to database
```

### Mode B — Legacy / dormant leads

```
Workflow engine polls CRM at defined interval
  → Finds leads with status = UNCONTACTED
  → Exclusion check: existing customers are skipped
  → Routes through same Voice → SMS → Email sequence
  → Conversion confirmed → logged to database
```

### Step by step

| Step | What happens | System |
|------|-------------|--------|
| 1 | Lead submits form with contact info, UTM parameters, and available lead attributes | Client landing page |
| 2 | Form fires webhook to our system | Client → Our system |
| 3 | Lead status set to `UNCONTACTED` | Our database |
| 4 | Exclusion check — existing customers are skipped | Workflow engine → Client backend |
| 5 | AI voice agent dials. Script personalizes using `archetype`, `angle`, and available lead attributes | Workflow engine → AI voice agent |
| 6 | No answer: SMS fires 15 minutes later | Workflow engine → AI messaging |
| 7 | No response after N attempts: email sequence activates | Workflow engine → AI messaging |
| 8 | Verbal yes: checkout/booking link sent via SMS instantly | AI voice agent → AI messaging |
| 9 | Lead converts | Client backend |
| 10 | Client backend fires conversion webhook to our system | Client → Workflow engine |
| 11 | Workflow engine matches conversion to lead via `email` join key | Workflow engine → Database |
| 12 | Attribution record logged: UTM fields, `archetype`, `angle`, `hook_type`, channel, conversion value | Database |
| 13 | Dashboard updates | Reporting dashboard |

---

## 5. Contact status framework

Every lead has exactly **one status** at all times. This rule is non-negotiable. Violations cause duplicate contacts and broken data.

| Status | Meaning | Next action |
|--------|---------|-------------|
| `UNCONTACTED` | Lead received, not yet contacted | System initiates contact |
| `IN_SEQUENCE` | Contact attempt in progress | No other flow may touch this lead |
| `CONNECTED` | AI voice agent reached lead | Monitor for verbal commitment |
| `CHECKOUT_SENT` | Conversion link delivered | Follow up in 30 minutes if no conversion |
| `CONVERTED` | Conversion confirmed by backend | Log to database |
| `DEAD` | All attempts exhausted | Move to long-term nurture only |
| `OPT_OUT` | Lead requested no contact | Never contact again |
| `CUSTOMER` | Existing customer — confirmed at intake | Exclude from all reactivation flows |

---

## 6. Data attribution chain

Every field must flow from lead submission to confirmed conversion without breaking.

| Field | Where it comes from | Where it must arrive |
|-------|--------------------|--------------------|
| `email` | Lead form | Lead record **and** conversion webhook — this is the join key |
| `phone` | Lead form | Lead record + AI voice agent dial queue |
| `first_name` | Lead form | Lead record + AI script personalization |
| `last_name` | Lead form | Lead record |
| `utm_source` | Landing page URL | Lead record + conversion record |
| `utm_campaign` | Landing page URL | Lead record + conversion record |
| `utm_content` | Landing page URL | Lead record + conversion record |
| `utm_medium` | Landing page URL | Lead record + conversion record |
| `click_id` | Ad platform click ID (fbclid, gclid, msclkid, or tracking system ID) | Lead record |
| `archetype` | Lead form or URL parameter | Lead record + AI script |
| `angle` | Lead form or URL parameter | Lead record + AI script |
| `hook_type` | Lead form or URL parameter | Lead record + message variant |
| `conversion_value` | Backend system webhook | Conversion record |
| `conversion_type` | Backend system webhook | Conversion record |

### The join key

`email` is the only field that connects a conversion record from the backend system back to the original lead record. Every conversion webhook must include the same email that was on the original form submission.

---

## 7. Database schema

### leads table

| Column | Type | Description |
|--------|------|-------------|
| `lead_id` | uuid | Primary key |
| `contact_id` | text | ID from source CRM |
| `client_id` | text | Client identifier |
| `email` | text | Primary join key — must match conversion webhook |
| `phone` | text | Used by AI voice agent and SMS |
| `first_name` | text | Personalization |
| `last_name` | text | Personalization |
| `archetype` | text | optimizer / validator / visionary / builder / explorer |
| `angle` | text | Message angle |
| `hook_type` | text | Hook type used in opening message |
| `utm_source` | text | Ad source |
| `utm_campaign` | text | Ad campaign |
| `utm_content` | text | Ad creative |
| `utm_medium` | text | Traffic medium |
| `click_id` | text | Platform or tracking system click ID |
| `lead_attributes` | jsonb | Vertical-specific lead data — intent signals, qualifiers |
| `status` | text | See contact status framework |
| `channel_closed` | text | Channel that produced conversion: voice / sms / email |
| `created_at` | timestamptz | When lead arrived |
| `first_contact_at` | timestamptz | When first contact was sent |
| `converted_at` | timestamptz | When conversion confirmed |

### conversions table

| Column | Type | Description |
|--------|------|-------------|
| `conversion` | text | From backend system — primary tracking ID, deduplicated on insert |
| `lead_id` | uuid | Foreign key to leads table |
| `email` | text | From backend webhook — join key to leads |
| `conversion_value` | numeric | Revenue or value per conversion |
| `conversion_type` | text | Type: purchase / booking / install / sign_up / lead_gen |
| `subscription_id` | text | For recurring / rebill tracking |
| `workflow_attributed` | boolean | True if our system touched this lead |
| `slot` | int | Sequence slot when conversion occurred |
| `message_variant` | text | Last variant delivered before conversion |
| `archetype` | text | Carried from lead record |
| `angle` | text | Carried from lead record |
| `hook_type` | text | Hook type of the converting message |
| `created_at` | timestamptz | Conversion timestamp |

---

## 8. Reporting dashboard

Single self-contained HTML file. Zero external dependencies. Open in any browser or deploy to Cloudflare Pages / GitHub Pages.

### Brand / client view — shown first

The brand view is a **proof-of-value report**. Not an optimization tool.

**The psychology behind what clients see:**

Clients have one question: is this working and is it worth what I am paying. They do not want to see how the system works internally. Showing optimization mechanics creates questions, not confidence. The brand view answers three things instantly:

1. How much money did the system recover?
2. Is it getting better over time?
3. Where is there still opportunity?

| What clients see | Why |
|-----------------|-----|
| Revenue Recovered — giant green number | Real dollars from leads they already paid for. The most powerful proof. |
| Our system vs their current process — RPL comparison | Quantifies the advantage in dollars per lead. Makes the fee feel like a bargain. |
| 7-day revenue trend | Shows the system is improving. Builds confidence over time. |
| Uncontacted leads urgency card | Translates idle leads into a dollar figure. Creates urgency. |
| Contact rate, conv rate, reply rate | Enough detail to build confidence without overwhelming. |
| Channel performance | Shows voice + SMS + email all working together. |
| Week-over-week improvement table | Validates momentum. |

**What clients do NOT see:** Message variants, A/B test data, other clients, sequence mechanics, optimization parameters, priority actions, cross-client intelligence.

---

### Admin view — internal team only

Six tabs. This is where all the optimization work happens. Every tab is designed so you can move from high-level overview to granular message-level detail without losing context.

**Overview** is the daily health check. It shows the top-line numbers — revenue recovered, revenue per lead, leads received, contact rate, reply rate, booked, and converted — alongside a visual conversion funnel and performance tables broken down by channel and by client. The funnel shows you exactly where leads are dropping off at each step. The brand performance table has every key metric per client so you can sort by any column and immediately see which client is underperforming and on which metric. Active and inactive clients can be filtered separately so the noise from dormant accounts doesn't bury the signal.

**Sequence optimizer** is where you find what is and is not working at the message level. Every slot in the contact sequence is listed in a sortable table — you can sort by RPV, reply rate, conversion rate, or data volume to immediately see which slots are driving the most revenue and which are underperforming. Click any slot and the detail view opens showing Voice, SMS, and Email variants stacked on top of each other. Each variant shows its full performance metrics and you can click any message to read the full copy and copy it to clipboard. Filters at the top let you narrow by client, channel, archetype, and hook type so you can isolate exactly the combinations you want to analyze.

**Split test lab** is the aggregate intelligence view. It tells you what is winning across the entire system — not just within one slot, but across all clients and all slots simultaneously. There are three sections: Hook intelligence shows which opener types are driving the highest contact rates, reply rates, and RPV. Offer intelligence shows which offers are converting best and which clients have not yet tested the top performers. CTA intelligence shows which calls to action are driving the highest conversion rates. Every section has filter dropdowns and every column is sortable. A drill-down tab lets you go Brand → Slot → Message → full copy when you want to trace a specific winner back to its source.

**Offer performance** shows every offer tested across all clients ranked by RPV. The winner is shown prominently at the top. The full history table shows Views, Conversions, Conv%, AOV, and RPV for every offer, plus a gap analysis — how many clients have tested it and how many have not, and the exact dollar value sitting on the table from not having applied the winner to every client. Sort by the gap column and the highest-value actions surface immediately.

**Cross-brand** is the replication engine. When a message, hook, or offer wins on one client, it shows up here as an opportunity to apply to the others. Rows are color coded — green means the winner has been fully replicated across all clients, red means there is a gap. The dollar value column shows exactly how much revenue is available by applying each winner to the remaining clients. This tab defaults to sorting by dollar value so the highest-leverage actions are always at the top. Filters let you narrow by client, channel, hook type, archetype, and slot.

**Priority actions** is the morning brief. It synthesizes everything in the dashboard into a single ranked list of the highest-dollar-impact actions you can take today. Each action has a category — Critical, Apply Winner, High Priority, or Optimize — a plain language description of what to do and why, the estimated dollar impact, and context tags. If you only have 30 minutes in a day to look at reporting, open this tab and start from the top.

### Key metrics

| Metric | Formula | Why it matters |
|--------|---------|----------------|
| **RPL** — Revenue Per Lead | Total revenue ÷ Total leads | North star — everything optimizes toward this |
| **RPV** — Revenue Per View | Revenue from offer ÷ Leads who saw the offer | Normalizes offer performance regardless of sequence position |
| **Contact rate** | Leads contacted ÷ Total leads | Primary lever we control |
| **Reply rate** | Replies ÷ Messages sent | Measures SMS and email hook effectiveness |
| **Conv rate** | Conversions ÷ Total leads | Overall system conversion |
| **$ Gap value** | Winner RPV × Leads on untested clients | Dollar value of not replicating a winner |

---

## 9. Sequence optimizer

The sequence is a series of numbered **slots**. Slot 1 is the first contact — highest value. Each slot has message variants tested per channel.

| Term | Meaning |
|------|---------|
| `slot` | Numbered position in the sequence. Separate optimization container. Never compare variants across slots. |
| `variant` | A specific message tested within a slot for a channel. A, B, C, etc. |
| `hook_type` | Psychological approach of the opener: `data_stat`, `pain_point`, `social_proof`, `transformation`, `fear` |
| `archetype` | Lead profile: `optimizer`, `validator`, `visionary`, `builder`, `explorer` |
| `angle` | Broader message framing |
| Winner | Highest RPV at 95%+ significance. Ready for replication across clients. |
| Low data | Under 100 messages. Do not optimize on low-data slots. |

| Channel | Primary metric | Secondary |
|---------|---------------|-----------|
| Voice | Contact % | Conv %, RPV |
| SMS | Reply % | Click %, Conv %, RPV |
| Email | Open % (subject line) | Click %, Conv %, RPV |

---

## 10. Implementation checklist

### Phase 1 — Data plumbing

- [ ] `email` present on both lead webhook and conversion webhook
- [ ] `phone` and `first_name` present in lead webhook
- [ ] UTM parameters in lead webhook: `utm_source`, `utm_campaign`, `utm_content`, `utm_medium`
- [ ] `click_id` captured and passed in lead webhook
- [ ] `archetype`, `angle`, `hook_type` passed in lead webhook if available
- [ ] `conversion_value` and `conversion_type` in backend system webhook
- [ ] Deduplication on conversion webhooks — same conversion must not process twice
- [ ] CRM API access confirmed
- [ ] AI voice agent API key and agent ID per client
- [ ] Backend system webhook endpoint confirmed
- [ ] Customer exclusion check working

### Phase 2 — Workflow build

- [ ] Real-time trigger — new leads dial within 60 seconds of form submission
- [ ] Contact status gate — every workflow step checks current status before acting
- [ ] Exclusion check runs before every first dial
- [ ] AI voice agent receives `archetype`, `angle`, `hook_type`, `first_name` as script variables
- [ ] No-answer SMS fires 15 minutes after missed dial
- [ ] Checkout/booking link SMS fires on verbal yes from voice agent webhook
- [ ] Dormant lead poller for legacy uncontacted leads
- [ ] Conversion webhook handler — deduplicates, joins via `email`, logs to database
- [ ] Client config file — all values from `brand-config.json`, nothing hardcoded

### Phase 3 — Dashboard live data

- [ ] Replace demo data with live Supabase queries
- [ ] Dashboard refreshes every 60 seconds
- [ ] UTM warning banner when `utm_source` is missing on recent leads
- [ ] Priority actions generated from live gap analysis

---

## 11. Rules for AI agents and developers

| Rule | Why |
|------|-----|
| Read the full file before making any change | Stale base files are the primary source of regressions |
| Surgical edits only — never rewrite working code | Rewrites break attribution and conversion tracking |
| Validate before every delivery | Catches issues before they reach production |
| `email` is the join key — it must exist on every lead and conversion record | Without it, conversions cannot be attributed |
| `status` must use exact values from the contact status framework | Any other value breaks the contact gate |
| `conversion_type` is generic — never assume it means purchase | System must work for any conversion type |
| All values from `brand-config.json` — nothing hardcoded | Hardcoded values block replication across clients |
| `archetype` values: `optimizer`, `validator`, `visionary`, `builder`, `explorer` only | Other values break message routing |
| Never build before explicit approval | Strategy confirmed before code is written |
| Contact status gate must run before every workflow action | Prevents duplicate contacts and data corruption |

---

## 12. Demo guide

8-10 minutes. Start with the client view, end with the admin view.

1. **Brand view — revenue recovered first.** *"This is what your system recovered today from leads already in your database."*
2. **Show the comparison line.** *"Our system generates X% more revenue per lead. Across today's volume that is an extra $X,XXX."*
3. **Show the urgency card.** *"You have XXX uncontacted leads right now. At your RPV that is $XX,XXX on the table."*
4. **Switch to Admin, Overview tab.** Walk the funnel. Each percentage is a lever.
5. **Sequence Optimizer — drill into Slot 1.** Show Variant A vs B. RPV difference. *"This is exactly which words are making people convert."*
6. **Priority Actions.** Top three items. *"Every morning this tells us where to focus first."*
7. **Close.** *"Zero manual work. Fully automated. Everything visible in real time."*

---

*Lead Engine Reporting System — v1.0 — Confidential*
