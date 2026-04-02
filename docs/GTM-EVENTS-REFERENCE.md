# GTM EVENTS QUICK REFERENCE

## Event Summary

| Step | HTML Page | Event Name | DSP Step | Description |
|------|-----------|------------|----------|-------------|
| 0 | index.html | `echo_lp_view` | N/A | Landing page view (retargeting only) |
| 1 | index.html | `echo_cta_click` | step_1 | Landing page CTA clicked |
| 2 | conversion-tracker.html | `lead_conversion` | step_2 | Survey/form submitted |
| 3 | thank-you.html | `thankyou_conversion` | step_3 | Main conversion (booking/sale) |

---

## Event: echo_lp_view

**When:** User lands on page (page load)  
**DSP Step:** N/A (no AdKernel postback, retargeting only)  
**Optimization:** Build awareness audiences for retargeting

**Data Sent:**
```javascript
{
  event: 'echo_lp_view',
  conversion: 'CONV_ID',
  campaign: 'Q1_2026_fitness',
  archetype: 'optimizer',
  angle: 'data_driven',
  eps_score: 78,
  aps_score: 78,
  headline: 'Start Your Journey',
  subheadline: 'Begin today'
}
```

**Retargeting Event Fired:**
```javascript
// Immediately after echo_lp_view, fire retargeting event
dataLayer.push({
  event: 'master_lp_view_retargeting',
  conversion: conversion_id,
  archetype: archetype,
  angle: angle,
  eps_score: eps_score,
  aps_score: aps_score
});
```

**Pixels Fired:** 15 retargeting pixels
- 5 Customer Journey (cj_step0_p1 through p5)
- 5 Archetype placeholders (arch_step0_p1 through p5)
- 5 Angle placeholders (angle_step0_p1 through p5)

---

## Event: echo_cta_click

**When:** User clicks CTA button on landing page  
**DSP Step:** step_1  
**Optimization:** Which traffic sources click through?

**Data Sent:**
```javascript
{
  event: 'echo_cta_click',
  conversion: 'CONV_ID',
  cta_text: 'Get Started',
  dsp_step: 'step_1',
  time_on_page: 45
}
```

---

## Event: lead_conversion

**When:** User completes survey/form  
**DSP Step:** step_2  
**Optimization:** Which sources submit forms?

**Data Sent:**
```javascript
{
  event: 'lead_conversion',
  lead_source: 'formbricks',
  conversion_id: 'CONV_ID',
  eps_score: 85,
  aps_score: 90,
  archetype: 'optimizer',
  angle: 'data_driven',
  dsp_step: 'step_2'
}
```

---

## Event: thankyou_conversion

**When:** Main conversion achieved (booking/sale/etc)  
**DSP Step:** step_3  
**Optimization:** Which sources convert to revenue?

**Data Sent:**
```javascript
{
  event: 'thankyou_conversion',
  conversion_type: 'booking',
  conversion: 'CONV_ID',
  eps_score: 85,
  aps_score: 100,
  archetype: 'optimizer',
  dsp_step: 'step_3'
}
```

---

## GTM Tag Template (AdKernel DSP)

```html
<script>
(function() {
  var conversionId = {{DLV - conversion}};
  var dspStep = {{DLV - dsp_step}};
  var apsScore = {{DLV - aps_score}};
  
  if (conversionId && dspStep) {
    var stepNum = dspStep.replace('step_', '');
    var url = 'https://rtb2-useast.amplifai.it.com/conversion?cid=' + conversionId + '&step=' + stepNum + '&quality_score=' + apsScore;
    var img = new Image();
    img.src = url;
  }
})();
</script>
```

---

## Required Data Layer Variables

Create these in GTM Variables:

- `DLV - conversion` → conversion
- `DLV - dsp_step` → dsp_step  
- `DLV - aps_score` → aps_score
- `DLV - eps_score` → eps_score
- `DLV - archetype` → archetype
- `DLV - angle` → angle

---

## Testing with Debug Mode

Add `?debug=1` to any page URL to see detailed console logs:

```
https://lp.brand.com/?debug=1
https://lp.brand.com/conversion-tracker.html?debug=1&testsurvey=high_eps
https://lp.brand.com/thank-you.html?debug=1&type=booking
```

**Console will show:**
- ✅ Which events fired
- 📊 Data sent to GTM
- 🎯 Conversion IDs
- 📈 EPS/APS scores
