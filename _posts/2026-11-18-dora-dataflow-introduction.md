---
title: "Dora: Building Robotics and AI Pipelines with Dataflows"
date: 2026-11-18 00:00:00 +0900
permalink: /blog/dora-dataflow-introduction/
tags: [Robotics, Dora, Dataflow, Rust, Autonomous Driving]
style: fill
color: primary
description: A brief introduction to Dora's Rust-based dataflow framework, core features, and potential applications in autonomous driving.
---

**Dora** is a Rust-based framework for building robotics and AI applications as **dataflows**. It separates functions such as sensor input, inference, planning, and control into nodes, with explicit connections describing how data moves between them. [Official website](https://dora-rs.ai/)

## Organizing a Dataflow

An autonomous driving pipeline could be organized as follows:

```text
Camera / LiDAR → Perception → Planning → Control
```

Dora can describe these connections in YAML. Each node declares its program, inputs, and outputs, and subscribes to outputs from other nodes. This makes the pipeline structure explicit alongside the individual algorithms. The [GitHub README](https://github.com/dora-rs/dora#dataflow-configuration) provides configuration examples.

## Key Features

- **Shared memory and Apache Arrow** reduce copying and serialization overhead between nodes on the same machine, which is relevant to large payloads such as images and point clouds.
- **Multi-language nodes** let Rust, Python, C, and C++ components share a dataflow, connecting AI models with processing modules written in other languages.
- **Distributed execution** supports communication across machines through Zenoh, alongside local node communication.
- **Record and replay** captures dataflow messages for repeated algorithm evaluation using recorded inputs.

The [official feature documentation](https://github.com/dora-rs/dora#features) describes the supported capabilities and their usage.

## Potential Applications in Autonomous Driving

A possible application is connecting camera and LiDAR inputs to a perception model, then passing its outputs to prediction and planning modules. Dataflows could also describe the connections between a simulator, a learned policy, and a controller.

A practical evaluation could start with a small **sensor input → inference → visualization** pipeline. Measuring communication latency, end-to-end processing time, memory usage, and format-conversion costs would help assess its suitability for a particular workload. These are application ideas to explore experimentally.

## References

- [Dora official website](https://dora-rs.ai/)
- [dora-rs/dora GitHub repository](https://github.com/dora-rs/dora)

