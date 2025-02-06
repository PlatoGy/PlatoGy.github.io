---
layout: post
title: CV Workshop 7
author: Patrick Gao
date: 2025-02-06 14:00
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

## Workshop 7  

- Using the pygame library, the following video clip can be generated


## Step1: Identification
- Before being able to track the ball, we must identify it
- This mean learning its appearance
- Use (r, g) in the normalised RGB colour space




## Step 1: continued

- The PNG image for the colourful ball is on Blackboard
- Read the image, create an array for the (r, g) space
- For each pixel of the ball,  populate the array
- Normalise the (r, g) space to make it a probability density function (PDF)
- The PDF will be the colour model for your ball



## Step 2: extracting frames


- You are given a video clip for the ball bouncing in the constraint environment
- Extract all frames and save them in a FRAMES folder


## Step 3: tracking

- Using the alpha-beta tracker, track the ball throughout the video
- What you need to do is to detect where the ball is in the first frame
- The ball in the image should be the same size of the ball in the video and the frames
- So, you can use template matching to search for its first position
- You then define a bounding rectangle for the ball
- In the minimal alpha-beta tracker, you can use a fixed bounding rectangle, its position and a constant velocity


