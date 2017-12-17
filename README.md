# **Finding Lane Lines on the Road** 

## Nilesh Shah

### 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image2]: ./Solutions/solidYellowCurve.jpg "Grayscale"
[image3]: ./Solutions/solidYellowLeftOUTPUT.MP4

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps: 
* #1. Convert image to grayscale
* #2. Apply Canny edge detection to detect edge outlines
* #3. Select the region of interest to limit to roughly the extent of lane lines in the image
* #4a. Extract the hough lines, process the lines so that the Left Lane Line pieces are combined as 1 single solid line
* #4b. Similarly process the Right Lane Lin pieces. This processing is done in the modified draw_lines function
* #5. Overlay the processed Hough Lines onto the origina image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by doing the following:
*  -Divide the points of the lines into Left Lane & Right Lane lines based on their slope values (negative slopes=Left Lane)
*  -Fit a line equation to the left lane line points and another line to the right lane lines
*  -Start the Left Lane line from the bottom of the image (corresponding to the maximum Y value of the image, minimum X value of set of points) and end the line at roughly the midpoint of the image (corresponding to the maximum X value of the set of points, and calculating it's Y value based on the line fit equation)
*  -Repeat similar procedure for the Right Lane Line

This is an example output image with Lane Lines detected by the pipeline:
![alt text][image2]

### 2. Identify potential shortcomings with your current pipeline
One potential shortcoming is the Draw Lines function implementation. When testing the pipeline on video files, the pipeline shows erratic lines in a few of the frames due to the basic nature of the line fitting algorithm I used. It does not maintain continuity from one frame to another.

While the pipeline performance is good on still images and somewhat tolerable while detecting relatively straight to gently curving stretches of road in a video, This pipeline seems to  not perform as well on the Challenge video which has significant road curvature throughout the video.

An example of pipeline deployed on video:
![alt text][image2]



### 3. Suggest possible improvements to your pipeline

A possible improvement would be to improve the line fitting algorithm so that the detected lane lines are smooth across video frames. 

Another potential improvement could be to enhance the basic fitting algorithm which fits to line equation to maybe fit to a polynomial which could potentially improve the performance of detection on significantly continuously curved lane lines.
