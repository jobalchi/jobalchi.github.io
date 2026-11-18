---
name: "Holo Bot: Shared Scooter Recovery Robot"
year: 2023
permalink: /projects/holo-bot/
tools: [ROS 2, Nav2, Sensor Fusion, YOLOv5, ArUco]
image: /assets/img/projects/holo-bot/thumbnail.jpg
description: A shared-scooter recovery project connecting outdoor navigation, visual detection, marker-based docking, and a custom lift mechanism.
demo_video: /assets/videos/projects/holo-bot/demonstration.mp4
demo_poster: /assets/img/projects/holo-bot/demo-poster.jpg
---

<div class="academic-page holo-project" markdown="1">

# Holo Bot

<p class="holo-project-subtitle">Shared Scooter Recovery Robot</p>
<p class="holo-project-meta">2023 · Smart Convergence Capstone Design · Team 홀로서기</p>

Holo Bot is a team robotics project for locating fallen or improperly parked shared scooters and assisting their return to a designated personal-mobility parking zone. The work progressed from a mobile-manipulation simulation to a capstone prototype combining outdoor navigation, visual perception, marker-based docking, and a custom lift mechanism.

The system connects a WeGo ST-MINI mobile platform with GNSS, IMU, wheel odometry, LiDAR, and cameras. ROS 2 coordinates the navigation, detection, docking, and lift-control components.

<figure class="holo-project-figure">
  <img src="{{ '/assets/img/projects/holo-bot/robot-design.png' | relative_url }}" alt="Front and rear views of Holo Bot showing the mobile platform, lift, cameras, LiDAR, and GNSS antenna" width="1600" height="1200" decoding="async">
  <figcaption>Mobile-platform design and sensor placement.</figcaption>
</figure>

## Demonstration

<div class="holo-project-video">
  <video controls playsinline preload="none" poster="{{ page.demo_poster | relative_url }}" width="1280" height="720" aria-label="Holo Bot demonstration">
    <source src="{{ page.demo_video | relative_url }}" type="video/mp4">
    Your browser does not support embedded video. <a href="{{ page.demo_video | relative_url }}">Download the demonstration video</a>.
  </video>
</div>

## Mission Workflow

The mission logic connects patrol navigation to scooter recovery:

1. **Patrol the parking area** through designated outdoor waypoints and check for scooters outside the parking zone.
2. **Detect a scooter** with YOLOv5 and use depth information to estimate its position.
3. **Establish an approach pose** using ArUco-marker observations and the scooter's coordinate frame.
4. **Turn and dock in reverse**, adjusting the robot's alignment relative to the marker.
5. **Operate the lift and gripper**, then hand control back to navigation for the intended return to the parking zone.

## From Simulation to Prototype

The initial study used V-REP to explore mobile manipulation. A mobile base and UR5 arm approached and grasped a scooter model, with BiTRRT-based motion planning and proximity sensing supporting the simulated scenario.

That stage used simulator-provided position information and proximity sensors as substitutes for parts of the intended sensing system. The capstone then developed a physical mobile platform and a dedicated lift mechanism, alongside tests of navigation, perception, docking, and actuator control.

<figure class="holo-project-figure">
  <img src="{{ '/assets/img/projects/holo-bot/simulation.png' | relative_url }}" alt="Early V-REP simulation with a mobile manipulator, scooters, parking stands, pedestrians, and planned paths" width="1600" height="1200" loading="lazy" decoding="async">
  <figcaption>Early simulation of path planning, manipulation, and obstacle detection.</figcaption>
</figure>

## Hardware and Sensors

The capstone platform pairs the WeGo ST-MINI base with an upper structure built using profiles, acrylic panels, and printed components. A laptop motherboard provides the main computing platform, while a Raspberry Pi 4B handles the lift-control interface.

<dl class="holo-project-specs">
  <div><dt>Mobile platform</dt><dd>WeGo ST-MINI; base dimensions of 612 × 580 × 245 mm</dd></div>
  <div><dt>Depth camera</dt><dd>STEREOLABS ZED2i for scooter detection and distance estimation</dd></div>
  <div><dt>Docking camera</dt><dd>Logitech C920 for rear-facing ArUco-marker observations</dd></div>
  <div><dt>Outdoor positioning</dt><dd>U-blox C099-F9P GNSS receiver, UM7-LT IMU, and wheel odometry</dd></div>
  <div><dt>Obstacle sensing</dt><dd>RPLiDAR S2 for range observations and navigation</dd></div>
  <div><dt>Controllers</dt><dd>Intel i7-8750H and GTX 1060 6 GB main computer; Raspberry Pi 4B subcontroller</dd></div>
</dl>

## Outdoor Navigation and Sensor Fusion

The navigation system uses **ROS 2 Nav2** with GPS-coordinate waypoints. The `robot_localization` package fuses GPS, IMU, and wheel-odometry observations through extended Kalman filters.

The localization architecture separates local and global estimation. Wheel odometry and IMU data feed the local filter, while `navsat_transform` connects GNSS observations to the map-referenced global estimate. This provides the positioning framework for outdoor waypoint navigation.

Cartographer mapping tests were also conducted at the campus test field and an indoor engineering-building corridor. The project materials document positioning traces, sensor-fusion observations, and a waypoint-navigation test near the library.

