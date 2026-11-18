---
name: "Robot Vision System: Campus Autonomous Driving"
year: 2023
permalink: /projects/robot-vision-system/
tools: [Autonomous Driving, OpenCV, ROS 2, Unity, Python]
image: /assets/img/projects/robot-vision-system/campus-driving.jpg
description: A camera-based driving system for a Unity model of Hanyang University ERICA, using OpenCV and ROS 2 for lane following and intersection control.
---

<article class="academic-page rvs-project" markdown="1">

<header class="academic-page-header">
  <h1>Robot Vision System</h1>
  <p class="rvs-project-subtitle">Vision-Based Autonomous Driving on the ERICA Campus</p>
  <p class="rvs-project-meta">2023 · Robot Vision System · Hanyang University ERICA</p>
</header>

This vision-system design project developed a camera-based autonomous driving system for a **Unity model of the Hanyang University ERICA campus**. The simulated vehicle used its front camera to follow lane markings, read traffic lights, and detect stop lines. A ROS 2 controller combined those observations with the vehicle's simulated position to decide when to steer, slow down, or brake.

<figure class="rvs-project-figure">
  <img src="{{ '/assets/img/projects/robot-vision-system/campus-driving.jpg' | relative_url }}" alt="Red simulated vehicle approaching a curve on a road in the Unity model of the ERICA campus" width="1600" height="1015" decoding="async">
  <figcaption>The simulated vehicle approaching a bend on an ERICA campus road.</figcaption>
</figure>

## Driving Demonstration

<figure class="rvs-project-figure rvs-project-demo">
  <video controls playsinline preload="none" poster="{{ '/assets/img/projects/robot-vision-system/demo-poster.jpg' | relative_url }}" width="640" height="480" aria-label="Onboard driving demonstration in the Unity model of the ERICA campus">
    <source src="{{ '/assets/videos/projects/robot-vision-system/campus-driving-demo.mp4' | relative_url }}" type="video/mp4">
    <a href="{{ '/assets/videos/projects/robot-vision-system/campus-driving-demo.mp4' | relative_url }}">Download the driving demonstration</a>
  </video>
  <figcaption>Onboard footage of lane following and intersection approaches in the Unity campus model.</figcaption>
</figure>

## Campus Route and Simulation

The assignment defined a **four-waypoint loop** through the campus, with a shared start and finish near Way 0. The Unity road network reproduced the campus setting with curves, lane markings, and intersections. Between intersections, the vehicle followed the visible lane boundaries. At selected junctions, position ranges identified where the controller should apply the route-specific rules.

<figure class="rvs-project-figure">
  <img src="{{ '/assets/img/projects/robot-vision-system/campus-overview.jpg' | relative_url }}" alt="Aerial view of the Unity campus model showing the road network, intersections, and campus buildings" width="1600" height="672" loading="lazy" decoding="async">
  <figcaption>The ERICA campus road network in Unity.</figcaption>
</figure>

<figure class="rvs-project-figure rvs-project-route">
  <img src="{{ '/assets/img/projects/robot-vision-system/campus-route.jpg' | relative_url }}" alt="ERICA campus map with a red loop linking Way 0, Way 1, Way 2, and Way 3" width="1117" height="820" loading="lazy" decoding="async">
  <figcaption>The planned campus loop with four waypoints and a shared start and finish.</figcaption>
</figure>

## Unity and ROS 2 Integration

The **ROS TCP Endpoint** connected Unity to the Python ROS 2 nodes. Unity supplied front-camera frames and vehicle state. The lane, traffic-light, and stop-line detectors ran as separate nodes and published their results to the driving node, which returned steering, motor-speed, and brake commands to the simulator.

<figure class="rvs-project-figure">
  <img src="{{ '/assets/img/projects/robot-vision-system/front-camera.jpg' | relative_url }}" alt="Simulated front-camera view showing the vehicle hood, a yellow lane marking, and a right-turn road arrow" width="1600" height="932" loading="lazy" decoding="async">
  <figcaption>The front-camera view used by the three perception nodes.</figcaption>
</figure>

## Lane Detection and Steering

The **OpenCV** lane detector converted each front-camera frame into a steering reference.

