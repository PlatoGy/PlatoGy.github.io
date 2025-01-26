---
layout: post
title: CV Workshop 4
author: Patrick Gao
date: 2025-01-26 22:00
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

## Workshop 4  

## Part 1: Smoothing filters (15 min)

- Revise the lecture where I introduced the Gaussian and other smoothing filters
- Check the filters implemented in the Pillow library
https://pillow.readthedocs.io/en/stable/reference/ImageFilter.html
- Implement code that uses BLUR, SMOOTH and SMOOTH_MORE
- Using Matplotlib, display all the results, including the original image you have used 



## Part 2: moving shape on an image (15 min)


- Please study the code provided in the next slide
- It makes use of the ipywidgets library, which provides interactivity
- Do implement code that moves a transparent rectangle on the image
- This will have to be controlled by two sliders, for horizontal and vertical movement


## Part 3: sliding filter (30 min)

- Use the code I provided in the previous slide
- This time, instead of having a transparent rectangle you will implement a sliding filter
- The two sliders will control the horizontal and vertical position of the sliding window
- The sliding window will be filtered, and the original image in the rectangular area will be replaced with the filtered pixels
- You can see how an image can be cropped using
https://learnopencv.com/cropping-an-image-using-opencv/#:~:text=There%20is%20no%20specific%20function,And%20it's%20done! 


## Part 4: edge filters (10 min)

- Study the edge filters implemented in the Pillow library
https://pillow.readthedocs.io/en/stable/reference/ImageFilter.html
- Using the code developed for the previous problem, use the sliding window to extract edge information in the moving window


## Part 5: Interest point detection (30 min)

- Go back to the lecture that covered the corner detectors
- Using the OpenCV library, study how corners can be extracted using the Harris function
https://docs.opencv.org/3.4/dc/d0d/tutorial_py_features_harris.html
- Run the Harris corner detector on the shape image
Implement Harris with the sliding window as described in the previous exercises
- Use the circle drawing function provided in OpenCV
https://www.geeksforgeeks.org/python-opencv-cv2-circle-method/  