<div class="holo-project-gallery">
  <figure class="holo-project-figure">
    <img src="{{ '/assets/img/projects/holo-bot/sensor-fusion.png' | relative_url }}" alt="Localization architecture connecting wheel odometry, IMU, local and global EKF filters, GPS, and navsat_transform" width="1600" height="1200" loading="lazy" decoding="async">
    <figcaption>Local and global estimation with GPS, IMU, and wheel odometry.</figcaption>
  </figure>
  <figure class="holo-project-figure">
    <img src="{{ '/assets/img/projects/holo-bot/outdoor-positioning.png' | relative_url }}" alt="GNSS and RTK positioning trace displayed over a campus satellite map" width="1600" height="1200" loading="lazy" decoding="async">
    <figcaption>Outdoor positioning trace visualized over the campus map.</figcaption>
  </figure>
</div>

## Scooter Perception and Approach

The perception pipeline combines a scooter-specific **YOLOv5** model with the ZED2i depth camera. Image detections identify a target scooter, while depth and coordinate transforms support estimating its position relative to the robot and map.

ArUco markers provide an additional reference for approach alignment. The approach strategy uses marker pose and a designated K-Point to define the desired relationship between the robot and scooter before the reverse-docking stage.

<div class="holo-project-gallery">
  <figure class="holo-project-figure">
    <img src="{{ '/assets/img/projects/holo-bot/scooter-detection.png' | relative_url }}" alt="Outdoor scooter-detection test using the trained YOLOv5 model and ZED2i camera" width="1600" height="1200" loading="lazy" decoding="async">
    <figcaption>Scooter detection using the trained model.</figcaption>
  </figure>
  <figure class="holo-project-figure">
    <img src="{{ '/assets/img/projects/holo-bot/marker-approach.png' | relative_url }}" alt="ArUco-marker placement and robot-to-scooter coordinate frames used to define the K-Point approach" width="1600" height="1200" loading="lazy" decoding="async">
    <figcaption>Marker observations and coordinate frames for the approach strategy.</figcaption>
  </figure>
</div>

## Docking and Recovery Control

The rear camera detects the ArUco marker's ID and pose. The docking controller uses the marker's relative distance and orientation to command linear and angular velocity through `/cmd_vel`, reversing toward the scooter while correcting alignment.

The demonstrated docking code stops motion when the marker distance falls below **0.5 m** and passes a completion signal to the next stage. This connects visual alignment to the lift-control sequence.

<figure class="holo-project-figure">
  <img src="{{ '/assets/img/projects/holo-bot/docking.png' | relative_url }}" alt="Annotated docking code showing reverse motion, angular correction, and the marker-distance stopping condition" width="1600" height="1200" loading="lazy" decoding="async">
  <figcaption>Marker-based docking logic and the stopping condition.</figcaption>
</figure>

## Lift and Gripper Coordination

The capstone replaces the earlier manipulator concept with a dedicated mechanism driven by a stepper motor and linear stage. The linkage lifts the scooter, and a servo-driven gripper secures it for the intended transport step.

ROS 2 publisher–subscriber messages coordinate the mechanism with docking and navigation. After receiving `docking_msg`, the Raspberry Pi drives the stepper until a limit switch indicates the upper position. The control sequence then operates the gripper and issues the transition for travel toward the parking zone.

The prototype work includes bench tests of the lift and gripper, along with the navigation, perception, and docking tests described above.

<figure class="holo-project-figure">
  <img src="{{ '/assets/img/projects/holo-bot/lift-test.png' | relative_url }}" alt="Two frames of the physical lift mechanism during bench testing" width="1600" height="1200" loading="lazy" decoding="async">
  <figcaption>Lift mechanism during prototype testing.</figcaption>
</figure>

## Contribution

I worked on **outdoor navigation and sensor fusion**. My contribution focused on GPS-waypoint navigation with ROS 2 Nav2 and integrating GPS, IMU, and wheel-odometry observations through the `robot_localization` framework. I worked on the positioning and navigation components that support the robot's movement through the outdoor test environment.

</div>

{% include academic-page-styles.html %}

<style>
  .holo-project > h1 {
    margin: 0 0 0.65rem;
    font-size: 2.1rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .holo-project-subtitle {
    margin: 0 0 0.35rem;
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.5;
  }

  .holo-project-meta {
    margin: 0 0 1.5rem;
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .holo-project-video {
    margin: 1.5rem 0;
  }

  .holo-project-video > video {
    display: block;
    width: 100%;
    height: auto;
    aspect-ratio: 16 / 9;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #000;
  }

  .holo-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .holo-project li + li {
    margin-top: 0.45rem;
  }

  .holo-project-specs,
  .holo-project-gallery {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1.25rem;
    margin: 1.5rem 0;
  }

  .holo-project-specs {
    row-gap: 0;
    border-top: 1px solid var(--academic-border);
  }

  .holo-project-specs > div {
    min-width: 0;
    padding: 0.85rem 0;
    border-bottom: 1px solid var(--academic-border);
  }

  .holo-project-specs dt {
    margin-bottom: 0.25rem;
    font-size: 0.85rem;
    font-weight: 600;
  }

  .holo-project-specs dd {
    margin: 0;
    color: var(--academic-muted);
    overflow-wrap: anywhere;
  }

  .holo-project-figure {
    min-width: 0;
    margin: 1.5rem 0;
  }

  .holo-project-gallery > .holo-project-figure {
    margin: 0;
  }

  .holo-project .holo-project-figure > img {
    display: block;
    width: 100%;
    max-width: 100%;
    height: auto;
    margin: 0;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #fff;
  }

  .holo-project-figure > figcaption {
    margin-top: 0.5rem;
    color: var(--academic-muted);
    font-size: 0.8rem;
    line-height: 1.65;
  }

  @media (max-width: 767.98px) {
    .holo-project-specs,
    .holo-project-gallery {
      grid-template-columns: minmax(0, 1fr);
    }
  }
</style>
