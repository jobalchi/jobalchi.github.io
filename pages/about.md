---
layout: page
title: About
permalink: /about/
weight: 1
---

<div class="about-intro">
  <div class="about-intro-copy">
    <h1><strong>About Me</strong></h1>
    <p>
      Hi I am <strong>{{ site.author.name }}</strong> :wave:,<br>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    </p>
  </div>
  <img
    class="about-profile-image"
    src="{{ site.author.image | relative_url }}"
    alt="{{ site.author.name }} profile photo"
  >
</div>

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
  .about-intro {
    display: flex;
    align-items: center;
    gap: 2rem;
    margin-bottom: 1.5rem;
  }

  .about-intro-copy {
    flex: 1;
    min-width: 0;
  }

  .about-profile-image {
    width: 190px;
    height: 190px;
    flex: 0 0 190px;
    border-radius: 50%;
    object-fit: cover;
    object-position: center;
    box-shadow: 0 0.5rem 1.25rem rgba(0, 0, 0, 0.15);
  }

  @media (max-width: 575.98px) {
    .about-intro {
      flex-direction: column;
      align-items: flex-start;
      gap: 1.25rem;
    }

    .about-profile-image {
      order: -1;
      align-self: center;
      width: 160px;
      height: 160px;
      flex-basis: 160px;
    }
  }

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
