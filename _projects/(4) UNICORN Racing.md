---
name: "2025 RoboRacer Autonomous Racing Competition"
year: 2025
permalink: /projects/unicorn-racing/
tools: [Autonomous Racing, Opponent Prediction, Trajectory Planning, Overtaking, ROS]
image: /assets/img/projects/unicorn-racing/team.jpg
description: Team UNICORN Racing's ICRA 2025 competition project, where I worked on GP-based opponent prediction and lane-based dynamic overtaking planning. The team finished 2nd overall.
demo_url: https://www.youtube.com/watch?v=Ukox0IPqGNA
demo_video_id: Ukox0IPqGNA
team_url: https://hmcl-unist.github.io/unicorn-racing/aboutus/
---

<div class="academic-page unicorn-project" markdown="1">

# 2025 RoboRacer Autonomous Racing Competition

<p class="unicorn-project-subtitle">Opponent Prediction and Dynamic Overtaking</p>
<p class="unicorn-project-meta">2025 · RoboRacer · Team UNICORN Racing</p>

I participated in the **2025 RoboRacer Autonomous Racing Competition** at ICRA as a member of **Team UNICORN Racing**, working on **opponent prediction and dynamic planning**. The team developed an autonomous racing stack that connected mapping, state estimation, opponent perception, overtaking, and vehicle control for physical head-to-head racing.

Our racing objectives prioritized avoiding contact with other vehicles and track boundaries while pursuing a low lap time. UNICORN Racing finished **2nd overall**, with a **1st-place combined time-trial result** and a **19.05-second fastest lap** in the fastest-lap trial.

<figure class="unicorn-project-figure">
  <img src="{{ '/assets/img/projects/unicorn-racing/team.jpg' | relative_url }}" alt="Team UNICORN Racing with its racing vehicles and second-place award at ICRA 2025 in Atlanta" width="1279" height="761" decoding="async">
  <figcaption>Team UNICORN Racing at ICRA 2025.</figcaption>
</figure>

## Highlights

<div class="unicorn-project-video">
  <iframe src="https://www.youtube-nocookie.com/embed/{{ page.demo_video_id | escape }}" title="UNICORN Racing 2025 race highlights" width="1280" height="720" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" allow="encrypted-media; picture-in-picture; fullscreen" allowfullscreen></iframe>
</div>

<div class="unicorn-project-links">
  <a class="btn academic-publication-link unicorn-project-link" href="{{ page.demo_url | escape }}" target="_blank" rel="noopener noreferrer" aria-label="Watch the UNICORN Racing highlights on YouTube (opens in a new tab)">
    <i class="fab fa-youtube" aria-hidden="true"></i> Watch Highlights
  </a>
  <a class="btn academic-publication-link unicorn-project-link" href="{{ page.team_url | escape }}" target="_blank" rel="noopener noreferrer" aria-label="Visit the UNICORN Racing team website (opens in a new tab)">
    <i class="fas fa-globe" aria-hidden="true"></i> Team Website
  </a>
</div>

## Racing Stack

The system connected offline race preparation with online estimation, perception, planning, and control. A map and optimized raceline provided the reference for driving, while vehicle-state estimates and opponent observations informed the next maneuver.

Online, LiDAR, IMU, and wheel-odometry observations supported state estimation. Opponent perception fed the planning stack, while a state machine selected the trajectory appropriate for the current racing situation. The controller translated that trajectory into commands for the VESC-driven vehicle.

<figure class="unicorn-project-figure">
  <img src="{{ '/assets/img/projects/unicorn-racing/architecture.jpg' | relative_url }}" alt="UNICORN Racing architecture connecting race preparation, state estimation, opponent perception, planning, and control" width="1600" height="691" loading="lazy" decoding="async">
  <figcaption>Full racing-stack architecture.</figcaption>
</figure>

## Hardware

The racing platform used a **Serpent SRX8 GTE '23 chassis**, an Intel ASUS NUC 14 Pro onboard computer, and a VESC 6 Mk VI HP motor controller. A Hokuyo UST-30LX LiDAR and MicroStrain 3DM-GX5-25-AHRS IMU provided the primary range and inertial measurements. The drivetrain paired a Hobbywing motor with STRADALE SP33 MEGA SOFT tires.

## Mapping and Raceline Optimization

**Cartographer** generated the map used for localization and raceline preparation. Track processing extracted a centerline and boundaries from the map, with skeletonization, contour extraction, and smoothing preparing the geometry for optimization.

The preparation pipeline supported shortest-path, minimum-curvature, and minimum-time optimization. The resulting raceline and velocity profile served as the global reference for normal driving and for rejoining after an avoidance maneuver.

## State Estimation

The team's localization work addressed degraded Cartographer performance on high-speed straights. Cartographer was modified to use wheel-odometry information without passing the unreliable wheel-odometry constraint into pose-graph optimization.

**Adaptive wheel odometry** adjusted the wheel-speed conversion to account for slip during acceleration and braking. An EKF combined the state-estimation inputs to provide the vehicle state used by planning and control.

## Perception and Opponent Prediction

LiDAR detection used an adaptive breakpoint detector and two-stage clustering to group points and merge fragmented observations of an opponent. Tracking connected those observations over time.

