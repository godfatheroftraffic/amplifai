# BRAND CONFIG GUIDE

## 🎯 QUICK REFERENCE: What Humans Must Configure

**5 things you MUST set (10 minutes):**

1. **Brand Name:**
```json
   "brand": { "name": "Your Brand Name" }
```

2. **GTM Container ID:**
```json
   "brand": { "gtmId": "GTM-XXXXXXX" }
```
   *(Get from: Google Tag Manager → Admin → Container ID)*

3. **Domain:**
```json
   "brand": { "domain": "lp.yourbrand.com" }
```

4. **Footer Links:**
```json
   "footer": {
     "links": {
       "privacy": { "url": "https://yourbrand.com/privacy" },
       "terms": { "url": "https://yourbrand.com/terms" }
     }
   }
```

**Everything else is optional.**  
**AI handles the rest automatically.**


Complete reference for all `brand-config.json` options.

---

## Structure Overview

```json
{
  "brand": { ... },           // Brand identity
  "landing_page": { ... },    // Landing page defaults & styling
  "footer": { ... },          // Footer links
  "consent": { ... },         // GDPR/CCPA settings
  "conversion_tracker": { ... } // A/B testing & webhooks
}
```

---

## Brand Identity

```json
"brand": {
  "name": "Your Brand Name",
  "domain": "lp.yourbrand.com",
  "gtmId": "GTM-XXXXXXX",
  "copyright": "© 2024 Your Brand Name. All rights reserved."
}
```

**Options:**
- `name` - Brand name (used in default config, tracking)
- `domain` - Landing page domain
- `gtmId` - **REQUIRED** - Google Tag Manager container ID
- `copyright` - Footer copyright text

---

## Landing Page Defaults

```json
"landing_page": {
  "defaults": {
    "headline": "Transform Your Business Today",
    "subheadline": "Join thousands of...",
    "cta_text": "Get Started Now",
    "cta_link": "https://calendly.com/yourbrand/meeting",
    "background_image": "hero-background.jpg",
    "overlay": "dark"
  }
}
```

**Options:**
- `headline` - Default headline (overridden by `?hl=` URL param)
- `subheadline` - Default subheadline (overridden by `?sh=`)
- `cta_text` - Default button text (overridden by `?cta=`)
- `cta_link` - Default button destination (overridden by `?link=`)
- `background_image` - Default image from `/public/` folder (overridden by `?img=`)
- `overlay` - Default darkness: `"light"` | `"medium"` | `"dark"` | `"xdark"`

**URL Parameter Overrides:**
All landing page defaults can be overridden via URL:
```
?hl=Custom+Headline&sh=Custom+Subheadline&cta=Click+Here&img=custom.jpg
```

---

## Landing Page Styling

```json
"landing_page": {
  "styling": {
    "headline_size": "3rem",
    "headline_color": "#ffffff",
    "subheadline_size": "1.5rem",
    "subheadline_color": "#ffffff",
    "button_color": "#2563eb",
    "button_text_color": "#ffffff",
    "button_size": "large",
    "button_style": "rounded"
  }
}
```

**Options:**
- `headline_size` - CSS font size (e.g., `"3rem"`, `"48px"`)
- `headline_color` - Hex color (e.g., `"#ffffff"`)
- `subheadline_size` - CSS font size
- `subheadline_color` - Hex color
- `button_color` - Button background color
- `button_text_color` - Button text color
- `button_size` - `"small"` | `"medium"` | `"large"` | `"xlarge"`
- `button_style` - `"square"` | `"rounded"` | `"pill"`

**URL Parameter Overrides:**
```
?btn_color=%23ff0000&btn_size=xlarge&btn_style=pill
```

---

## Landing Page Features

### Social Proof
```json
"features": {
  "social_proof": {
    "enabled": true,
    "default_text": "Join 10,000+ satisfied customers"
  }
}
```

Shows trust badge below CTA button.

**URL Override:** `?social_proof=on&social_text=Custom+text`

### Scarcity
```json
"features": {
  "scarcity": {
    "enabled": false,
    "default_spots": 3,
    "default_text": "Only {spots} spots remaining!"
  }
}
```

Shows red scarcity banner. `{spots}` is replaced with number.

**URL Override:** `?scarcity=5&scarcity_text=Only+{spots}+left!`

---

## Footer

```json
"footer": {
  "enabled": true,
  "links": {
    "privacy": {
      "enabled": true,
      "text": "Privacy",
      "url": "https://yourbrand.com/privacy"
    },
    "terms": {
      "enabled": true,
      "text": "Terms",
      "url": "https://yourbrand.com/terms"
    },
    "cookies": {
      "enabled": true,
      "text": "Cookies",
      "url": "https://yourbrand.com/cookies"
    },
    "contact": {
      "enabled": true,
      "text": "Contact",
      "url": "https://yourbrand.com/contact"
    }
  }
}
```

**Options:**
- `enabled` - Show/hide entire footer
- Each link has:
  - `enabled` - Show/hide this link
  - `text` - Link text
  - `url` - Link destination

---

## Consent (GDPR/CCPA)

```json
"consent": {
  "requireConsent": false,
  "requirePIIConsent": false
}
```

