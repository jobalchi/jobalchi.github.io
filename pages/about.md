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
      I am interested in <strong>decision-making under uncertainty</strong> and <strong>optimal policy design</strong> for autonomous driving systems.<br>
      If you are interested in my work, please feel free to reach out.
    </p>
    <div class="about-social-links" aria-label="Contact links">
      <a class="about-social-link about-social-link-email" href="mailto:{{ site.author.email }}" aria-label="Email" title="Email">
        <i class="fas fa-envelope" aria-hidden="true"></i>
        <span>Mail</span>
      </a>
      <a class="about-social-link about-social-link-github" href="https://github.com/{{ site.author.github }}" aria-label="GitHub" title="GitHub">
        <i class="fab fa-github" aria-hidden="true"></i>
        <span>GitHub</span>
      </a>
      <a class="about-social-link about-social-link-linkedin" href="https://www.linkedin.com/in/{{ site.author.linkedin }}" aria-label="LinkedIn" title="LinkedIn">
        <i class="fab fa-linkedin-in" aria-hidden="true"></i>
        <span>LinkedIn</span>
      </a>
    </div>
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

  .about-social-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem 1.25rem;
    margin-top: 1rem;
  }

  .about-social-link {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    color: #6c757d;
    font-size: 1rem;
    font-weight: 500;
    text-decoration: none !important;
    transition: color 0.2s ease, transform 0.2s ease;
  }

  .about-social-link:hover {
    transform: translateY(-2px);
    opacity: 0.8;
  }

  .about-social-link-email,
  .about-social-link-email:hover {
    color: #db4437;
  }

  .about-social-link-github,
  .about-social-link-github:hover {
    color: #333;
  }

  .about-social-link-linkedin,
  .about-social-link-linkedin:hover {
    color: #0077b5;
  }

  [data-theme="dark"] .about-social-link-github,
  [data-theme="dark"] .about-social-link-github:hover {
    color: #f5f5f5;
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
