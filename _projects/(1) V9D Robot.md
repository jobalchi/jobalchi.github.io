---
name: "V9D Robot: Indoor Virtual Tour Assistant"
year: 2023
permalink: /projects/v9d-robot/
tools: [ROS 2, Nav2, Cartographer, Gazebo, Three.js]
image: /assets/img/projects/v9d-robot/thumbnail.jpg
description: An indoor virtual-tour robot combining ROS 2 SLAM, Nav2 obstacle avoidance, Polylabel capture waypoints, and Gazebo simulation.
demo_url: https://www.youtube.com/watch?v=5P0a5i9b5wk
demo_video_id: 5P0a5i9b5wk
tour_url: https://senaro-a4da0.web.app
---

<div class="academic-page v9d-project" markdown="1">

# V9D Robot

<p class="v9d-project-subtitle">Indoor 360° Virtual Tour Assistant</p>
<p class="v9d-project-meta">2023 · Digital Innovation Sharing University Robotics Conference · Team SENARO</p>

V9D Robot is a team project designed to reduce the manual work involved in creating indoor virtual tours. It combines a mobile platform and height-adjustable 360° camera with a ROS 2 navigation stack. The software connects Cartographer mapping, AMCL localization, Nav2 obstacle avoidance, and map-based capture-waypoint generation, supported by a robot model and indoor environment in Gazebo.

<div class="v9d-project-links">
  <a class="btn academic-publication-link v9d-project-link" href="{{ page.demo_url | escape }}" target="_blank" rel="noopener noreferrer" aria-label="Watch the V9D Robot demonstration on YouTube (opens in a new tab)">
    <i class="fab fa-youtube" aria-hidden="true"></i> Watch Demo
  </a>
  <a class="btn academic-publication-link v9d-project-link" href="{{ page.tour_url | escape }}" target="_blank" rel="noopener noreferrer" aria-label="Explore the V9D Robot virtual tour (opens in a new tab)">
    <i class="fas fa-globe" aria-hidden="true"></i> Open Virtual Tour
  </a>
</div>

<figure class="v9d-project-figure">
  <img src="{{ '/assets/img/projects/v9d-robot/robot-design.png' | relative_url }}" alt="V9D Robot rendering with updated dimensions, battery, LiDAR, IMU, and camera specifications" width="1600" height="900" decoding="async">
  <figcaption>Robot design and updated specifications for the prototyping project.</figcaption>
</figure>

## Demonstration

<div class="v9d-project-video">
  <iframe src="https://www.youtube-nocookie.com/embed/{{ page.demo_video_id | escape }}" title="V9D Robot demonstration" width="1280" height="720" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" allow="encrypted-media; picture-in-picture; fullscreen" allowfullscreen></iframe>
</div>

## Hardware Design

The final design combines a two-motor mobile base, LiDAR and IMU sensing, an Intel NUC computer, and an Insta360 ONE X2 camera on a powered height-adjustment mechanism. A front-mounted touch display provides access to the tour-creation workflow.

<dl class="v9d-project-specs">
  <div><dt>Dimensions</dt><dd>540 × 540 × 1200 mm</dd></div>
  <div><dt>Design weight</dt><dd>Approximately 60 kg</dd></div>
  <div><dt>Drive system</dt><dd>Two 40 W BLDC motors</dd></div>
  <div><dt>Camera lift</dt><dd>15 W stepper motor and linear stage</dd></div>
  <div><dt>Sensors</dt><dd>RPLiDAR S2, with a 0.05–30 m sensing range, and a 9DoF IMU</dd></div>
  <div><dt>Camera</dt><dd>Insta360 ONE X2 with automatic height adjustment</dd></div>
  <div><dt>Compute and interface</dt><dd>Intel NUC, 15.8-inch touch display, USB 3.0, and HDMI</dd></div>
  <div><dt>Power</dt><dd>25.2 V, 40 Ah Li-ion battery (6S8P); estimated operating time of about 5 hours</dd></div>
</dl>

The power-distribution design supplies the drive motors and camera lift from the main battery and uses a DC–DC converter for the computer and peripherals. Operating-time figures are design estimates.

