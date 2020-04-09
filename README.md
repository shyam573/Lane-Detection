
# Detecting lane lines on road  

This project of lane detection is built as part of self-driving car nanodegree program of Udacity. The main of this project is to detect lane lines on the road using basic computer vision techniques.

## Pipeline
The pipeline of execution is as follows:
1. Conversion of color image to grayscale image
2. Applying Gaussian blur to that grayscale image and perform Canny edge detection
3. Form region of interest 
4. Get hough lines for that image
5. Draw solid lines using those obtained hough lines
6. Drawing the solid lines on to the original image

The image is initially converted to grayscale and then apply Gaussian blur to that image to detect edges better. Apply canny edge detection to detect edges by tuning low threshold and high threshold values. Obtain the suitable vertices to form a region of interest so that only edges in that region can only be used. Perform hough transform on that masked image to get good lines by tuning the hough parameters. Incomplete lines can only be obtained if hough lines are drawn directly onto the image. 


### Modification of draw_lines function
Solid lines can be drawn by using slope and intercept values of the hough lines. Lines are initially separated into left lines and right lines. Left lines are lines whose y-coordinate values decrease with increasing x-coordinate values and right lines are those whose y-coordinate values decrease with increasing x-coordinate values. After separating the lines, linear regression is performed on all the left lines and right lines separately to obtain slope and intercept values of the linear fit line using `stats.linregress` . For left and right lines, find the minimum value of y-coordinate possible and using the corresponding slope and intercept values to obtain x-coordinate values. Similarly, find the maximum possible value of y-coordinate which is nothing but image_y shape minus 1. Find the corresponding x-coordinate values using slope and intercept values for both lines. Using these points, draw left and right solid lines.

Alternately, the x and y coordinate values can be averaged., also slopes. Using slope, x and y value, intercept can be obtained. For minimum and maximum values of y-coordinate values for hough lines, same approach as explained above can be used. Then solid lines can be drawn with those obtained points.

## Drawbacks of this approach

1. This approach does not perform well when there are shadows on the lane lines or in other weather conditions.
2. This approach needs parameters to be tuned manually which is a hectic task and is really hard to obtain near-optimal parameters. 
3. The slope and intercept values are found using linear regression approach and it does not work well with curved lines.
4. If any vehicle obstructs the view, then lane lines cannot be obtained.

## Possible improvements
1. Drawbacks like shadow effects, view-obstruction, parameter-tuning and curved roads can be addressed using neural networks. Large amounts of suitable data with labels are required to use this method.
2. Alternately, non-linear curve fit or sliding window methods can be used to treat curved road methods.
