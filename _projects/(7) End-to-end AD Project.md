---
name: "End-to-end AD Project"
year: 2026
permalink: /projects/end-to-end-ad/
tools: [End-to-End Driving, Imitation Learning, Reinforcement Learning, Curriculum Learning, Sim-to-Real]
image: /assets/img/projects/end-to-end-ad/simulation-preview.jpg
description: Team UNICORN's simulation-centered autonomous racing research, where I work on policy pre-training and post-training, reinforcement learning, and context-aware methods.
---

<div class="academic-page e2e-project" markdown="1">

# End-to-end AD Project

<p class="e2e-project-subtitle">Simulation-Based End-to-End Autonomous Racing</p>
<p class="e2e-project-meta">2026 · UNIST · Team UNICORN</p>

This project develops an **end-to-end autonomous racing policy** through simulation-based learning and Sim-to-Real validation. The research connects a lightweight multimodal perception backbone, expert-policy imitation, reinforcement-learning fine-tuning, and context-aware policy design.

My work covers **policy pre-training and post-training, reinforcement learning, and context-aware methods**. The project builds on initial BEV-based behavior-cloning experiments and simulation-to-vehicle test environments, while extending the learning pipeline and system design toward more demanding racing behavior. Higher control rates, improved lap times, and reliable transfer remain research objectives.

## End-to-End Architecture

The architecture combines front-camera images and 3D LiDAR observations in a **bird's-eye-view (BEV) representation**. Camera and LiDAR encoders feed a fused BEV backbone, with auxiliary tasks for map segmentation, object detection, and relative-pose estimation.

Buffered BEV features are combined with encoded ego-vehicle state and temporal information. A transformer block produces a latent representation, and a multi-head decoder outputs steering-angle and velocity profiles. The backbone design considers racing-specific regions of interest and the sensing configuration available on the platform.

<figure class="e2e-project-figure">
  <img src="{{ '/assets/img/projects/end-to-end-ad/architecture.jpg' | relative_url }}" alt="End-to-end racing architecture fusing camera and LiDAR BEV features with ego state before decoding steering and velocity profiles" width="1700" height="843" decoding="async">
  <figcaption>Multimodal BEV encoding, temporal state representation, and policy decoding.</figcaption>
</figure>

## Policy Pre-Training

The initial policy is trained through **imitation learning from an MPC-based racing expert**. The expert combines track-progress objectives with collision-avoidance constraints informed by predicted opponent motion and uncertainty, providing structured driving demonstrations.

The pre-training design aligns sensor-derived latent features with expert information through a negative log-likelihood objective. The multi-head decoder produces steering and velocity action distributions, establishing a policy that can subsequently be refined through interaction with the environment.

<figure class="e2e-project-figure e2e-project-pretraining">
  <img src="{{ '/assets/img/projects/end-to-end-ad/policy-pretraining.jpg' | relative_url }}" alt="Policy pre-training pipeline connecting sensor observations and expert driving data to a latent representation and steering and velocity action distributions" width="1000" height="888" loading="lazy" decoding="async">
  <figcaption>Expert-guided policy initialization through imitation learning.</figcaption>
</figure>

<figure class="e2e-project-figure">
  <img src="{{ '/assets/img/projects/end-to-end-ad/imitation-learning-track.png' | relative_url }}" alt="Gazebo training track alongside a plot of its boundaries, centerline reference, and driving direction" width="1734" height="572" loading="lazy" decoding="async">
  <figcaption>Gazebo training track and centerline reference.</figcaption>
</figure>

The following clips show trajectory visualizations from the imitation-learning experiments.

<div class="e2e-project-gallery">
<figure class="e2e-project-figure">
  <video controls playsinline preload="none" poster="{{ '/assets/img/projects/end-to-end-ad/imitation-learning-2-poster.jpg' | relative_url }}" width="1920" height="1080" aria-label="Imitation-learning trajectory visualization 1">
    <source src="{{ '/assets/videos/projects/end-to-end-ad/imitation-learning-2.mp4' | relative_url }}" type="video/mp4">
    Your browser does not support embedded video. <a href="{{ '/assets/videos/projects/end-to-end-ad/imitation-learning-2.mp4' | relative_url }}">Watch imitation-learning example 1</a>.
  </video>
  <figcaption>Imitation-learning trajectory visualization 1.</figcaption>
</figure>

<figure class="e2e-project-figure">
  <video controls playsinline preload="none" poster="{{ '/assets/img/projects/end-to-end-ad/imitation-learning-3-poster.jpg' | relative_url }}" width="1920" height="1080" aria-label="Imitation-learning trajectory visualization 2">
    <source src="{{ '/assets/videos/projects/end-to-end-ad/imitation-learning-3.mp4' | relative_url }}" type="video/mp4">
    Your browser does not support embedded video. <a href="{{ '/assets/videos/projects/end-to-end-ad/imitation-learning-3.mp4' | relative_url }}">Watch imitation-learning example 2</a>.
  </video>
  <figcaption>Imitation-learning trajectory visualization 2.</figcaption>
</figure>
</div>

## Policy Post-Training and Curriculum

Post-training refines the initialized policy using **Proximal Policy Optimization (PPO)** and parallel simulation rollouts. Steering and velocity use separate action distributions, while expert-data updates remain alongside reinforcement-learning updates to limit drift from the demonstrated policy.