<figure class="v9d-project-figure">
  <img src="{{ '/assets/img/projects/v9d-robot/power.png' | relative_url }}" alt="Updated power-distribution diagram showing the battery, motor drivers, camera lift, DC–DC converter, computer, and RPLiDAR S2" width="1600" height="900" loading="lazy" decoding="async">
  <figcaption>Power distribution and the operating-time estimate used in the design.</figcaption>
</figure>

## Robot Model and Simulation

The robot is represented in URDF with links and joints for the chassis, driven wheels, caster assemblies, LiDAR, and camera. Visual meshes, collision geometry, and inertial properties support displaying the model in RViz and running it in Gazebo.

The camera housing is modeled as visual and collision geometry, while separate front and rear camera plugins generate wide-angle simulation images. A simulated LiDAR supplies range observations. The indoor test world includes walls, doors, desks, and chairs to represent the geometry the robot must navigate.

<div class="v9d-project-gallery">
  <figure class="v9d-project-figure">
    <img src="{{ '/assets/img/projects/v9d-robot/simulation-model.png' | relative_url }}" alt="V9D robot model displayed in RViz and Gazebo" width="1600" height="900" loading="lazy" decoding="async">
    <figcaption>URDF model displayed in RViz and Gazebo.</figcaption>
  </figure>
  <figure class="v9d-project-figure">
    <img src="{{ '/assets/img/projects/v9d-robot/simulation-environment.png' | relative_url }}" alt="Furnished indoor environment with walls, doors, tables, and chairs in Gazebo" width="1600" height="900" loading="lazy" decoding="async">
    <figcaption>Indoor environment constructed for simulation.</figcaption>
  </figure>
</div>

## ROS 2 SLAM and Obstacle-Avoidance Navigation

The software framework uses **ROS 2 Foxy and Nav2**, separating map creation, localization, and local motion control.

### Mapping with Cartographer

Cartographer processes LiDAR observations to construct an indoor occupancy map. Scan matching aligns observations as the robot moves, providing the map used by subsequent localization and navigation tasks.

### Localization with AMCL

Adaptive Monte Carlo Localization (AMCL) estimates the robot's pose on the saved map using a particle-based representation of position uncertainty. Aligning incoming LiDAR observations with the map allows the pose estimate to converge and supports navigation between capture locations.

### Local Control with DWB

Nav2's DWB controller handles local motion for path following and obstacle avoidance. It evaluates candidate motions against the path and costmap to select velocity commands for the robot. This local control connects the navigation goals to obstacle-aware movement through the indoor environment.

<div class="v9d-project-gallery">
  <figure class="v9d-project-figure">
    <img src="{{ '/assets/img/projects/v9d-robot/localization.png' | relative_url }}" alt="AMCL illustration showing particle initialization, convergence, and alignment with LiDAR observations" width="1600" height="900" loading="lazy" decoding="async">
    <figcaption>Illustration of AMCL particle convergence.</figcaption>
  </figure>
  <figure class="v9d-project-figure">
    <img src="{{ '/assets/img/projects/v9d-robot/local-navigation.png' | relative_url }}" alt="DWB navigation illustration with path, obstacle, and costmap layers displayed in RViz" width="1600" height="900" loading="lazy" decoding="async">
    <figcaption>DWB navigation visualization with path and costmap layers.</figcaption>
  </figure>
</div>

## Capture Waypoint Generation

Capture locations are generated from the occupancy-map image using **Polylabel**. The approach selects points inside free-space contours, favoring interior clearance even when a region is concave and its geometric centroid may lie outside the usable space.

1. **Divide the map image** into an N × M grid of regions of interest.
2. **Extract free space** by thresholding the white regions and finding their contours.
3. **Filter small regions** using the contour-area threshold.
4. **Apply Polylabel** to select an interior capture point for each retained contour.
5. **Convert pixels to map coordinates** using the resolution and origin from `map.yaml`, accounting for the image's vertical-axis direction.

The generated map-frame points become candidate navigation goals. The implementation also references Nav2 Simple Commander for sequencing navigation tasks.

