---
layout: post
title:  "Display time-based content using Liquid"
tags: [jekyll, liquid]
---

{% raw %}
```javascript
{% capture now %}{{ site.time | date: '%s' }}{% endcapture %}
{% capture postdate %}{{ post.date | date: '%s' }}{% endcapture %}
```
{% endraw %}