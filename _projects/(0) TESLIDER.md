---
name: "TESLIDER: Autonomous Driving in KartRider"
permalink: /projects/teslider/
tools: [Python, OpenCV, Tkinter, Computer Vision]
image: /assets/img/projects/teslider/thumbnail.png
description: A vision-based driving prototype that uses game screenshots, lane detection, and automated keyboard input to navigate in KartRider.
videos:
  - title: Demonstration 1
    src: /assets/videos/projects/teslider/demo-1.mp4
    poster: /assets/img/projects/teslider/demo-1-poster.jpg
  - title: Demonstration 2
    src: /assets/videos/projects/teslider/demo-2.mp4
    poster: /assets/img/projects/teslider/demo-2-poster.jpg
  - title: Demonstration 3
    src: /assets/videos/projects/teslider/demo-3.mp4
    poster: /assets/img/projects/teslider/demo-3-poster.jpg
  - title: Demonstration 4
    src: /assets/videos/projects/teslider/demo-4.mp4
    poster: /assets/img/projects/teslider/demo-4-poster.jpg
---

<div class="academic-page teslider-project" markdown="1">

# TESLIDER

<p class="teslider-project-subtitle">Vision-Based Autonomous Driving in KartRider</p>
<p class="teslider-project-meta">2022 · Creative Convergence Project I · Team TESLIDER</p>

TESLIDER is a team project exploring how computer vision can connect game-screen observations to driving actions. Built with Python and OpenCV, the prototype captures the KartRider client window, detects lane markings, and generates keyboard inputs to steer the in-game vehicle.

<figure class="teslider-project-figure">
  <img src="{{ '/assets/img/projects/teslider/demo.png' | relative_url }}" alt="Four demonstration frames showing KartRider running beside the TESLIDER lane-monitoring interface" width="1440" height="810" decoding="async">
  <figcaption>Demonstration frames from the team's final presentation.</figcaption>
</figure>

## System Overview

The system combines screen capture, lane detection, driving control, and a monitoring interface. Python's `win32gui` locates the game window, `ImageGrab` captures its contents, and `ctypes` sends keyboard inputs. A Tkinter interface displays the perception and control outputs.

The implementation separates lane detection and keyboard input into modules and uses threads to run monitoring and control concurrently.

<figure class="teslider-project-figure">
  <img src="{{ '/assets/img/projects/teslider/architecture.png' | relative_url }}" alt="TESLIDER architecture showing lane detection and keyboard-input modules feeding driving control and the Tkinter interface" width="1440" height="810" loading="lazy" decoding="async">
  <figcaption>Module organization and the main components of the application.</figcaption>
</figure>

## Lane Detection and Steering

The perception pipeline turns the captured game image into line-slope estimates for steering:

1. **Select regions of interest.** Focus processing on relevant road regions in the original image and a bird's-eye view.
2. **Preprocess the image.** Apply Gaussian blur and convert the image to HSV color space.
3. **Extract lane colors.** Use HSV ranges intended to isolate yellow, white, and gray lane markings.
4. **Detect lane lines.** Apply Canny edge detection and a Hough transform to identify straight-line segments.
5. **Estimate slopes and steer.** Use line-slope estimates, with linear regression explored and applied during development, to select forward, left, or right keyboard inputs.

The controller uses threshold-based decisions and short steering-key presses. Its behavior depends on the quality of the detected lines and the selected slope thresholds.

<figure class="teslider-project-figure">
  <img src="{{ '/assets/img/projects/teslider/lane-detection.png' | relative_url }}" alt="Straight and curved KartRider road scenes paired with bird's-eye views and highlighted processing regions" width="1440" height="810" loading="lazy" decoding="async">
  <figcaption>Original game views and bird's-eye regions used for driving control.</figcaption>
</figure>

## Monitoring Interface

The Tkinter GUI shows left and right lane-monitoring views, the estimated driving state, and keyboard-input logs. The interface also includes Run, Off, and Reset buttons and monitoring checkboxes, although some button and checkbox bindings remained incomplete at the final presentation.

<figure class="teslider-project-figure">
  <img src="{{ '/assets/img/projects/teslider/interface.png' | relative_url }}" alt="Annotated Tkinter interface with lane views, driving-state logs, keyboard-input logs, and application controls" width="1440" height="810" loading="lazy" decoding="async">
  <figcaption>Monitoring interface and its intended controls.</figcaption>
</figure>

## Demonstration Videos

Four short clips from the project presentation show the prototype in operation alongside its monitoring interface.

<div class="teslider-project-video-grid">
  {% for video in page.videos %}
    <figure class="teslider-project-video">
      <video controls playsinline preload="none" poster="{{ video.poster | relative_url }}" width="1280" height="720" aria-label="{{ video.title | escape }}">
        <source src="{{ video.src | relative_url }}" type="video/mp4">
        Your browser does not support embedded video. <a href="{{ video.src | relative_url }}">Download {{ video.title | escape }}</a>.
      </video>
      <figcaption>{{ video.title | escape }}</figcaption>
    </figure>
  {% endfor %}
</div>

## Contribution

I developed the main lane-detection algorithm in Python and OpenCV. My work covered ROI selection, HSV color segmentation, Canny edge detection, and Hough-transform-based line detection to provide lane estimates for steering.

</div>

{% include academic-page-styles.html %}

<style>
  .teslider-project > h1 {
    margin: 0 0 0.65rem;
    font-size: 2.1rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .teslider-project-subtitle {
    margin: 0 0 0.35rem;
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.5;
  }

  .teslider-project-meta {
    margin: 0 0 1.5rem;
    color: var(--academic-muted);
    font-size: 0.85rem;
  }

  .teslider-project > h2 {
    margin: 2.5rem 0 1rem;
    padding-top: 1.25rem;
    border-top: 1px solid var(--academic-border);
    font-size: 1.4rem;
    font-weight: 700;
    line-height: 1.3;
  }

  .teslider-project li + li {
    margin-top: 0.45rem;
  }

  .teslider-project-figure {
    margin: 1.5rem 0;
  }

  .teslider-project .teslider-project-figure > img {
    display: block;
    width: 100%;
    max-width: 100%;
    height: auto;
    margin: 0;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #000;
  }

  .teslider-project-video-grid {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1.25rem;
    margin: 1.5rem 0;
  }

  .teslider-project-video {
    min-width: 0;
    margin: 0;
  }

  .teslider-project-video > video {
    display: block;
    width: 100%;
    height: auto;
    aspect-ratio: 16 / 9;
    border: 1px solid var(--academic-border);
    border-radius: 0.25rem;
    background-color: #000;
  }

  .teslider-project-figure > figcaption,
  .teslider-project-video > figcaption {
    margin-top: 0.5rem;
    color: var(--academic-muted);
    font-size: 0.8rem;
    line-height: 1.65;
  }

  @media (max-width: 767.98px) {
    .teslider-project-video-grid {
      grid-template-columns: minmax(0, 1fr);
    }
  }
</style>