The **Gaussian Process opponent predictor** learned the opponent's driving line and longitudinal speed in Frenet coordinates. Its mean trajectory and uncertainty supported future obstacle prediction for the planner. As observations accumulated, the learned trajectory covered more of the lap, while return-to-line prediction handled departures from the established driving line.

## Planning and Race-State Coordination

Separate planners handled the start, recovery toward the raceline, static-obstacle avoidance, and dynamic overtaking. The **lane-based dynamic planner** selected a passing side using available clearance, generated a smooth transition onto a neighboring reference lane, and returned toward the optimized raceline after passing the opponent.

Prediction validity, available space, and track boundaries determined whether an avoidance path could be used. Direction hysteresis reduced rapid side changes, while the state machine coordinated global tracking, recovery, overtaking, trailing, attack, start, and follow-the-gap behaviors. Overtaking-sector rules and path-validity checks connected the selected maneuver to the race situation.

<figure class="unicorn-project-figure">
  <img src="{{ '/assets/img/projects/unicorn-racing/dynamic-planner.jpg' | relative_url }}" alt="Lane-based dynamic avoidance diagram showing left and right passing references, an opponent vehicle, and a convergence point" width="1400" height="511" loading="lazy" decoding="async">
  <figcaption>Lane-based overtaking around a moving opponent and rejoining the raceline.</figcaption>
</figure>

<figure class="unicorn-project-figure unicorn-project-state-machine">
  <img src="{{ '/assets/img/projects/unicorn-racing/state-machine.jpg' | relative_url }}" alt="Racing state machine and its associated optimized, recovery, static-avoidance, dynamic-avoidance, and start trajectories" width="1000" height="871" loading="lazy" decoding="async">
  <figcaption>Racing states and the available trajectory types.</figcaption>
</figure>

## Control

The control stack compensated for localization and actuation delays when selecting forward speed targets. Trailing used a PD-based adaptive cruise-control rule, while lateral control used a modified pure-pursuit approach with lookahead adapted to speed and estimated lateral acceleration. Additional steering correction supported curved-path tracking.

## Competition Results

<dl class="unicorn-project-facts">
  <div><dt>Overall result</dt><dd>2nd place</dd></div>
  <div><dt>Combined time trial</dt><dd>1st place · 35 points</dd></div>
  <div><dt>Fastest-lap trial</dt><dd>1st place · 19.05 seconds</dd></div>
  <div><dt>Consecutive-lap trial</dt><dd>2nd place · 29 laps</dd></div>
</dl>

<figure class="unicorn-project-figure">
  <img src="{{ '/assets/img/projects/unicorn-racing/time-trial-results.jpg' | relative_url }}" alt="Competition tables showing UNICORN Racing's 29 consecutive laps, 19.05-second fastest lap, and first-place combined time-trial score" width="1800" height="718" loading="lazy" decoding="async">
  <figcaption>Consecutive-lap, fastest-lap, and combined time-trial results.</figcaption>
</figure>

## Contribution

I worked on **GP-based opponent prediction and the lane-based dynamic planner**, connecting learned opponent trajectories to passing-path generation and integration with the team's racing state machine.

</div>

{% include academic-page-styles.html %}

<style>
  .unicorn-project > h1 {
    margin: 0 0 0.65rem;
    font-size: 2.1rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .unicorn-project-subtitle {
    margin: 0 0 0.35rem;
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.5;
  }

  .unicorn-project-meta {
    margin: 0 0 1.5rem;
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .unicorn-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .unicorn-project-video {
    position: relative;
    aspect-ratio: 16 / 9;
    margin: 1.5rem 0;
    overflow: hidden;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #000;
  }

  .unicorn-project-video > iframe {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    border: 0;
  }

  .unicorn-project-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.65rem;
    margin: 1rem 0 1.5rem;
  }

  .unicorn-project-link {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    font-size: 0.85rem;
  }

  .unicorn-project-facts {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    column-gap: 1.25rem;
    margin: 1.5rem 0;
    border-top: 1px solid var(--academic-border);
  }

  .unicorn-project-facts > div {
    min-width: 0;
    padding: 0.85rem 0;
    border-bottom: 1px solid var(--academic-border);
  }

  .unicorn-project-facts dt {
    margin-bottom: 0.25rem;
    font-size: 0.85rem;
    font-weight: 600;
  }

  .unicorn-project-facts dd {
    margin: 0;
    color: var(--academic-muted);
    overflow-wrap: anywhere;
  }

  .unicorn-project-figure {
    min-width: 0;
    margin: 1.5rem 0;
  }

  .unicorn-project .unicorn-project-figure > img {
    display: block;
    width: 100%;
    max-width: 100%;
    height: auto;
    margin: 0;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #fff;
  }

  .unicorn-project-figure > figcaption {
    margin-top: 0.5rem;
    color: var(--academic-muted);
    font-size: 0.8rem;
    line-height: 1.65;
  }

  .unicorn-project .unicorn-project-state-machine > img {
    max-width: 32rem;
    margin-inline: auto;
  }

  @media (max-width: 767.98px) {
    .unicorn-project-facts {
      grid-template-columns: minmax(0, 1fr);
    }
  }
</style>
