---
name: "2024 University Student Autonomous Driving Competition"
year: 2024
permalink: /projects/autonomous-driving-2024/
tools: [Autonomous Driving, Local Planning, Graph-Based Planning, Sensor Fusion, ROS]
image: /assets/img/projects/autonomous-driving-2024/competition-thumbnail.jpg
description: A full-size autonomous racing project with Team UNIST HMCL, where I developed graph-based local path planning using surrounding-object motion and cost-based path selection.
demo_url: https://www.youtube.com/watch?v=O4rKc23REUk
demo_video_id: O4rKc23REUk
---

<div class="academic-page driving2024-project" markdown="1">

# 2024 University Student Autonomous Driving Competition

<p class="driving2024-project-subtitle">High-Speed Autonomous Driving and Graph-Based Local Planning</p>
<p class="driving2024-project-meta">2024 · MOTIE Competition · Team UNIST HMCL</p>

I participated in the **2024 University Student Autonomous Driving Competition** as a member of **Team UNIST HMCL**, working on **graph-based local path planning**. The project developed a full-size autonomous driving system for multi-vehicle racing on a high-speed track, connecting localization, perception, prediction, planning, and vehicle control.

The racing environment included three-lane roads, banked sections, and moving opponents. The system combined a map-based reference path with local replanning to respond to surrounding traffic, while simulation and physical-vehicle testing exposed the practical demands of high-speed driving.

## Video

<div class="driving2024-project-video">
  <iframe src="https://www.youtube-nocookie.com/embed/{{ page.demo_video_id | escape }}" title="UNIST HMCL 2024 autonomous driving competition video" width="1280" height="720" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" allow="encrypted-media; picture-in-picture; fullscreen" allowfullscreen></iframe>
</div>

<div class="driving2024-project-links">
  <a class="btn academic-publication-link driving2024-project-link" href="{{ page.demo_url | escape }}" target="_blank" rel="noopener noreferrer" aria-label="Watch the UNIST HMCL 2024 competition video on YouTube (opens in a new tab)">
    <i class="fab fa-youtube" aria-hidden="true"></i> Watch Video
  </a>
</div>

## System Architecture

The software stack was built on **Ubuntu 20.04 and ROS 1**, with Python and C++ components. Sensor drivers connected LiDAR, cameras, GPS, and IMUs to localization and perception. Vehicle pose and predicted object motion then fed the global and local planners, whose paths and speed profiles were passed to the controller.

<dl class="driving2024-project-facts">
  <div><dt>Operating system</dt><dd>Ubuntu 20.04</dd></div>
  <div><dt>Middleware</dt><dd>ROS 1</dd></div>
  <div><dt>Implementation</dt><dd>Python and C++</dd></div>
  <div><dt>Planning validation</dt><dd>CARLA-based simulation and vehicle testing</dd></div>
</dl>

<figure class="driving2024-project-figure">
  <img src="{{ '/assets/img/projects/autonomous-driving-2024/architecture.jpg' | relative_url }}" alt="HMCL autonomous driving software architecture linking sensors, localization, perception, prediction, global and local planning, and vehicle control" width="1499" height="578" decoding="async">
  <figcaption>Localization, perception, planning, and control architecture.</figcaption>
</figure>

## Sensor Integration and Perception

The team calibrated multiple LiDARs, camera intrinsics and camera–LiDAR alignment, IMU measurements, and GPS-to-map coordinates. This provided a shared spatial basis for combining sensor observations.

**YOLOv5** supported camera-based object detection, while **PointPillars** supplied LiDAR-based detections. Camera–LiDAR fusion complemented the individual sensors, and tracking provided surrounding-object information for prediction and planning. LiDAR-only and fusion-based detection were also used in parallel to preserve detection availability if one pipeline stopped.

<figure class="driving2024-project-figure">
  <img src="{{ '/assets/img/projects/autonomous-driving-2024/perception-fusion.jpg' | relative_url }}" alt="Camera detections and LiDAR object detections shown side by side in the report's sensor-fusion example" width="1399" height="424" loading="lazy" decoding="async">
  <figcaption>Camera–LiDAR perception-fusion example.</figcaption>
</figure>

## Mapping and Localization

Point-cloud and vector maps represented the track geometry, road connectivity, and section-specific information such as speed limits and banked areas. Map-derived reference paths were smoothed through global path optimization to reduce unnecessary movement and support high-speed tracking.

The localization system used parallel **LiDAR–IMU and GPS–IMU estimation branches**, with separate IMUs and reliability-based selection. An extended Kalman filter supported smoother transitions between estimates, while GPS information helped align the point-cloud map with the global reference.

