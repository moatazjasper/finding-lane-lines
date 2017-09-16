# **Finding Lane Lines on the Road** 
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw\_lines() function.

**My pipeline consisted of 6 steps**:

1. Converting the image to Greyscale.
2. Perform Gaussian Blurring on the Greyscale image.
3. Perform Canny Edge Detection after defining suitable low and high thresholds. I took John Canny's advice and made the ratio 1:2 .
4. Draw the polygon to corner down the area of interest in the image.
5. Define Hough Transform Parameters and Call its interface.
6. Draw resulting Hough Lines on the original image.

I combined my Pipeline in an interface/method called **pipeline\_interface()** so that it can be easily called to process both separate images and the videos without the overhead effort of tracking changes.

In order to draw a single line on the left and right lanes, I saved the old one as **draw\_lines\_original()** and modified the **draw\_lines()** function by creating an array of slopes and intercepts of the lines outputted by Hough Transform. Then I clustered highest and lowest slopes (supposedly left and right lines segments' slopes), then by averaging these slopes respectively, I could find one line for the left side and one line for right side, thusfar achieving what was requested.



### 2. Identify potential shortcomings with your current pipeline

The created left and right lines are still pretty much unstable. If a higher slope line appears (higher than the left lane line), the drawn left line will jump to it.


### 3. Suggest possible improvements to your pipeline

They need to be stabilized and consider lane width and position respective to the detection camera.