1. **Isolate lane markings.** Use HSV color filtering to retain yellow and white road markings.
2. **Extract edges.** Apply Gaussian smoothing and Canny edge detection, then keep the road region of interest.
3. **Detect line segments.** Use the probabilistic Hough transform and group candidate segments by slope.
4. **Fit the lane boundaries.** Fit a line to each group to estimate the left and right boundary angles.
5. **Publish a steering reference.** Average and scale the fitted angles and send the result to the driving node.

<figure class="rvs-project-figure">
  <img src="{{ '/assets/img/projects/robot-vision-system/lane-detection.png' | relative_url }}" alt="Six lane-detection stages from a camera frame through HSV filtering, Canny edges, road masking, Hough segments, and two fitted lane boundaries" width="1980" height="1125" loading="lazy" decoding="async">
  <figcaption>Lane detection from the raw camera frame to fitted left and right boundaries.</figcaption>
</figure>

## Traffic Lights and Stop Lines

The traffic-light detector estimated the active signal color.

1. **Select the search region.** Keep the upper portion of the frame where traffic lights are expected.
2. **Locate the signal.** Apply a **Haar cascade** and extract the detected region.
3. **Classify the color.** Compare pixel counts in red, yellow, and green HSV masks and publish the dominant signal color.

<figure class="rvs-project-figure">
  <img src="{{ '/assets/img/projects/robot-vision-system/traffic-light-detection.png' | relative_url }}" alt="Traffic light localized by the Haar cascade and classified as yellow based on the pixel counts in its color masks" width="1980" height="1042" loading="lazy" decoding="async">
  <figcaption>Traffic-light localization and HSV classification of a yellow signal.</figcaption>
</figure>

The stop-line detector checked for a road marking directly ahead of the vehicle.

1. **Filter road markings.** Use HSV masks for gray and white pixels, then apply Canny edge detection.
2. **Isolate the road.** Limit processing to the road region of interest and apply a perspective transform to produce a **bird's-eye view**.
3. **Detect a nearby stop line.** Search the lower half of the transformed image with the Hough transform and publish a detection when a candidate line is found.

<figure class="rvs-project-figure">
  <img src="{{ '/assets/img/projects/robot-vision-system/stop-line-detection.png' | relative_url }}" alt="Six stop-line detection stages including color filtering, road masking, perspective transformation, and a final red line overlay" width="1980" height="1125" loading="lazy" decoding="async">
  <figcaption>Stop-line detection with a perspective transform and a near-field Hough search.</figcaption>
</figure>

## PID Steering and Intersection Control

The driving node used a **PID controller** for lane following and applied intersection rules based on the detected signal, stop line, and vehicle position.

1. **Compute the steering error.** Compare the lane-derived steering reference with a target of zero.
2. **Calculate the steering command.** Apply the PID controller to the error. The integral gain was set to zero, so the implementation used the proportional and derivative terms.
3. **Apply the intersection rules.** Brake when a red light and a stop line are detected in a configured intersection zone. At selected junctions, a yellow light reduces speed and a green light triggers the configured straight or turning maneuver.
4. **Send the vehicle commands.** Publish steering, motor speed, and brake state back to Unity through ROS 2.

## Contribution

I implemented the **lane, traffic-light, and stop-line perception nodes** and integrated them with the ROS 2 driving controller. I connected the simulator's camera and state inputs to steering, speed, and brake outputs, so the same system handled lane following and intersection decisions on the planned campus route.

</article>

{% include academic-page-styles.html %}

<style>
  .rvs-project-subtitle {
    margin: 0.65rem 0 0.15rem;
    font-size: 1rem;
    font-weight: 600;
  }

  .rvs-project-meta,
  .rvs-project-figure > figcaption {
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .rvs-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
  }

  .rvs-project-figure {
    margin: 1.5rem 0;
  }

  .rvs-project-figure > img,
  .rvs-project-figure > video {
    display: block;
    width: 100%;
    height: auto;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
  }

  .rvs-project-figure > figcaption {
    margin-top: 0.45rem;
  }

  .rvs-project-route {
    max-width: 42rem;
    margin-inline: auto;
  }

  .rvs-project-demo {
    max-width: 40rem;
    margin-inline: auto;
  }
</style>
