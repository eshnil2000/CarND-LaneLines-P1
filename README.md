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
[image3]: ./Solutions/solidYellowLeftOUTPUT.mp4

---
The Solution to this problem is outlined in the Jupyter Notebook: Term1_Assignment1.ipynb
[Term1_Assignment1](Term1_Assignment1.ipynb)
For easy viewing of the output images & video, an HTML file is available at [Term1_Assignment1](Term1_Assignment1.html)

The output images and videos from the processing pipeline can be found in the folder: 
[Solutions](Solutions)

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

Initially, I was getting shaky lane lines. This was due to 2 main reasons:
* 1. I didnt have any color detection algorithm built in to pick out yellow & white. I added in HLS filter to capture only yellow & whites, the results improved significantly.
* 2. In some of the frames, the lane lines were being dropped completely. I realized this happened when the lane lines were broken up and close to the bottom of the image. I decided to widen the ROI at the bottom of the image to include the entire X axis. This improved the results even more, as this is now picking up some of the small dashed lane lines at the bottom of the image. 

### 2. Identify potential shortcomings with your current pipeline

While the pipeline performance is good on still images and somewhat tolerable while detecting relatively straight to gently curving stretches of road in a video, This pipeline seems to  not perform as well on the Challenge video which has significant road curvature throughout the video. Looking at some of the heuristics I hard coded (like ROI), it seems if there is a significant upslope/downslope, this may throw off the lane detection pipeline. In situations like lane changes, the pipeline is not set up to handle such transitions. I didnt test the pipeline under darkness conditions, that may throw off some of the hard coded color detection via HLS.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to improve the line fitting algorithm so that the detected lane lines are smooth across video frames and of constant length.

Another potential improvement could be to enhance the basic fitting algorithm which fits to line equation to maybe fit to a polynomial which could potentially improve the performance of detection on significantly continuously curved lane lines.

Some of the hardcoded parameters like ROI, color ranges could be automatically tuned so that they can adapt to varying light and road conditions.


