# **Finding Lane Lines on the Road** 

## Nilesh Shah

### 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps: 
#1. Convert image to grayscale
#2. Apply Canny edge detection to detect edge outlines
#3. Select the region of interest to limit to roughly the extent of lane lines in the image
#4a. Extract the hough lines, process the lines so that the Left Lane Line pieces are combined as 1 single solid line
#4b. Similarly process the Right Lane Lin pieces. This processing is done in the modified draw_lines function
#5. Overlay the processed Hough Lines onto the origina image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by doing the following:
-Divide the points of the lines into Left Lane & Right Lane lines based on their slope values (negative slopes=Left Lane)
-Fit a line equation to the left lane line points and another line to the right lane lines
-Start the Left Lane line from the bottom of the image (corresponding to the maximum Y value of the image, minimum X value of set of points) and end the line at roughly the midpoint of the image (corresponding to the maximum X value of the set of points, and calculating it's Y value based on the line fit equation)
-Repeat similar procedure for the Right Lane Line


If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]:./Solutions/solidYellowCurve.jpg "Lane Lines detected"


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
