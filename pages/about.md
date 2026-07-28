---
layout: page
title: About
permalink: /about/
weight: 1
---

# **About Me**

Hi I am **{{ site.author.name }}** :wave:,<br>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.

<div class="row">
  <div class="col-lg">
    {% include about/skills.html title="Programming Skills" source=site.data.programming-skills %}
    {% include about/skills.html title="Other Skills" source=site.data.other-skills %}
  </div>
  <div class="col-lg">
    {% include about/skills.html title="Languages" source=site.data.language-skills %}
  </div>
</div>

<div class="row">
{% include about/timeline.html title="Society" source=site.data.society variant="society" %}
</div>

<div class="row">
{% include about/timeline.html title="Experience" source=site.data.experience variant="experience" %}
</div>

<div class="row">
{% include about/timeline.html title="Education" source=site.data.timeline variant="education" %}
</div>

<style>
  .timeline-section-education > h2 {
    color: #007bff;
  }

  .timeline-section-experience > h2 {
    color: #fd7e14;
  }

  .timeline-section-experience .timeline-body::after {
    background-color: #fd7e14;
  }

  .timeline-section-experience .timeline-item::after {
    border-color: #fd7e14;
  }

  .timeline-section-society > h2 {
    color: #28a745;
  }

  .timeline-section-society .timeline-body::after {
    background-color: #28a745;
  }

  .timeline-section-society .timeline-item::after {
    border-color: #28a745;
  }
</style>
