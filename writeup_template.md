# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

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

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I apply Gaussian smoothing. 
Then I apply Canny transform. Then I apply an image mask. Last I modified draw_lines function and return images with hough lines drawn

I intially used the parameters used during tutorials. But there are multiple small noise lines near the road end. I tried to change the paramters such as threshold and max_line_gap. 
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculate the average of slope and intercept. Then use the upper left x,y and upper right x,y to get the bottom points. It works fine in most cases but it does not work for some images. So I add filter to only allow certain line to be included. I am using max_slope and min_slope as basic range and make sure the slope of line is within 20%.  

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming is because I am using max_slope and min_slope to identify the range. But for video like challenge. Because the curve of the road, the max_slope and min_slope is too wild and not accurate. So it only works good for nearly straight road.

Another potential shortcoming is I am using hard coded parameter such as min_line_len and max_line_gap, it does not work well for different resolution images. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use a dynamic number based on resolution for parameter related to pixel. 

Another potential improvement could be instead of using max_slope and min_slope. Using a median left slope and median right slope as central. Apply filter within 20% of those two slope. 
