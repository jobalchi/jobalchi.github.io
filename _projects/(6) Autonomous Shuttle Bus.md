---
name: "Autonomous Shuttle Bus"
year: 2024
permalink: /projects/autonomous-shuttle-bus/
tools: [Autonomous Driving, HD Mapping, Motion Prediction, Local Planning, Sensor Fusion]
image: /assets/img/projects/autonomous-shuttle-bus/demo-poster.jpg
description: A 2024 UNIST autonomous shuttle demonstration, where I worked on HD map construction, map-based prediction, and local planning for campus driving.
demo_url: https://www.youtube.com/watch?v=qivD2N3cMXw
demo_video_id: qivD2N3cMXw
---

<div class="academic-page shuttle-project" markdown="1">

# Autonomous Shuttle Bus

<p class="shuttle-project-subtitle">HD Mapping, Map-Based Prediction, and Local Planning</p>
<p class="shuttle-project-meta">2024 · UNIST Future Mobility Research Institute · UNIST</p>

I worked on **HD map construction, map-based prediction, and local planning** for a UNIST autonomous shuttle bus project. The campus demonstration connected a mapped driving route with surrounding-object perception and vehicle control, showing how the shuttle responded to vehicles and pedestrians along its path.

The driving scenarios included stopping for a vehicle ahead, following a moving vehicle while maintaining separation, and stopping after detecting a pedestrian. Target speeds were configured by route section, connecting route context to the shuttle's driving behavior.

## Demonstration

<div class="shuttle-project-video">
  <iframe src="https://www.youtube-nocookie.com/embed/{{ page.demo_video_id | escape }}" title="UNIST autonomous shuttle bus driving demonstration" width="1280" height="720" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" allow="encrypted-media; picture-in-picture; fullscreen" allowfullscreen></iframe>
</div>

<div class="shuttle-project-links">
  <a class="btn academic-publication-link shuttle-project-link" href="{{ page.demo_url | escape }}" target="_blank" rel="noopener noreferrer" aria-label="Watch the autonomous shuttle bus demonstration on YouTube (opens in a new tab)">
    <i class="fab fa-youtube" aria-hidden="true"></i> Watch Demo
  </a>
</div>

## System Overview

The shuttle platform brought together environmental sensing, mapping, localization, perception, planning, and vehicle control. The system overview also connects state estimation with speed, heading, steering, and acceleration/braking control.

During the demonstration, the monitoring views combined a point-cloud map, the shuttle's route and position, camera-based object detections, and external views of the vehicle. These views made it possible to inspect perception and the shuttle's response within the same driving scene.

<figure class="shuttle-project-figure">
  <img src="{{ '/assets/img/projects/autonomous-shuttle-bus/system-overview.png' | relative_url }}" alt="Autonomous shuttle system overview showing sensing, mapping, perception, localization, planning, state estimation, and vehicle control" width="1040" height="485" loading="lazy" decoding="async">
  <figcaption>Sensing, mapping, planning, and control components of the shuttle platform.</figcaption>
</figure>

## HD Mapping and Map-Based Prediction

My work included building the **HD map** used as a reference for campus driving. The mapped environment provided spatial context for localization and route planning, while the point-cloud view supported checking the shuttle's progress along the driving corridor.

I also worked on **map-based prediction**, using map context to inform surrounding-motion prediction for local planning. This connected the known road layout to decisions about how the shuttle should proceed around nearby road users.

<figure class="shuttle-project-figure">
  <img src="{{ '/assets/img/projects/autonomous-shuttle-bus/map-based-prediction-trajectories.png' | relative_url }}" alt="Annotated intersection map showing an opponent vehicle and two lane-based candidate trajectories" width="1896" height="704" loading="lazy" decoding="async">
  <figcaption>Map-based candidate trajectories for an opponent vehicle.</figcaption>
</figure>

<figure class="shuttle-project-figure">
  <div class="shuttle-project-video">
    <video controls playsinline preload="none" poster="{{ '/assets/img/projects/autonomous-shuttle-bus/map-based-prediction-poster.jpg' | relative_url }}" width="1600" height="900" aria-label="Map-based motion prediction visualization">
      <source src="{{ '/assets/videos/projects/autonomous-shuttle-bus/map-based-prediction.mp4' | relative_url }}" type="video/mp4">
      Your browser does not support embedded video. <a href="{{ '/assets/videos/projects/autonomous-shuttle-bus/map-based-prediction.mp4' | relative_url }}">Watch the prediction video</a>.
    </video>
  </div>
  <figcaption>Map-based prediction visualization.</figcaption>
</figure>

## Local Planning and Vehicle Interaction

The local planning work connected the reference route, surrounding-object information, and the shuttle's immediate driving response. Route-section speed targets provided the driving context, while the vehicle-ahead scenarios demonstrated braking and following behavior.

In the stopping scenario, the front camera identifies a vehicle on the route and the external view shows the shuttle's response. In the following scenario, the visualization shows the detected lead vehicle together with the mapped route as the shuttle continues while maintaining separation.

