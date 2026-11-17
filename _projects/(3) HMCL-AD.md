---
name: "HMCL-AD: GP Prediction and MPC Overtaking"
year: 2025
permalink: /projects/hmcl-ad/
tools: [ROS 2, PyTorch, GPyTorch, MPC, FORCESPRO]
image: /assets/img/projects/hmcl-ad/demo-poster.jpg
description: An undergraduate research project I led on Gaussian-process opponent prediction and MPC-based overtaking in 1/10-scale autonomous racing.
demo_video: /assets/videos/projects/hmcl-ad/demonstration.mp4
demo_poster: /assets/img/projects/hmcl-ad/demo-poster.jpg
demo_url: https://www.youtube.com/watch?v=tR-cWtZaJP8
demo_video_id: tR-cWtZaJP8
---

<div class="academic-page hmcl-project" markdown="1">

# HMCL-AD

<p class="hmcl-project-subtitle">Gaussian-Process Prediction and MPC-Based Overtaking</p>
<p class="hmcl-project-meta">2024–2025 · BTS Research Program · Team HMCL-AD</p>

I led HMCL-AD and mentored two undergraduate researchers on opponent-motion prediction and overtaking in 1/10-scale autonomous racing. The project combined a Gaussian Process Regression (GPR) predictor with a Model Predictive Control (MPC) controller, connecting learned motion forecasts and their uncertainty to the ego vehicle's overtaking decisions. The GP-based opponent prediction approach draws on Zhu et al. [\[1\]](#reference-1).

The research progressed from ROS and simulation setup to data collection, GP training, and head-to-head testing with physical vehicles.

## Demonstration

<div class="hmcl-project-video">
  <video controls playsinline preload="none" poster="{{ page.demo_poster | relative_url }}" width="1280" height="720" aria-label="HMCL-AD autonomous racing research demonstration">
    <source src="{{ page.demo_video | relative_url }}" type="video/mp4">
    Your browser does not support embedded video. <a href="{{ page.demo_video | relative_url }}">Download the demonstration video</a>.
  </video>
</div>

<div class="hmcl-project-video">
  <iframe src="https://www.youtube-nocookie.com/embed/{{ page.demo_video_id | escape }}" title="HMCL-AD YouTube demonstration" width="1280" height="720" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" allow="encrypted-media; picture-in-picture; fullscreen" allowfullscreen></iframe>
</div>

<div class="hmcl-project-links">
  <a class="btn academic-publication-link hmcl-project-link" href="{{ page.demo_url | escape }}" target="_blank" rel="noopener noreferrer" aria-label="Watch the HMCL-AD demonstration on YouTube (opens in a new tab)">
    <i class="fab fa-youtube" aria-hidden="true"></i> Watch Demo
  </a>
</div>

## Prediction and Control Framework

The framework separates track generation, race recording, predictor training, online prediction, and vehicle control. F1TENTH Gym and the physical racing platforms provide vehicle states and sensor observations, while the control modules return steering and acceleration commands.

The system architecture uses ROS 2 for integration, PyTorch and GPyTorch for the learning pipeline, and FORCESPRO for the model predictive contouring control (MPCC) modules. This modular organization supports changing predictors and comparing behavior across racing scenarios.

<dl class="hmcl-project-facts">
  <div><dt>Experiment platform</dt><dd>Two 1/10-scale vehicles in head-to-head racing</dd></div>
  <div><dt>Prediction model</dt><dd>Gaussian Process Regression with forecast uncertainty</dd></div>
  <div><dt>Forecast grid</dt><dd>12 prediction steps at 0.1-second intervals</dd></div>
  <div><dt>Control</dt><dd>MPC/MPCC using opponent forecasts, uncertainty, and vehicle geometry</dd></div>
</dl>

<figure class="hmcl-project-figure">
  <img src="{{ '/assets/img/projects/hmcl-ad/architecture.jpg' | relative_url }}" alt="HMCL-AD architecture linking simulation and physical vehicles to track generation, race recording, GP training, prediction, and MPCC control" width="1280" height="720" loading="lazy" decoding="async">
  <figcaption>Modular prediction, learning, and control architecture.</figcaption>
</figure>

## Learning Opponent Motion

Randomized racing scenarios were used to record ego- and opponent-vehicle motion, including time, position, velocity, and acceleration. The experiments compared constant-velocity, MPC-based, and GP prediction approaches.

The work began with a pretrained GP predictor and then collected project-specific racing data for training and model updates in GPyTorch. Experiments under different track conditions motivated updating the dataset and examining prediction uncertainty in vehicle interactions.

