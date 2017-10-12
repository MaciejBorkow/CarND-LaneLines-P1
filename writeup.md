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

4) Next I determined a **region of interest mask** by creating a tetragon on the image from canny edge detection algorithm. The tetragon covered a road region where I wanted to detect lanes. I did it to ignore other line detected in the image.

5) At the end I found all lines in the region of interest by **Hough algorithm**, splited the lines into two groups: left lane and rigtht lane. I determined a sloap and an intercept for the each line in one group and then calculated average for these two coefficients. Then I had formula of linear function for he left and rigt lane. I calculated end points of the **lane linear functions** in mask of interest and drew them on the original image.
![image][image_detected]

draw_lines2() functon
---
In order to draw a single line on the left and right lanes, I created  **the draw_lines2()** function by:

1) Splitting all lines dected with Hough function into two groups a left lane and a right lane. I did it by calculating slope for each line and then fit to the on gorupe. If slope was grater than 0 it went to the right lane group otherwise to the left lane group. I added restriction on the slope value to remove missmatch lines.

linear function:
$$y = slop*x + intercept$$
slope equation:
$$slope = (y2 - y1) / (x2 - x1)$$
intercept equation:
$$intercept = (x1 * y2 - x2 * y1) / (x1 - x2)$$

2) I calculated slope and intercept for each line in the groupe and averaged this two coefficients in the groupe.
3) Then I determinet lane linera functions formula for the each grupe.
4) I calculated end points for the each lane in area of interst where lane were on the road.
5) I drew this line in the origanl image. 


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when we wante to do sharp turn. The algorithm will not detect lanes on the sides.

Another shortcoming could be where there is no lane on the road. 

Next one shortcoming could be there where new line are painted on the old one. It could have proble with detection wich one is the dominate.

Another shortcoming is detection lane on the briht road.



### 3. Suggest possible improvements to your pipeline

A possible improvement would be to takes only Red and Green color in turning into gray scale. Yellow color is composed from red and green color in RGB color model.

Another potential improvement could be dynamic change a region of interest. One line could be determined by line of the horizon.


