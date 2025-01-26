---
layout: post
title: CV Workshop 3
author: Patrick Gao
date: 2025-01-23 14:18
categories:
  - MISCADA
  - CV Course
tags:
  - Term 2 Assignment
mermaid: true
math: true
pin: false
---

# MISCADA – computer vision

## Workshop 3  
### Colour segmentation

# Normalise the RGB values

- Please refer to [https://en.wikipedia.org/wiki/Rg_chromaticity](https://en.wikipedia.org/wiki/Rg_chromaticity)
- For a colour image of your choice
  - Scan all the pixels
  - For each pixel normalize its value
  - Use only the r and g normalised values
- Using Matplotlib, display the pixels in the [r,g] space

# Implement the K-means

- This clustering algorithm is available, however I want you to develop your code for it, it is very simple
- To test the implementation use 200 random points in a 2D space with positive coordinates and no larger than 100

## Steps
- Initialise K centres
- While centres change or a number of cycles have elapsed
  - Assign each pixel to the closest centre
  - Recalculate the centres using mean value

# Normalised RGB space clustering

- Use the K-means algorithm to cluster a colour image
- Assume 4 colours
- Initialise the K centres at random in the [r,g] space
- Using Matplotlib, display the centres at initialization and at convergence
- Once the algorithm converged, colour image pixels using the 4 clusters
- Using Matplotlib, display original colour image and the clustered image

# YUV space

- Using the K-means, cluster in the [u,v] space and image of your choice
- Follow the instructions from the previous slides and display the original colour image and the clustered one

# Assessing your implementation

- To assess your implementation, you can use the available K-means algorithms
- It is readily available in the SciPy library
- [SciPy K-means Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.vq.kmeans.html)
- Do implement clustering in [r,g] and [u,v] using the SciPy K-means and then compare with your implementation
