---
layout: page
title: Structure from Motion (SfM) 
description: 3D reconstruction using SfM
img: assets/img/sfm1.jpeg
importance: 2
category: Other Projects
---
Structure from Motion (SfM) is a computer vision technique for reconstructing 3D structures from 2D image (sequencial and non-sequencial) . This project demonstrates the end-to-end pipeline for SfM, including feature detection, camera pose estimation, triangulation, and 3D point cloud generation with code, mathematical representation and open source alternatives.

<div class="row">
    <div class="col-xl mt-3 mt-md-0">
        <div class="embed-responsive embed-responsive-16by9">
            {% include video.liquid path="https://www.youtube.com/embed/x0KW0VWS5S4" class="img-fluid rounded z-depth-1" controls=true %}
        </div>
    </div>
</div>

## Steps
The following steps are typically used in standard structure from motion.

1. Camera Model
2. Feature Detection
3. Feature Matching
4. Fundamental Matrix Estimation
5. Essential Matrix Estimation
6. Triangulation
7. Bundle Adjustment
8. Sparse Point Cloud
9. Dense Reconstruction

---

## 1. Camera Model
It is a mathematical representation that describes how a 3D point in the world is projected onto a 2D image plane.
Simple **pinhole camera model** is represented by following mathematical formula:

$$
\mathbf{x} = K [R \,|\, t] \mathbf{X}
$$

Where:
- $$ \mathbf{x}$$: 2D point in the image (in homogeneous coordinates).
- $$ K $$: Intrinsic camera matrix (focal length, principal point).
- $$ R, t $$: Camera rotation and translation (extrinsic parameters).
- $$ \mathbf{X} $$: 3D point in the scene.

---

## 2. Feature Detection
Feature Detection can be defined as involves identifying unique, stable points or regions in an image that can be reliably matched across different views or frames. It  is crucial because it provides the "landmarks" or "anchors" within the image that can be matched with other images. The goal is to find points that are distinct, robust under transformations (like rotation, scaling, and lighting changes), and can be reliably tracked across multiple views.
Typically three types of Features matching are there:
1. Keypoints
2. Descriptors
3. Regions of Interest(Rols)

It detects feature points $$ \mathbf{x}_i $$ in each image using algorithms like Scale-Invariant Feature Transform (SIFT),Speeded Up Robust Features (SURF) and Oriented FAST and Rotated BRIEF (ORB).

---

## 3. Feature Matching
Once featuresare detected across several images taken from different viewpoints., the next step is to match them across images. This is where the descriptors come in, as they uniquely identify the features.
- Match descriptors $$ \mathbf{x}_i \leftrightarrow \mathbf{x}_j $$ between image pairs.
- Use a similarity metric (e.g., Euclidean distance, K-D Tree - a binary tree structure) to find correspondences.
- Filter out outliers using techniques like RANSAC.

---

## 4. Fundamental Matrix Estimation
The **Fundamental Matrix** $$ \mathbf{F} $$ satisfies the epipolar constraint:

$$
\mathbf{x}_j^T \mathbf{F} \mathbf{x}_i = 0
$$

To estimate $$ \mathbf{F} $$:
1. Use the **eight-point algorithm**:
   - Construct a linear system from matched points.
   - Solve $$ \mathbf{A} \mathbf{f} = 0 $$, where $$ \mathbf{f} $$ represents entries of $$ \mathbf{F} $$.
2. Enforce the rank-2 constraint on $$ \mathbf{F} $$ by applying Singular Value Decomposition (SVD).

---

## 5. Essential Matrix Estimation
The **Essential Matrix** $$ \mathbf{E} $$ is derived from $$ \mathbf{F} $$ and camera intrinsics $$ K $$:

$$
\mathbf{E} = K^T \mathbf{F} K
$$

Decompose $$ \mathbf{E} $$ into relative rotation $$ \mathbf{R} $$ and translation $$ \mathbf{t} $$:

$$
\mathbf{E} = \mathbf{R} [\mathbf{t}]_\times
$$

Where:
- $$ [\mathbf{t}]_\times $$ is the skew-symmetric matrix of $$ \mathbf{t} $$.
- Solve using SVD of $$ \mathbf{E} $$.

---

## 6. Triangulation
For each matched feature pair, compute the 3D point $$ \mathbf{X} $$ by solving:

$$
\mathbf{A} \mathbf{X} = 0
$$

Where:

$$
\mathbf{A} = 
\begin{bmatrix}
\mathbf{x}_1 \times P_1 \\
\mathbf{x}_2 \times P_2
\end{bmatrix}
$$

Solve for $$ \mathbf{X} $$ using SVD.

---

## 7. Bundle Adjustment
Refine camera parameters $$ \{K, R, t\} $$ and 3D points $$ \mathbf{X} $$ by minimizing the **reprojection error**:

$$
\min_{K, R, t, \mathbf{X}} \sum_{i,j} \| \mathbf{x}_{ij} - \pi(K, R_j, t_j, \mathbf{X}_i) \|^2
$$

Where:
- $$ \mathbf{x}_{ij} $$: Observed 2D projection of 3D point $$ \mathbf{X}_i $$ in image $$ j $$.
- $$ \pi $$: Projection function using the camera model.

Solve using non-linear least squares methods like the **Levenberg-Marquardt algorithm**.

---

## 8. Sparse Point Cloud
Combine triangulated points $$ \mathbf{X} $$ into a **sparse point cloud** representing the scene.

---

## 9. Dense Reconstruction (Optional)
To densify the sparse point cloud, use **Multi-View Stereo (MVS)** to estimate depth $$ z $$ for every pixel by minimizing:

$$
z = \arg \min_z \sum_i \| I_i(u, v) - I_j(\pi(u, v, z)) \|^2
$$

Where:
- $$ I_i $$: Image intensity at a pixel.
- $$ \pi(u, v, z) $$: Projected pixel location in another image.

---







