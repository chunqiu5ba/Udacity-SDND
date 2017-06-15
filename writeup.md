# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[./test_images_output]: # (Image References)

[image1]: ./test_images_output/y2w_solidYellowLeft.jpg "Yellow to White"
[image2]: ./test_images_output/gray_solidYellowLeft.jpg "Gray"
[image3]: ./test_images_output/edges_solidYellowLeft.jpg "Edges"
[image4]: ./test_images_output/mask_solidYellowLeft.jpg "With Mask"
[image5]: ./test_images_output/line_solidYellowLeft.jpg "Line"
[image6]: ./test_images_output/solidYellowLeft.jpg "Finished"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. 

First, To handle the challenge task, I changed the yellow lane to white color
![alt text][image1]
Then, I converted the images to grayscale. 
![alt text][image2]
Next, I did gaussian smoothing, and canny edge detection.
![alt text][image3]
Then masked out the unwanted areas with a four sided polygon; 
![alt text][image4]
Run Hough Treansform on edge detected image is the next step
![alt text][image5]
Finally combine the line image with its oringinal footage
![alt text][image6]

In order to draw a single line on the left and right lanes, I used np.linalg.lstsq in scipy library to fit detected canny into a line on the single image, then saved the results to a global variables. I used the average from last 30 results to decide the line slope, intercept of the line, drew it on the original image. This will smooth the line movement on the final video.



### 2. Identify potential shortcomings with your current pipeline

In the challenge vedio, there are drmastic light/shade changes on the road thus yellow lane is hard to be detected. This prgram didn't always on the target yellow lane. I have tried serveal approaches including: Histograms Equalization, Dark the image, "Smart Canny" which hi-low trashold based on the computed median of the image. Those options and combination of options didn't turn out to be very helpful.

Also when there is a sharp turn on the road, extrapolating lines may not function well


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use scipy.optimize.curve_fit to handle turns on the road.

Another potential improvement could be fine tunning the yellow to white fuction, to pick up the yellow lane more accurate in the challange vedio.
