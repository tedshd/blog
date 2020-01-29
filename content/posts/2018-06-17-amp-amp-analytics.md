---
layout: post
title: 'AMP - amp analytics & conversion'
date: 2018-06-17
comments: true
categories: [amp]
---
## AMP - amp analytics & conversion

Use google analytics must use `amp-analytics` component

It can use PHP print template function to view

First include

```html
<script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
```

### ga click event

[Refer - Adding Analytics to your AMP pages](https://developers.google.com/analytics/devguides/collection/amp-analytics/)

```php
function amp_ga_event_click_template($ga_id, $selector, $cate, $action, $label, $non_interaction = "0")
{

$template = <<<EOF
<amp-analytics type="googleanalytics">
<script type="application/json">
    {
        "vars": {
            "account": "%s"
        },
        "triggers": {
            "trackClickOnHeader" : {
                "on": "click",
                "selector": "%s",
                "request": "event",
                "vars": {
                    "eventCategory": "%s",
                    "eventAction": "%s",
                    "eventLabel": "%s"
                },
                "extraUrlParams": {
                    "ni": "%s"
                }
            }
        }
    }
</script>
</amp-analytics>
EOF;
    return printf($template, $ga_id, $selector, $cate, $action, $label, $non_interaction);
}
```

### google adwords conversion

[Refer - Using AMP for your AdWords Landing Pages](https://developers.google.com/adwords/amp/landing-pages)

For landing page pageview

```php
function amp_ga_conversion_pageview_template($conversion_id, $lang = "en", $conversion_label)
{

$template = <<<EOF
<amp-analytics type="googleadwords">
  <script type="application/json">
  {
    "triggers": {
      "onVisible": {
        "on": "visible",
        "request": "conversion"
      }
    },
    "vars": {
      "googleConversionId": "%s",
      "googleConversionLanguage": "%s",
      "googleConversionFormat": "3",
      "googleConversionLabel": "%s",
      "googleRemarketingOnly": "false"
    }
  }
  </script>
</amp-analytics>
EOF;
    return printf($template, $conversion_id, $lang, $conversion_label);
}
```

For click conversion

```php
function amp_ga_conversion_click_template($ga_id, $selector, $conversion_id, $conversion_label, $non_interaction = "0")
{

$template = <<<EOF
<amp-analytics type="googleadwords">
  <script type="application/json">
  {
    "vars": {
        "account": "%s"
    },
    "triggers": {
        "trackClickOnHeader" : {
            "on": "click",
            "selector": "%s",
            "request": "conversion",
            "vars": {
                "googleConversionId": "%s",
                "googleConversionFormat": "3",
                "googleConversionLabel": "%s",
                "googleRemarketingOnly": "false"
            },
            "extraUrlParams": {
                "ni": "1"
            }
        }
    }
  }
  </script>
</amp-analytics>
EOF;

    return printf($template, $ga_id, $selector, $conversion_id, $conversion_label, $non_interaction);
}
```
