---
layout: page
title: SLAM
description: Minor Project - Simultaneous Localization and Mapping (SLAM) Using Grid-Map and Particle Filter
img: assets/img/slam/slam.png
importance: 3
category: College Projects
---

<header>
    <h1>
        <a href="{{ '/assets/pdf/slam.pdf' | relative_url }}" target="_blank" rel="noopener noreferrer" class="float-right" style="color: grey; text-decoration: none;">
        <i class="fa-solid fa-file-pdf"></i>
        </a>
    </h1>
</header>

**Please refer to the entire thesis by clicking on the grey PDF button on the right.**

## Abstract

---

<div style="text-align: justify;">
    Simultaneous Location and Mapping (SLAM) is a method used to numerically solve the problem of extracting map and location in an unknown environment for Mobile robot navigation. It has been widely popular due to its wide range of applications in any sort of robot motion in an unexplored environment. Various approaches have been developed for tackling this problem like probabilistic approach, feature based, graph based and so on. We are using grid-map based approach derived from Tiny Slam that is enhanced with a layer of particle filter over it. The approach resulted in a improved map with less orientation errors and can encompass even greater robot motion speed. The robot motion however doesn’t encompass any control measures resulting in errors in map updates due to inertial jerk.
</div>
<div style="border: 10px solid transparent;"></div>

## Introduction

---

#### Navigation

<div style="text-align: justify;">
Navigating in unknown environments presents a unique set of challenges, primarily related to localization and mapping. The localization challenge involves determining the precise position of an entity within an unfamiliar area, while the mapping challenge focuses on creating an accurate representation of the environment. Simultaneous Localization and Mapping (SLAM) offers an iterative solution to these challenges, continuously updating its understanding of both position and environment. However, the process is often complicated by errors in motion and measurements, which can significantly impact accuracy. To address this, a probabilistic approach is employed, allowing for a more robust and flexible response to the uncertainties inherent in navigating unknown spaces. This approach helps in making more informed decisions based on the likelihood of different scenarios, enhancing the overall effectiveness of the navigation system.
</div>
<div style="border: 10px solid transparent;"></div>

#### TINY SLAM

<div style="text-align: justify;">
    TINY SLAM is a simple solution to the SLAM problem, designed for use on embedded platforms. It's quite small, with only about 200 lines of code, and is easy to understand.
</div>
<div style="border: 10px solid transparent;"></div>

#### MAP

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/slam/gridmap.png" class="img-fluid rounded z-depth-1"%}
    </div>
</div>

<div class="caption">
    Occupancy Grid Map
</div>

<div style="text-align: justify;">
    MAP is an Occupancy Grid Map used in navigation and mapping where each grid cell is assigned a probability. This probability, denoted as P(mi), represents the chance that the cell is not occupied. Initially, all grid cells are given a value of 0.5, indicating a neutral stance where it's equally likely for the cell to be occupied or unoccupied. This setup allows for a dynamic and probabilistic approach to understanding and mapping an environment.
</div>
<div style="border: 10px solid transparent;"></div>

#### Particle Filter

<div style="text-align: justify;">
    The Particle Filter is a probabilistic method used to provide the best estimation in systems like SLAM . It involves a process called resampling, which helps in refining the accuracy of the estimation. In this approach, each 'particle' represents a possible state, and these particles are evaluated based on their likelihood or the probability of being correct. The most probable particles are then more likely to survive and be carried over to the next generation of estimations. This method significantly improves the performance of existing SLAM systems by continuously updating and refining the understanding of the environment based on the probability of different scenarios.
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/slam/bwpf.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

<div class="caption">
    Particle filter in action
</div>
<div style="border: 10px solid transparent;"></div>

## Methodology

---

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/slam/systemdiagram.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    System Block Diagram
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/slam/messageflow.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    Flow diagram
</div>
