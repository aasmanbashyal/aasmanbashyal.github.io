---
layout: page
title: Gaussian Splatting 
description: 3D reconstruction using Gaussian Splatting
img: assets/img/gaussian.gif
importance: 3
category: Other Projects
---
Gaussian splatting is a modern technique introduced recently in computer graphics and 3D rendering. It represents 3D data, such as point clouds, by "splatting" smooth, bell-shaped curves known as **Gaussians**.  This method helps to create soft and realistic renderings with less computational cost compared to traditional methods, like meshes.

The key advantage of Gaussian splatting is that it allows for smooth, continuous transitions between points in 3D space, which is especially useful for rendering high-density data or visualizing volumetric structures.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <div class="embed-responsive embed-responsive-16by9">
        {% include video.liquid path="https://www.youtube.com/embed/-6xx_EPm7YA" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
        </div>
    </div>

</div>

## Steps of Gaussian Splatting

### 1. Data Collection

First, you need a **point cloud** or 3D data that you want to represent with Gaussians. A point cloud is a set of points in space, usually collected from sensors, such as LiDAR, cameras, or scanners.

### 2. Preprocess the Point Cloud

- Clean the data to remove any **noise** or **outliers** (incorrect or extreme data points).
- If needed, **downsample** the data, meaning reduce the number of points so that the rendering process is more manageable.

### 3. Define the Gaussian Function

For each data point in the point cloud, define a Gaussian function. A Gaussian function in 3D can be written as:

$$
G(x) = \exp\left(-\frac{(x - \mu)^T \Sigma^{-1} (x - \mu)}{2}\right)
$$

Where:
- $$ \mu $$ is the **mean** or center of the Gaussian (the location of the data point),
- $$ \Sigma $$ is the **covariance matrix** that determines the shape of the Gaussian (how spread out or narrow it is),
- $$ x $$ is the 3D point in space.

The covariance matrix controls the **width** and **orientation** of the Gaussian splat. If the covariance is small, the splat will be narrow and sharp; if it is large, the splat will be broader and softer.

### 4. Splatting Process

For each point in the point cloud, "splat" the Gaussian over the 3D space. This means that the function is placed around each point, covering its surrounding area. The Gaussian function’s intensity (height) can also be adjusted, allowing you to control how strong each splat is.

### 5. Blending Overlapping Gaussians

When Gaussians from different points overlap, you need to blend them together. The simplest way to do this is to **add** their values. If two Gaussians overlap, their intensities are combined:

$$
G_{\text{total}}(x) = \sum_{i=1}^{n} G_i(x)
$$

Where:
- $$ G_i(x) $$ represents the Gaussian for the $$ i $$-th point,
- $$ n $$ is the total number of points in the cloud.

This blending creates smooth transitions between neighboring points, resulting in a soft and continuous representation of the 3D data.

### 6. Rendering the Scene

After splatting the Gaussians, you can **render** the scene by tracing rays or using a volume rendering technique. The contribution of each splat to the final image depends on factors like the view direction, light, and camera position.


### 7. Optimization 

For very large datasets, optimizations can be applied to improve performance:
- **Hierarchical splatting**: Use multiple levels of detail, where more detailed splats are used for close-up views and less detailed ones for faraway views.
- **Adaptive Gaussian sizes**: Change the size of the splats depending on the scene’s complexity or the distance to the camera.