The reward design combines collision and overtaking outcomes with denser signals for track progress, progress relative to an opponent, and smooth steering and acceleration changes. These signals support learning throughout a rollout rather than relying only on occasional terminal events.

<figure class="e2e-project-figure">
  <img src="{{ '/assets/img/projects/end-to-end-ad/policy-posttraining.jpg' | relative_url }}" alt="Parallel simulation workers collecting rollout data for combined imitation-learning and reinforcement-learning policy updates" width="1700" height="350" loading="lazy" decoding="async">
  <figcaption>Parallel rollout collection and combined imitation/RL policy updates.</figcaption>
</figure>

The **curriculum** introduces racing objectives in stages: first maximizing progress around a track, then learning overtaking through relative progress, and finally incorporating close-interaction collision penalties. This staged design aims to reduce unnecessary early exploration before adding more demanding interactions.

<figure class="e2e-project-figure">
  <img src="{{ '/assets/img/projects/end-to-end-ad/curriculum.jpg' | relative_url }}" alt="Three-stage racing curriculum progressing from minimum-lap-time driving to overtaking and collision-aware racing" width="1700" height="574" loading="lazy" decoding="async">
  <figcaption>Curriculum progression from solo racing to overtaking and collision-aware interaction.</figcaption>
</figure>

The rollout sequence below shows Gazebo racing behavior at different training iterations for overtaking and collision-aware settings.

<figure class="e2e-project-figure">
  <video controls loop playsinline preload="none" poster="{{ '/assets/img/projects/end-to-end-ad/gazebo-rl-poster.jpg' | relative_url }}" width="1298" height="838" aria-label="Gazebo reinforcement-learning results across training iterations">
    <source src="{{ '/assets/videos/projects/end-to-end-ad/gazebo-rl-results.mp4' | relative_url }}" type="video/mp4">
    Your browser does not support embedded video. <a href="{{ '/assets/videos/projects/end-to-end-ad/gazebo-rl-results.mp4' | relative_url }}">Watch the Gazebo RL results</a>.
  </video>
  <figcaption>Gazebo RL rollouts across training iterations: overtaking and collision-aware racing.</figcaption>
</figure>

## Context-Aware Policy Design

The situation-awareness work explores **latent context inference** for changing driving conditions. Context factors of interest include road friction, opponent-speed scale, steering aggressiveness, and track-segment type. The aim is to help the policy interpret the current situation beyond an isolated raw-sensor observation.

The design also considers a validity mask so that context is used when it contributes meaningfully to the dynamics. This reduces unnecessary dependence on context and supports studying generalization under unfamiliar conditions.

## Simulation and Sim-to-Real

The development loop connects simulation, driving data, and vehicle tests. Parallel environments support learning, while system identification and real-data-based dynamics tuning address differences between simulated and physical behavior.

The Sim-to-Real strategy includes domain randomization, sensor-noise injection, asynchronous sensor handling, and targeted use of real driving data. Scenario generation and closed-loop testing are part of the broader validation design, including interactions such as merging, cut-ins, and sudden braking.

<figure class="e2e-project-figure">
  <img src="{{ '/assets/img/projects/end-to-end-ad/sim-to-real.jpg' | relative_url }}" alt="Simulation-centered development loop linking real driving data, scenario generation, simulation, adversarial scenario optimization, and Sim-to-Real evaluation" width="1700" height="704" loading="lazy" decoding="async">
  <figcaption>Simulation, data collection, scenario generation, and Sim-to-Real evaluation loop.</figcaption>
</figure>

## Reliability and Runtime Design

The wider system design explores uncertainty-based policy gating, conservative fallback behavior, and physics-informed stability and collision-risk assessment. Training and deployment optimization directions include mixed precision, distributed learning, model compilation, quantization, TensorRT, and reducing communication overhead. These are development strategies to evaluate alongside driving performance.

## Contribution

I work on **policy pre-training and post-training, reinforcement learning, and context-aware methods**. My focus connects expert-guided initialization with rollout-based policy improvement, reward and curriculum design, and situation-aware policy representations for autonomous racing.

</div>

{% include academic-page-styles.html %}

<style>
  .e2e-project > h1 {
    margin: 0 0 0.65rem;
    font-size: 2.1rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .e2e-project-subtitle {
    margin: 0 0 0.35rem;
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.5;
  }

  .e2e-project-meta {
    margin: 0 0 1.5rem;
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .e2e-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .e2e-project-figure {
    min-width: 0;
    margin: 1.5rem 0;
  }

  .e2e-project-gallery {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1.25rem;
    margin: 1.5rem 0;
  }

  .e2e-project-gallery > .e2e-project-figure {
    margin: 0;
  }

  .e2e-project .e2e-project-figure > img,
  .e2e-project .e2e-project-figure > video {
    display: block;
    width: 100%;
    max-width: 100%;
    height: auto;
    margin: 0;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #fff;
  }

  .e2e-project .e2e-project-pretraining > img {
    max-width: 32rem;
    margin-inline: auto;
  }

  .e2e-project-figure > figcaption {
    margin-top: 0.5rem;
    color: var(--academic-muted);
    font-size: 0.8rem;
    line-height: 1.65;
  }

  @media (max-width: 767.98px) {
    .e2e-project-gallery {
      grid-template-columns: minmax(0, 1fr);
    }
  }
</style>