<figure class="driving2024-project-figure">
  <img src="{{ '/assets/img/projects/autonomous-driving-2024/vector-map-comparison.png' | relative_url }}" alt="Side-by-side GNSS-based and LiDAR-based vector maps of the high-speed track" width="1834" height="560" loading="lazy" decoding="async">
  <figcaption>GNSS-based and LiDAR-based vector maps of the high-speed track.</figcaption>
</figure>

## Graph-Based Local Planning

My work focused on the **graph-based local path planner**. The planner used real-time surrounding-object information to predict object motion, evaluate path costs, and select a local path around traffic. This connected the global reference route to the changing obstacle situation near the ego vehicle.

The planning pipeline combined map-based reference-path generation with local replanning and a velocity profile for the controller. CARLA-based simulation supported testing planning behavior before physical-vehicle validation.

<figure class="driving2024-project-figure">
  <img src="{{ '/assets/img/projects/autonomous-driving-2024/reference-planning.jpg' | relative_url }}" alt="Reference-path preparation pipeline from sensor-derived maps through centerline extraction to track optimization" width="1199" height="510" loading="lazy" decoding="async">
  <figcaption>Map-based reference-path preparation.</figcaption>
</figure>

<figure class="driving2024-project-figure">
  <img src="{{ '/assets/img/projects/autonomous-driving-2024/local-planning-combined.png' | relative_url }}" alt="Graph-based planner figure combining full-track and detailed graph plots above online local-trajectory visualizations in RViz" width="1872" height="1142" loading="lazy" decoding="async">
  <figcaption>Graph-based planning: track-level and detailed graphs (top), and online local planning in RViz (bottom).</figcaption>
</figure>

## Prediction and Vehicle Control

The team's opponent-prediction approach used the three lanes' path information with a **Stanley-model-based trajectory estimate**. Perception-validity checks filtered noisy observations and false vehicle detections before the prediction was used in planning.

Vehicle control paired **PID longitudinal control** with a **preview lateral controller**. Parameters were tuned for lane changes, curves, and banked sections, while CAN communication connected the software commands to the vehicle interface.

## Development Insights

Physical testing highlighted the connection between path generation and controllability. When some graph-generated paths were difficult to track, the team also developed behavior-based path shifting, limiting the lateral change to a controllable range for obstacle avoidance.

Long-range detection, banked-road localization, and changing road grip remained important challenges. The report identified wet-surface tracking and model mismatch as areas needing further development, reinforcing the need to evaluate planning and control together under representative driving conditions.

## Contribution

I developed the **graph-based local path planner**, focusing on cost-based path selection using surrounding-object motion to support local replanning within the team's autonomous driving system.

I also built the **low-level CAN communication system**, connecting the autonomous driving software to the vehicle's control interface.

</div>

{% include academic-page-styles.html %}

<style>
  .driving2024-project > h1 {
    margin: 0 0 0.65rem;
    font-size: 2.1rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .driving2024-project-subtitle {
    margin: 0 0 0.35rem;
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.5;
  }

  .driving2024-project-meta {
    margin: 0 0 1.5rem;
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .driving2024-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .driving2024-project-video {
    position: relative;
    aspect-ratio: 16 / 9;
    margin: 1.5rem 0;
    overflow: hidden;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #000;
  }

  .driving2024-project-video > iframe {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    border: 0;
  }

  .driving2024-project-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.65rem;
    margin: 1rem 0 1.5rem;
  }

  .driving2024-project-link {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    font-size: 0.85rem;
  }

  .driving2024-project-facts {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    column-gap: 1.25rem;
    margin: 1.5rem 0;
    border-top: 1px solid var(--academic-border);
  }

  .driving2024-project-facts > div {
    min-width: 0;
    padding: 0.85rem 0;
    border-bottom: 1px solid var(--academic-border);
  }

  .driving2024-project-facts dt {
    margin-bottom: 0.25rem;
    font-size: 0.85rem;
    font-weight: 600;
  }

  .driving2024-project-facts dd {
    margin: 0;
    color: var(--academic-muted);
    overflow-wrap: anywhere;
  }

  .driving2024-project-figure {
    min-width: 0;
    margin: 1.5rem 0;
  }

  .driving2024-project .driving2024-project-figure > img {
    display: block;
    width: 100%;
    max-width: 100%;
    height: auto;
    margin: 0;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #fff;
  }

  .driving2024-project-figure > figcaption {
    margin-top: 0.5rem;
    color: var(--academic-muted);
    font-size: 0.8rem;
    line-height: 1.65;
  }

  @media (max-width: 767.98px) {
    .driving2024-project-facts {
      grid-template-columns: minmax(0, 1fr);
    }
  }
</style>
