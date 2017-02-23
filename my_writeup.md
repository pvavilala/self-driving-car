#**Finding Lane Lines on the Road** 

[//]: # (Image References)

[image1]: ./output_images/allofthem.png "Different Stages Of The Pipeline"

---

**Finding Lane Lines on the Road**

This is the first project for Udacity's Self Driving Car Nano Degree. It was a very challenging experience and also a lot of fun. At every stage of this project- from setup to submission- I learnt something new which made it a very rewarding experience.
---

### Reflection

###1. The Pipeline


In the first step of my platform the image was converted to a grayscale representation. To perform this action the helper function provided in the notebook was used. This action changes the colors to a single dimension and makes it easier to identify lines.

The next stage in the pipeline was to perform gaussian blurring in order to reduce noise. After this Cany edge detection was performed to find the contours of the lines.

The fourth step of the pipeline was to determine a region of interest for the lane lines and mask everything else out. After many iterations i choose a polygon mask and used dynamic values as vertices (i.e the vertices are dependent on image dimensions)

The fifth step was to perform the Hough transformation to identify the lanes. After a few iterations I used a set of parameters which one of the instructors used and they worked well.

For improving the draw lines function (to create a single lane line on each side) I got a few ideas from the discussion forums. I describe the procedure as follows

* The Hough Lines contain the pair of points each line is represented by. Using these points the slope and intercept for each line can be calculated. The direction of the slope also tells us which lane line it is ( right or left). 

* After collecting the slope and intercepts for all the lines, the next step is to eliminate the outliers. All lines whose slope was more than 1 standard deviation away from the average slope of all the lines were eliminated. 

* After eliminating the outliers the average slope and average intercept for the remaining left side lane lines and remaining right side lane lines were calculated. These are now the lines we want.

* The intersection point of the two lane lines calculated above is calculated and lines were drawn from the intersection point to the bottom of the image.


![alt text][image1]
###2. Identify potential shortcomings with your current pipeline

There are a few shortcomings with my pipeline the most important one being that the code is a bit too rigid and has been trained to work for the given set of images. It will not work well with a different quality of images because a lot of the parameters have been hard coded.

The line markings are in white, I was unable to fix it show red lines. I believe the code in draw_lines is somehow causing this but I haven't been able to rectify it yet.

For the yellow lines video there is a lot of jitter, I believe this may be because I am being a bit too rigid in eliminating outliers when finding the average of the slopes


###3. Suggest possible improvements to your pipeline

Possible improvements are to fix the shortcomings referred to earlier. More fine tuning with other images could help the pipeline generalize better.