The GP predictor supplies a motion forecast together with uncertainty over the prediction horizon. That uncertainty is important when the opponent's response is less well represented by the training data.

## MPC-Based Overtaking

The ego controller uses the opponent's predicted trajectory, forecast uncertainty, and vehicle footprint to formulate collision-avoidance constraints while planning its own motion. As the race progresses, updated state observations and opponent forecasts feed the next control decision.

GPU acceleration and the solver-based control pipeline were used to support simulation and on-board execution. Evaluation included physical head-to-head driving as well as simulated racing scenarios.

## Experiments and Team Activities

The team established simulation, training, and indoor physical-test environments and prepared a head-to-head prediction-and-overtaking demonstration for the RiTA 2024 lab tour.

The team also participated in the **3rd F1TENTH Korea Championship**, placing **1st in qualifying and 3rd overall**. These activities gave the undergraduate researchers experience with vehicle preparation, experimental analysis, and the practical uncertainty of physical racing.

<div class="hmcl-project-gallery">
  <figure class="hmcl-project-figure">
    <img src="{{ '/assets/img/projects/hmcl-ad/indoor-track.jpg' | relative_url }}" alt="Two small autonomous racing vehicles on the indoor HMCL test track" width="606" height="354" loading="lazy" decoding="async">
    <figcaption>Indoor track used for physical head-to-head experiments.</figcaption>
  </figure>
  <figure class="hmcl-project-figure">
    <img src="{{ '/assets/img/projects/hmcl-ad/competition.jpg' | relative_url }}" alt="HMCL-AD team members preparing vehicles at the 3rd F1TENTH Korea Championship" width="1280" height="720" loading="lazy" decoding="async">
    <figcaption>Vehicle preparation at the F1TENTH Korea Championship.</figcaption>
  </figure>
</div>

## Contribution

As **team lead and undergraduate research mentor**, I guided two undergraduate researchers through the development and integration of GP-based opponent prediction and MPC-based overtaking. My role included supporting their ROS and simulation setup, guiding model-training and control experiments, and coordinating analysis across simulated and physical racing environments.

## References

<p id="reference-1">[1] ZHU, Edward L., et al. <a href="https://doi.org/10.1109/IROS55552.2023.10341566">A Gaussian process model for opponent prediction in autonomous racing.</a> In: <em>2023 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)</em>. IEEE, 2023. p. 8186–8191.</p>

</div>

{% include academic-page-styles.html %}

<style>
  .hmcl-project > h1 {
    margin: 0 0 0.65rem;
    font-size: 2.1rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .hmcl-project-subtitle {
    margin: 0 0 0.35rem;
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.5;
  }

  .hmcl-project-meta {
    margin: 0 0 1.5rem;
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .hmcl-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .hmcl-project-video {
    margin: 1.5rem 0;
  }

  .hmcl-project-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.65rem;
    margin: 1rem 0 1.5rem;
  }

  .hmcl-project-link {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    font-size: 0.85rem;
  }

  .hmcl-project-video > video,
  .hmcl-project-video > iframe {
    display: block;
    width: 100%;
    height: auto;
    aspect-ratio: 16 / 9;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #000;
  }

  .hmcl-project-facts,
  .hmcl-project-gallery {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1.25rem;
    margin: 1.5rem 0;
  }

  .hmcl-project-facts {
    row-gap: 0;
    border-top: 1px solid var(--academic-border);
  }

  .hmcl-project-facts > div {
    min-width: 0;
    padding: 0.85rem 0;
    border-bottom: 1px solid var(--academic-border);
  }

  .hmcl-project-facts dt {
    margin-bottom: 0.25rem;
    font-size: 0.85rem;
    font-weight: 600;
  }

  .hmcl-project-facts dd {
    margin: 0;
    color: var(--academic-muted);
    overflow-wrap: anywhere;
  }

  .hmcl-project-figure {
    min-width: 0;
    margin: 1.5rem 0;
  }

  .hmcl-project-gallery > .hmcl-project-figure {
    margin: 0;
  }

  .hmcl-project .hmcl-project-figure > img {
    display: block;
    width: 100%;
    max-width: 100%;
    height: auto;
    margin: 0;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #fff;
  }

  .hmcl-project-figure > figcaption {
    margin-top: 0.5rem;
    color: var(--academic-muted);
    font-size: 0.8rem;
    line-height: 1.65;
  }

  @media (max-width: 767.98px) {
    .hmcl-project-facts,
    .hmcl-project-gallery {
      grid-template-columns: minmax(0, 1fr);
    }
  }
</style>
