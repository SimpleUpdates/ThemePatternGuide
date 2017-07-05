# ThemePatternGuide

## Installation

```bash
cd /path/to/theme/
git submodule add git@github.com:SimpleUpdates/ThemePatternGuide.git dev/
```

Add the following line to `global.less`:

```Less
@import "../dev/styleguide";
```

Register all your global color variables:

```Less
/* ~"color" explanation: https://github.com/less/less.js/issues/1595 */
.registerColors(
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
  ~"black"
);
```

Create `layout/styleguide.html`:

```Twig
{# Access this page at /admin/theme/view/layout/styleguide.html #}

{% extends "dev/styleguide-boilerplate.html" %}

{% block content %}
  {% embed "dev/pattern.html" with { name: "Colors" } %}
    {% block scenarios %}
      {% embed "dev/scenario.html" %}
        {% block scenario %}
          <div class="colors">
            {% for i in 0..20 %}<i></i>{% endfor %}
          </div>
        {% endblock %}
      {% endembed %}
    {% endblock %}
  {% endembed %}
	
  {# Update to match the path of one of your patterns: #}
  {% include "dev/pattern-include.html" with { partial: "partial/atom-logo.html" } %}
{% endblock %}
```

Visit your styleguide at `/admin/theme/view/layout/styleguide.html`.
