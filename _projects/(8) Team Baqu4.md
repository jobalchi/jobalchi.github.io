---
name: "2022 International College Student Creative Car Contest"
year: 2022
permalink: /projects/baqu4-2022/
tools: [Autonomous EV, Computer Vision, ROS Noetic, Arduino]
image: /assets/img/projects/baqu4-2022/team.jpg
description: Team Baqu4's first autonomous electric race car combined camera-based cone detection, steering and braking control, and a dedicated safety system. The team received the Special Award.
videos:
  - name: test-run-1
    title: Nighttime test on a cone-marked course
    width: 1280
    height: 720
  - name: test-run-4
    title: Onboard view approaching the stop cones
    width: 1280
    height: 720
  - name: test-run-2
    title: Trackside view of a competition run
    width: 1280
    height: 720
  - name: test-run-3
    title: RBD-22 departing along the cone-marked course
    width: 720
    height: 1280
---

<article class="academic-page baqu4-project" markdown="1">

<header class="academic-page-header">
  <h1>2022 International College Student Creative Car Contest</h1>
  <p class="baqu4-project-subtitle">Autonomous Electric Vehicle</p>
  <p class="baqu4-project-meta">2022 · Hanyang University ERICA · Team Baqu4</p>
</header>

For its first autonomous-driving entry, **Team Baqu4** equipped its student-built electric race car, **RBD(Revolution of Baqu4 DriverLess)-22**, to follow a course marked by traffic cones and brake at the designated stopping area. The team integrated camera-based perception, steering and braking control, and the competition's required safety functions. Baqu4 competed on October 7–8 at the Korea Automobile Testing & Research Institute in Hwaseong and received the **Special Award** in the autonomous EV category.

<div class="academic-publication-links" role="group" aria-label="Project links">
  <a class="btn academic-publication-link" href="https://kjm045451.wixsite.com/baqu4" target="_blank" rel="noopener noreferrer" aria-label="Baqu4 team history (opens in a new tab)">
    <i class="fas fa-globe mr-1" aria-hidden="true"></i> Baqu4 Team History
  </a>
  <a class="btn academic-publication-link" href="https://www.kasa.kr/staticdata/static/society/history/" target="_blank" rel="noopener noreferrer" aria-label="Competition record (opens in a new tab)">
    <i class="fas fa-clipboard-list mr-1" aria-hidden="true"></i> Competition Record
  </a>
</div>

<figure class="baqu4-project-figure">
  <img src="{{ '/assets/img/projects/baqu4-2022/team.jpg' | relative_url }}" alt="Team Baqu4 members with RBD-22 outside the Hanyang University competition tent" width="1600" height="1200" decoding="async">
  <figcaption>Team Baqu4 and RBD-22 at the competition.</figcaption>
</figure>

## The Driving Tasks

The competition rules specified a **150-meter acceleration run** and a braking inspection from **at least 40 km/h** within a **6-meter stopping zone**. For the autonomous EV inspection, the car had to brake autonomously with a driver on board. Baqu4's system had to translate camera observations into steering commands while the car accelerated, then recognize the stop marker and command the brake actuator.

## Seeing the Course

The team prototyped lane detection in **OpenCV**, using a perspective transform, color filtering, a region of interest, and histogram-based sliding windows. The prototype processed images quickly, but its detections were sensitive to changes in the scene. The team also evaluated a pretrained **YOLOv3** cone detector and contour-based detection. One CPU configuration ran YOLOv3 at roughly 3 frames per second, while a test on an RTX 2070 Super approached 30 frames per second and detected most of the cones in the test footage.

Cone detections gave the team points from which to estimate the left and right course boundaries. **Ouster OS1-32 LiDAR** was investigated in parallel, with point clouds visualized in RViz and recorded to ROS bags. The post-competition review lists LiDAR integration as follow-up work.

<figure class="baqu4-project-figure baqu4-project-detection">
  <img src="{{ '/assets/img/projects/baqu4-2022/cone-detection.png' | relative_url }}" alt="Camera frame with detected cones, estimated left and right boundaries, and a blue reference line" width="337" height="398" loading="lazy" decoding="async">
  <figcaption>A cone-detection experiment showing the estimated course boundaries.</figcaption>