<div class="shuttle-project-gallery">
  <figure class="shuttle-project-figure">
    <img src="{{ '/assets/img/projects/autonomous-shuttle-bus/vehicle-braking.jpg' | relative_url }}" alt="Mapped route, front-camera vehicle detection, and external shuttle view during the vehicle-ahead braking scenario" width="1280" height="720" loading="lazy" decoding="async">
    <figcaption>Vehicle-ahead detection and braking.</figcaption>
  </figure>
  <figure class="shuttle-project-figure">
    <img src="{{ '/assets/img/projects/autonomous-shuttle-bus/vehicle-following.jpg' | relative_url }}" alt="Lead-vehicle detection and route visualization during the shuttle's distance-maintaining following scenario" width="1280" height="720" loading="lazy" decoding="async">
    <figcaption>Following a moving vehicle while maintaining separation.</figcaption>
  </figure>
</div>

## Planning Videos

<div class="shuttle-project-gallery">
  <figure class="shuttle-project-figure">
    <div class="shuttle-project-video">
      <video controls playsinline preload="none" poster="{{ '/assets/img/projects/autonomous-shuttle-bus/scenario-1-poster.jpg' | relative_url }}" width="1600" height="900" aria-label="UNIST planning scenario 1">
        <source src="{{ '/assets/videos/projects/autonomous-shuttle-bus/scenario-1.mp4' | relative_url }}" type="video/mp4">
        Your browser does not support embedded video. <a href="{{ '/assets/videos/projects/autonomous-shuttle-bus/scenario-1.mp4' | relative_url }}">Watch scenario 1</a>.
      </video>
    </div>
    <figcaption>Planning scenario 1.</figcaption>
  </figure>
  <figure class="shuttle-project-figure">
    <div class="shuttle-project-video">
      <video controls playsinline preload="none" poster="{{ '/assets/img/projects/autonomous-shuttle-bus/scenario-2-poster.jpg' | relative_url }}" width="1600" height="900" aria-label="UNIST planning scenario 2">
        <source src="{{ '/assets/videos/projects/autonomous-shuttle-bus/scenario-2.mp4' | relative_url }}" type="video/mp4">
        Your browser does not support embedded video. <a href="{{ '/assets/videos/projects/autonomous-shuttle-bus/scenario-2.mp4' | relative_url }}">Watch scenario 2</a>.
      </video>
    </div>
    <figcaption>Planning scenario 2.</figcaption>
  </figure>
</div>

## Pedestrian Response

The pedestrian scenario shows a person detected near a campus crossing and the shuttle stopping in response. Camera detections, the map-based monitoring view, and an external camera document the same interaction from complementary perspectives.

Together, these scenarios demonstrate the connection between the mapped route, object perception, local planning, and the vehicle's physical response in a campus setting.

<figure class="shuttle-project-figure">
  <img src="{{ '/assets/img/projects/autonomous-shuttle-bus/pedestrian-response.jpg' | relative_url }}" alt="Pedestrian detection at a campus crossing shown alongside the point-cloud map and an external view of the shuttle" width="1280" height="720" loading="lazy" decoding="async">
  <figcaption>Pedestrian detection and stopping at a campus crossing.</figcaption>
</figure>

## Contribution

I worked on **HD map construction, map-based prediction, and local planning**, connecting the mapped campus environment and surrounding-motion prediction to the shuttle's route-based driving behavior.

</div>

{% include academic-page-styles.html %}

<style>
  .shuttle-project > h1 {
    margin: 0 0 0.65rem;
    font-size: 2.1rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .shuttle-project-subtitle {
    margin: 0 0 0.35rem;
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.5;
  }

  .shuttle-project-meta {
    margin: 0 0 1.5rem;
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .shuttle-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .shuttle-project-video {
    position: relative;
    aspect-ratio: 16 / 9;
    margin: 1.5rem 0;
    overflow: hidden;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #000;
  }

  .shuttle-project-video > iframe,
  .shuttle-project-video > video {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    border: 0;
  }

  .shuttle-project-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.65rem;
    margin: 1rem 0 1.5rem;
  }

  .shuttle-project-link {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    font-size: 0.85rem;
  }

  .shuttle-project-gallery {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1.25rem;
    margin: 1.5rem 0;
  }

  .shuttle-project-figure {
    min-width: 0;
    margin: 1.5rem 0;
  }

  .shuttle-project-gallery > .shuttle-project-figure {
    margin: 0;
  }

  .shuttle-project .shuttle-project-figure > img {
    display: block;
    width: 100%;
    max-width: 100%;
    height: auto;
    margin: 0;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #fff;
  }

  .shuttle-project-figure > figcaption {
    margin-top: 0.5rem;
    color: var(--academic-muted);
    font-size: 0.8rem;
    line-height: 1.65;
  }

  @media (max-width: 767.98px) {
    .shuttle-project-gallery {
      grid-template-columns: minmax(0, 1fr);
    }
  }
</style>