<figure class="v9d-project-figure">
  <img src="{{ '/assets/img/projects/v9d-robot/waypoints.png' | relative_url }}" alt="Python waypoint-generation implementation alongside a partitioned occupancy map with selected interior points" width="1600" height="900" loading="lazy" decoding="async">
  <figcaption>Grid-based map partitioning and generated capture points.</figcaption>
</figure>

## 360° Capture and Tour Visualization

The camera captures panoramic views at selected locations, with its height adjusted by the lift mechanism. The visualization design uses Three.js to display panoramic imagery on a spherical mesh, allowing the viewer to look around each captured scene.

Connecting these views and adding location markers forms the intended virtual-tour workflow. Indoor maps support robot navigation, while the panoramic images provide the visual experience of the tour.

<figure class="v9d-project-figure">
  <img src="{{ '/assets/img/projects/v9d-robot/panorama.png' | relative_url }}" alt="An indoor panoramic image connected to a Three.js-based 360-degree viewer" width="1440" height="810" loading="lazy" decoding="async">
  <figcaption>Panoramic imagery and the proposed interactive viewing pipeline.</figcaption>
</figure>

## User Workflow

The intended interaction starts from the robot's touch display and connects the navigation stack to tour creation:

1. **Create or load an indoor map** and initialize the robot's pose.
2. **Generate capture waypoints** from free-space regions in the occupancy map using Polylabel.
3. **Navigate between capture points** with AMCL localization and Nav2's DWB controller for local obstacle avoidance.
4. **Capture and save panoramic views** at the selected locations as the navigation sequence progresses.
5. **Connect the views and add location markers** to prepare the virtual tour for exploration.

## Contribution

I worked on **SLAM and obstacle-avoidance navigation** within the ROS 2 system. My contribution focused on integrating indoor mapping, robot localization, and Nav2-based navigation so the robot could move between capture waypoints while accounting for obstacles in its surroundings.

</div>

{% include academic-page-styles.html %}

<style>
  .v9d-project > h1 {
    margin: 0 0 0.65rem;
    font-size: 2.1rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .v9d-project-subtitle {
    margin: 0 0 0.35rem;
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.5;
  }

  .v9d-project-meta {
    margin: 0 0 1.5rem;
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .v9d-project-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.65rem;
    margin: 1rem 0 1.5rem;
  }

  .v9d-project-link {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    font-size: 0.85rem;
  }

  .v9d-project-video {
    position: relative;
    aspect-ratio: 16 / 9;
    margin: 1.5rem 0;
    overflow: hidden;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #000;
  }

  .v9d-project-video > iframe {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    border: 0;
  }

  .v9d-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .v9d-project li + li {
    margin-top: 0.45rem;
  }

  .v9d-project > h3 {
    margin: 1.5rem 0 0.5rem;
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.5;
  }

  .v9d-project-gallery {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1.25rem;
    margin: 1.5rem 0;
  }

  .v9d-project-gallery > .v9d-project-figure {
    min-width: 0;
    margin: 0;
  }

  .v9d-project-specs {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    column-gap: 1.5rem;
    margin: 1.25rem 0;
    border-top: 1px solid var(--academic-border);
  }

  .v9d-project-specs > div {
    min-width: 0;
    padding: 0.85rem 0;
    border-bottom: 1px solid var(--academic-border);
  }

  .v9d-project-specs dt {
    margin-bottom: 0.25rem;
    font-size: 0.85rem;
    font-weight: 600;
  }

  .v9d-project-specs dd {
    margin: 0;
    color: var(--academic-muted);
    overflow-wrap: anywhere;
  }

  .v9d-project-figure {
    margin: 1.5rem 0;
  }

  .v9d-project .v9d-project-figure > img {
    display: block;
    width: 100%;
    max-width: 100%;
    height: auto;
    margin: 0;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #fff;
  }

  .v9d-project-figure > figcaption {
    margin-top: 0.5rem;
    color: var(--academic-muted);
    font-size: 0.8rem;
    line-height: 1.65;
  }

  @media (max-width: 575.98px) {
    .v9d-project-specs {
      grid-template-columns: minmax(0, 1fr);
    }
  }

  @media (max-width: 767.98px) {
    .v9d-project-gallery {
      grid-template-columns: minmax(0, 1fr);
    }
  }
</style>