</figure>

## From Perception to Steering and Braking

The team compared two steering references. Using the **difference in boundary slopes** helped bring the vehicle toward the center, but repeated corrections could produce an S-shaped path. Using the **offset between the image center and the vanishing point** helped align the vehicle with the course, but could leave it too close to one boundary. The controller combined both signals, adjusted steering authority using wheel speed, and shaped the response with a hyperbolic tangent.

For the stopping task, the team used **HSV color filtering** to identify the designated stop cones. The braking logic required at least two cone detections beyond a threshold in the image before commanding the linear brake actuator.

## Vehicle Integration and Safety

The **Autonomous System Master Switch (ASMS)** controlled power to the autonomous steering and braking actuators. **ROS Noetic**, Python **rosserial**, and an **Arduino** connected the software to the vehicle's safety hardware. The system handled signals for the state-indicator LEDs, speaker, LoRa remote, and emergency-stop switches, with distinct indications for ready, driving, finished, and emergency states.

The post-competition ASMS review documented how concentrating communication and peripheral control on one Arduino complicated diagnosis. The team proposed moving some functions to dedicated controllers and documenting the wiring and circuits for emergency stop, the speaker, and manual mode.

<figure class="baqu4-project-figure">
  <img src="{{ '/assets/img/projects/baqu4-2022/vehicle.jpg' | relative_url }}" alt="RBD-22 on the marked competition course near the electric vehicle inspection tents" width="1600" height="900" loading="lazy" decoding="async">
  <figcaption>RBD-22 near the electric vehicle inspection area.</figcaption>
</figure>

## Test and Competition Footage

<div class="baqu4-project-gallery">
  {% for video in page.videos %}
    {% assign video_url = video.name | prepend: '/assets/videos/projects/baqu4-2022/' | append: '.mp4' | relative_url %}
    {% assign poster_url = video.name | prepend: '/assets/img/projects/baqu4-2022/' | append: '-poster.jpg' | relative_url %}
    <figure class="baqu4-project-figure">
      <video controls playsinline preload="none" poster="{{ poster_url }}" width="{{ video.width }}" height="{{ video.height }}" aria-label="{{ video.title | escape }}">
        <source src="{{ video_url }}" type="video/mp4">
        <a href="{{ video_url }}">{{ video.title | escape }}</a>
      </video>
      <figcaption>{{ video.title | escape }}</figcaption>
    </figure>
  {% endfor %}
</div>

## Contribution

I served as the team's **Autonomous System Responsible (ASR)** and developed the **Autonomous System Master Switch (ASMS)**. I integrated the ASMS with the autonomous driving software, state indicators, audible alerts, and emergency-stop modules so the vehicle could coordinate their behavior across ready, driving, finished, and emergency states.

</article>

{% include academic-page-styles.html %}

<style>
  .baqu4-project-subtitle {
    margin: 0.65rem 0 0.15rem;
    font-size: 1rem;
    font-weight: 600;
  }

  .baqu4-project-meta,
  .baqu4-project-figure > figcaption {
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .baqu4-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
  }

  .baqu4-project-figure {
    min-width: 0;
    margin: 1.5rem 0;
  }

  .baqu4-project-figure > img,
  .baqu4-project-figure > video {
    display: block;
    width: 100%;
    height: auto;
    margin: 0;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
  }

  .baqu4-project-figure > figcaption {
    margin-top: 0.45rem;
  }

  .baqu4-project-detection {
    max-width: 420px;
    margin-inline: auto;
  }

  .baqu4-project-gallery {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1.25rem;
  }

  .baqu4-project-gallery > figure {
    margin: 0;
  }

  .baqu4-project-gallery video {
    aspect-ratio: 16 / 9;
    object-fit: contain;
    background: #000;
  }

  @media (max-width: 767.98px) {
    .baqu4-project-gallery {
      grid-template-columns: minmax(0, 1fr);
    }
  }
</style>
