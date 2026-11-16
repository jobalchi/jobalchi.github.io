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
      <a class="about-social-link about-social-link-cv" href="{{ '/assets/files/Seongjun_Lee_CV.pdf' | relative_url }}" target="_blank" rel="noopener" aria-label="Curriculum Vitae" title="CV">
        <i class="fas fa-file-pdf" aria-hidden="true"></i>
        <span>CV</span>
      </a>
    </div>
    <div class="about-interest-tags" aria-label="Research interests">
      <span class="about-interest-tag"># Decision-Making</span>
      <span class="about-interest-tag"># Uncertainty-Aware</span>
      <span class="about-interest-tag"># Optimal Policy</span>
      <span class="about-interest-tag"># Autonomous Systems</span>
      <span class="about-interest-tag"># Reinforcement Learning</span>
    </div>
    {% include about/skill-icons.html %}
  </div>
  <img
    class="about-profile-image"
    src="{{ site.author.image | relative_url }}"
    alt="{{ site.author.name }} profile photo"
  >
</div>

<div class="about-history">
{% include about/society.html %}

{% include about/experience.html %}

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
    font-size: 0.9rem;
  }

  .about-intro-copy > h1 {
    font-size: 2.1rem;
  }

  .about-skill-icons {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem 1.1rem;
    margin: 1rem 0 0;
    padding: 0;
    list-style: none;
  }

  .about-skill-icon {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.35rem;
    min-width: 3rem;
    color: #626c67;
    font-size: 0.7rem;
    font-weight: 600;
    line-height: 1.4;
  }

  .about-skill-icon > i {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 2.4rem;
    height: 2.4rem;
    color: var(--skill-color);
    font-size: 1.8rem;
  }

  .about-skill-icon-python {
    --skill-color: #3776ab;
    --skill-dark-color: #7ab8e6;
  }

  .about-skill-icon-cpp {
    --skill-color: #00599c;
    --skill-dark-color: #79b8f1;
  }

  .about-skill-icon-pytorch {
    --skill-color: #ee4c2c;
    --skill-dark-color: #ff8066;
  }

  .about-skill-icon-ros {
    --skill-color: #22314e;
    --skill-dark-color: #b4c8e8;
  }

  .about-skill-icon-docker {
    --skill-color: #2496ed;
    --skill-dark-color: #54b7ff;
  }

  .about-skill-icon-git {
    --skill-color: #f05032;
    --skill-dark-color: #ff8c75;
  }

  [data-theme="dark"] .about-skill-icon {
    color: #b5bdb9;
  }

  [data-theme="dark"] .about-skill-icon > i {
    color: var(--skill-dark-color, var(--skill-color));
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
    font-size: 0.9rem;
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

  .about-social-link-cv,
  .about-social-link-cv:hover {
    color: #6f42c1;
  }

  [data-theme="dark"] .about-social-link-github,
  [data-theme="dark"] .about-social-link-github:hover {
    color: #f5f5f5;
  }

  .about-interest-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-top: 1.25rem;
  }

  .about-interest-tag {
    padding: 0.3rem 0.7rem;
    color: #007bff;
    background-color: rgba(0, 123, 255, 0.1);
    border: 1px solid rgba(0, 123, 255, 0.25);
    border-radius: 999px;
    font-size: 0.78rem;
    font-weight: 600;
    line-height: 1.4;
  }

  .about-profile-image {
    width: 190px;
    height: auto;
    flex: 0 0 190px;
    border-radius: 0;
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
      flex-basis: auto;
    }
  }

  .about-history {
    --history-muted: #626c67;
    --history-border: #d9dfdc;
    margin-top: 2.5rem;
  }

  .about-history-section + .about-history-section {
    margin-top: 3rem;
  }

  .about-history-section > h2 {
    margin: 0 0 1.25rem;
    font-size: 1.4rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .about-history-list {
    margin: 0;
    padding: 0;
    border-top: 1px solid var(--history-border);
    list-style: none;
  }

  .about-history-item {
    display: grid;
    grid-template-columns: 11rem minmax(0, 1fr);
    gap: 1.5rem;
    padding: 1.5rem 0;
    border-bottom: 1px solid var(--history-border);
  }

  .about-history-date {
    margin: 0;
    color: var(--history-muted);
    font-size: 0.85rem;
    font-weight: 600;
    line-height: 1.65;
    font-variant-numeric: tabular-nums;
  }

  .about-history-content {
    min-width: 0;
    overflow-wrap: anywhere;
  }

  .about-history-content > h3 {
    margin: 0 0 0.4rem;
    font-size: 1rem;
    font-weight: 700;
    line-height: 1.4;
  }

  .about-history-subtitle {
    margin: 0;
    color: var(--history-muted);
    font-size: 0.9rem;
    font-weight: 600;
    line-height: 1.65;
  }

  .about-history-details {
    margin: 0.85rem 0 0;
    color: var(--history-muted);
    font-size: 0.9rem;
    line-height: 1.75;
  }

  .about-history-detail {
    display: grid;
    grid-template-columns: 4rem minmax(0, 1fr);
    gap: 0.75rem;
    padding: 0.2rem 0;
  }

  .about-history-detail > dt {
    margin: 0;
    font-size: 0.85rem;
    font-weight: 600;
  }

  .about-history-detail > dd {
    min-width: 0;
    margin: 0;
  }

  .about-history-detail-link {
    color: inherit;
    text-decoration: underline;
    text-underline-offset: 0.18em;
  }

  .about-history-detail-link:hover {
    color: inherit;
    text-decoration-thickness: 2px;
  }

  .about-history-detail-link > i {
    margin-left: 0.2rem;
    font-size: 0.75em;
  }

  .about-history-translation {
    display: block;
    margin-top: 0.35rem;
    font-size: 0.85rem;
  }

  .about-experience-group {
    padding: 1.5rem 0;
    border-bottom: 1px solid var(--history-border);
  }

  .about-experience-role {
    margin: 0 0 0.75rem;
    font-size: 1rem;
    font-weight: 700;
    line-height: 1.5;
  }

  .about-experience-entries {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  .about-experience-entries > .about-history-item {
    padding: 0.6rem 0;
    border: 0;
  }

  .about-experience-organization {
    margin: 0;
    font-size: 0.95rem;
    font-weight: 500;
    line-height: 1.5;
  }

  .about-society-group {
    padding: 1.5rem 0;
    border-bottom: 1px solid var(--history-border);
  }

  .about-society-heading {
    display: flex;
    flex-wrap: wrap;
    align-items: baseline;
    gap: 0.35rem 1rem;
  }

  .about-society-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.85rem;
  }

  .about-society-link {
    display: inline-flex;
    align-items: baseline;
    gap: 0.3rem;
    color: var(--society-link-color, var(--history-muted));
    font-size: 0.8rem;
    line-height: 1.6;
    text-decoration: none;
    text-underline-offset: 0.18em;
  }

  .about-society-link:hover {
    color: var(--society-link-color, var(--history-muted));
    text-decoration: underline;
  }

  .about-society-link-naver {
    --society-link-color: #00843a;
  }

  .about-society-link-instagram {
    --society-link-color: #c13584;
  }

  [data-theme="dark"] .about-society-link-naver {
    --society-link-color: #03c75a;
  }

  [data-theme="dark"] .about-society-link-instagram {
    --society-link-color: #f27bb6;
  }

  .about-society-link:focus-visible {
    outline: 2px solid currentColor;
    outline-offset: 3px;
  }

  .about-society-name {
    margin: 0;
    font-size: 1rem;
    font-weight: 700;
    line-height: 1.5;
    overflow-wrap: anywhere;
  }

  .about-society-team {
    margin: 0.25rem 0 0;
    color: var(--history-muted);
    font-size: 0.9rem;
    line-height: 1.65;
  }

  .about-society-roles {
    margin: 0.75rem 0 0;
    padding: 0;
    list-style: none;
  }

  .about-society-roles > .about-history-item {
    align-items: baseline;
    padding: 0.4rem 0;
    border: 0;
  }

  .about-society-role {
    min-width: 0;
    margin: 0;
    font-size: 0.95rem;
    font-weight: 600;
    line-height: 1.5;
    overflow-wrap: anywhere;
  }

  [data-theme="dark"] .about-history {
    --history-muted: #b5bdb9;
    --history-border: #3d4541;
  }

  @media (max-width: 575.98px) {
    .about-history-item {
      grid-template-columns: minmax(0, 1fr);
      gap: 0.4rem;
      padding: 1.25rem 0;
    }

    .about-history-section + .about-history-section {
      margin-top: 2.25rem;
    }
  }
</style>
