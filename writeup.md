# **Finding Lane Lines on the Road** 


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road

[//]: # (Image References)

[image_gray]: ./writeup_images/solidWhiteRight_gray.jpg "Grayscale"
[image_blur]: ./writeup_images/solidWhiteRight_blur.jpg "Blur"
[image_canny]: ./writeup_images/solidWhiteRight_canny.jpg "Canny"
[image_detected]: ./writeup_images/solidWhiteRight_detected.jpg "detected"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline
---
My pipeline consisted of 5 steps. 
1) First, I converted the input images to **grayscale**. It is easier to operate on one color(gray) than three (Red Green Blue).
![image in gray scale][image_gray]

2) Then I used gaussian filter to blur image. **Gaussian filter** is suppressing noise and spurious gradients what is advantage during edges detection.
![image blur][image_blur]

3) Next I used **Canny Edge Detection** algorithm. It helped me to determined where are lane lines on th road. 
![image canny][image_canny]

4) Next I determined a **region of interest mask** by creating tetragon on the image from canny edge detection algorithm. I did it to ignore other line detected in the image.

5) At the end I found all lines in the region of interest by Hough algorithm, splited the lines two two groups: left lane and rigtht lane. I determined a sloap and an intercept for the each lane by averaging coefficients for detected lines from Hough. I calculated end points of the lane linear functions in mask of interest and drew them to the original image.
![image][image_detected]

draw_lines2() functon
---
In order to draw a single line on the left and right lanes, I created  the draw_lines() function by ...





### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