**Options:**
- `requireConsent` - Require cookie consent before setting cookies
- `requirePIIConsent` - Require PII consent before sending email/phone to webhooks

---

## Conversion Tracker: Split Testing

```json
"conversion_tracker": {
  "splitTest": {
    "enabled": true,
    "variants": [
      {
        "name": "control",
        "url": "https://calendly.com/yourbrand/30min",
        "weight": 50,
        "enabled": true
      },
      {
        "name": "variant_a",
        "url": "https://calendly.com/yourbrand/15min",
        "weight": 30,
        "enabled": true
      },
      {
        "name": "variant_b",
        "url": "https://yourbrand.com/video",
        "weight": 20,
        "enabled": false
      }
    ]
  }
}
```

**Options:**
- `enabled` - Enable/disable split testing
- `variants` - Array of test variations
  - `name` - Variant identifier
  - `url` - Destination URL
  - `weight` - Traffic percentage (must total 100 for enabled variants)
  - `enabled` - Turn variant on/off

**Auto-Rebalancing:**
If variant_b is disabled, traffic automatically rebalances:
- Control: 50 → 62.5%
- Variant A: 30 → 37.5%

**URL Override:**
```
?variant=control         (Force specific variant)
?dest=https://...        (Direct destination, skip split test)
```

---

## Conversion Tracker: Webhook Thresholds

```json
"webhookThresholds": {
  "ai_call_min_eps": 70,
  "sms_min_eps": 50,
  "email_min_eps": 30
}
```

**Cost Optimization:**
Only fire expensive webhooks (AI calls, SMS) for high-quality leads.

**Options:**
- `ai_call_min_eps` - Minimum EPS score to trigger AI call (0-100)
- `sms_min_eps` - Minimum EPS to send SMS
- `email_min_eps` - Minimum EPS to send email

**Example:**
- Lead with EPS 85 → AI Call ✅, SMS ✅, Email ✅
- Lead with EPS 60 → AI Call ❌, SMS ✅, Email ✅
- Lead with EPS 25 → AI Call ❌, SMS ❌, Email ❌

---

## Conversion Tracker: DSP Postback

```json
"dspPostback": {
  "enabled": true,
  "adkernel_campaign_id": "3214529",
  "step_mapping": {
    "survey_complete": "step_3",
    "calendar_booked": "step_4",
    "payment_complete": "step_5"
  }
}
```

**Options:**
- `enabled` - Send conversion postbacks to AdKernel/Keitaro
- `adkernel_campaign_id` - Your AdKernel campaign ID
- `step_mapping` - Map conversion types to DSP steps

**Purpose:**
Sends EPS/APS scores back to DSP for bid optimization.

---

## Conversion Tracker: Timing

```json
"timing": {
  "webhookTimeout": 3000,
  "redirectDelay": 3000,
  "fallbackLinkDelay": 10000
}
```

**Options (all in milliseconds):**
- `webhookTimeout` - Max time to wait for webhook response (3000 = 3 seconds)
- `redirectDelay` - Delay before redirecting user (3000 = 3 seconds)
- `fallbackLinkDelay` - When to show "Click to Continue" link (10000 = 10 seconds)

---

## Complete Example: E-commerce Brand

```json
{
  "brand": {
    "name": "ShopWave",
    "domain": "lp.shopwave.com",
    "gtmId": "GTM-ABC123",
    "copyright": "© 2024 ShopWave Inc."
  },
  
  "landing_page": {
    "defaults": {
      "headline": "Shop Smarter, Save More",
      "subheadline": "Exclusive deals on 10,000+ products",
      "cta_text": "Browse Deals",
      "cta_link": "https://shopwave.com/deals",
      "background_image": "shopwave-hero.jpg",
      "overlay": "medium"
    },
    "styling": {
      "button_color": "#ff6b35",
      "button_size": "xlarge",
      "button_style": "pill"
    },
    "features": {
      "social_proof": {
        "enabled": true,
        "default_text": "1M+ happy shoppers"
      },
      "scarcity": {
        "enabled": true,
        "default_spots": 50,
        "default_text": "Only {spots} left at this price!"
      }
    }
  },
  
  "footer": {
    "enabled": true,
    "links": {
      "privacy": { "enabled": true, "text": "Privacy", "url": "https://shopwave.com/privacy" },
      "terms": { "enabled": true, "text": "Terms", "url": "https://shopwave.com/terms" }
    }
  },
  
  "conversion_tracker": {
    "splitTest": {
      "enabled": true,
      "variants": [
        { "name": "product_page", "url": "https://shopwave.com/products/best-seller", "weight": 60, "enabled": true },
        { "name": "category_page", "url": "https://shopwave.com/deals", "weight": 40, "enabled": true }
      ]
    },
    "webhookThresholds": {
      "ai_call_min_eps": 80,
      "sms_min_eps": 60,
      "email_min_eps": 40
    }
  }
}
```

---

## Testing Your Config

After customizing, test with:

**Landing Page:**
```
https://lp.yourbrand.com/
```

**With Custom Params:**
```
https://lp.yourbrand.com/?hl=Special+Offer&cta=Claim+Now&img=special.jpg
```

**Conversion Tracker:**
```
https://lp.yourbrand.com/conversion-tracker.html?testsurvey=high_eps
```

See TESTING.md for complete test scenarios.
