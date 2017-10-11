
**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)
[image1]: ./image_process/grayscale.jpg "Grayscale"

[//]: # (Image References)
[image2]: ./image_process/binary.jpg "Binary"

[//]: # (Image References)
[image3]: ./image_process/gradient.jpg "Gradient"

[//]: # (Image References)
[image4]: ./test_images_output/solidYellowLeft.jpg "Result"

[//]: # (Image References)
[image5]: ./image_process/modified.jpg "Modified"
---

### 1. Reflection

My pipeline consisted of 4 steps. First, I converted the images to grayscale.

![alt text][image1]

Then I smoothed it by a Gaussian filter and applied fixed-level thresholding to a single-channel array (grayscale image) for removing a noise.

![alt text][image2]

I found a gradient image using a horizontal Sobel filter, which detects vertical edges more clearly.

![alt text][image3]

After image processing I determined a region of interest and put a mask removing redundant contours. Then I found lines that belong left and right lane lines on the road by Hough Transform. Using draw_lines() function I put these lines to the image.

![alt text][image4]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by dividing points of line segments identified with the Hough Transform to coordinates of left and right lanes. Then I found coefficients using 'np.polyfit' function to define full visible lane by a linear regression (y = ax + b).

![alt text][image5]


### 2. Identify potential shortcomings with my current pipeline

One potential shortcoming would be an impossibility of determining lane lines when there are shadows on the road or light changes.

Another shortcoming could be the determining lane lines incorrectly when the road changes a direction very often.


### 3. Suggest possible improvements to my pipeline

A possible improvement would be to use a non-linear regression instead of the linear regression for defining curve lane lines.

Another potential improvement could be an accumulation of the lane lines position from n-number of frames to 'predict' a line position when it's poorly distinguishable on the image.
