# **Finding Lane Lines on the Road** 
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw\_lines() function.

**My modified pipeline consisted of 8 steps**:

1. Converting the RGB image to HSL color space.
2. Masking the HSL image to detect white and yellow pixels.
3. Converting the masked image to Grayscale.
4. Perform Gaussian Blurring on the Grayscale image.
5. Perform Canny Edge Detection after defining suitable low and high thresholds. I took John Canny's advice and made the ratio 1:2 .
6. Draw the polygon to corner down the area of interest in the image.
7. Define Hough Transform Parameters and Call its interface.
8. Draw resulting Hough Lines on the original image.

I combined my Pipeline in an interface/method called **pipeline\_interface()** so that it can be easily called to process both separate images and the videos without the overhead effort of tracking changes.

In order to draw a single line on the left and right lanes, I modified the **draw\_lines()** function as follows:
1. Creating an array of slopes and intercepts of the lines outputted by Hough Transform using a method **get\_lines\_slope_intercept()**.
2. Defining maximum and minimum slopes.
3. Clustering the highest and lowest line segments slopes (within tolerance with maximum and minimum slopes values) making two clusters for right and left lane lines.
4. Averaging these slopes respectively, and interpolating upon it to draw one line for the left lane line and one line for right lane line, thus achieving what was requested.



### 2. Identify potential shortcomings with your current pipeline

The created left and right lines are still pretty much unstable. If a higher slope line appears, that wasn't filtered by color selection, (higher than the left lane line), the drawn left line will jump to it. Same goes for the right lane line.


### 3. Suggest possible improvements to your pipeline

1. Lane overlays need to be stabilized and consider lane width and position respective to the detection camera.
2. Second degree polynomial needs to be implemented for curve fitting.
