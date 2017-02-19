#**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./output/solidWhiteRight_output.jpg  "PipelineApplied"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps; 
* converted the images to grayscale
* applied canny filter on the grayscale images to get edges
* specified areas to focus on for the line detection
* applied Hough transformation to the images to detect and draw lines
* overlaid the lines onto the orginal image 

The following is one of examples of images applied the pipeline.
![alt text][image1]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function as below.
* Calculate the slope of each line and get the average of the slope. With an assumption that all of lines are part of left line or right line, categorize each slope to left line or right line.
* Then pick up the first point in the line list for each left line and right line, and draw a line going through the line with the average scope for each left and right line.


###2. Identify potential shortcomings with your current pipeline

Potential shortcomings are;
* The assumption used for drawline() that all of lines detected by the Hough transformation are part of either right line or left line is a big assumption and not very robust. Actually in "yellow.mp4", some wrong lines were observed. This is because the alogorhythm tried to draw a line against input line which is not the part of left line or right line.

* The solution is assuming that lanes are divided with lines and do not take curves into consideration. 

* Also the current implementation is weak against noises. For example, when this pipeline was applied to the "extra.mp4", it stopped with buffer overflow. This is because a vertical line with slope 0 was detected as a part of lane line and the algorhythm could not draw a line expanding from top to bottom with that slope.

###3. Suggest possible improvements to your pipeline

A possible improvement would be to optimize the parameter of filters and masks to focus on only target lanes. The current parameters are set after several try&errors, so the parameters should be optimized more. With more optimized filters, error detection should reduce.

Another potential improvement could be to add logic to ignore lines which do not seem to be part of left line or right line. It can be done by checking the difference among slopes of lines and dropping unusual ones, although the implementation could not cover this logic.
