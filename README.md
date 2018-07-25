# ThemePatternGuide

## Installation

```bash
cd /path/to/theme/
git submodule add git@github.com:SimpleUpdates/ThemePatternGuide.git module/ThemePatternGuide/
```

Add the following line to `global.less`:

```Less
@import (optional) "../module/ThemePatternGuide/styleguide";
```

Register all your global color variables:

```Less
/* ~"color" explanation: https://github.com/less/less.js/issues/1595 */
@registeredColors:
  accentColor,
  accentColorBleached,
  accentColorLight,
  accentColorMid1,
  accentColorMid2,
  accentColorMid3,
  accentColorDim,
  accentColorDark,
  ~"white",
  ~"lightGray",
  ~"black";
```

Create `layout/styleguide.html`:

```Twig
{# Access this page at /admin/theme/view/layout/styleguide.html #}

{% set base = "module/ThemePatternGuide/styleguide-boilerplate.html" %}
{% extends base %}
{% import base as guide %}

{% block content %}
  {% embed "#{styleguideThemePath}/pattern.html" with { name: "Example" } %}
    {% block scenarios %}
      {% embed "dev/scenario.html" %}
        {% block scenario %}
          <p>First Scenario HTML</p>
        {% endblock %}
      {% endembed %}
      {% embed "dev/scenario.html" %}
        {% block scenario %}
          <p>Second Scenario HTML</p>
        {% endblock %}
      {% endembed %}
    {% endblock %}
  {% endembed %}
	
  {# Update to match the path of one of your patterns: #}
  {{ guide.patternInclude({ partial: "partial/atom-logo.html" }) }}
  
  {# More complex usage #}
  {{ guide.patternInclude({
    partial: "partial/molecule-hero.html",
    scenarios: {
      "Configured": {
        "pageTitle": "Page Title",
        "image": "https://unsplash.it/750/250"
      },
      "No Image": {
        "pageTitle": "Page Title",
        "image": null
      }
    },
    params: [ "pageTitle", "image" ]
  }) }}
{% endblock %}
```

Visit your styleguide at `/admin/theme/view/layout/styleguide.html`.
