UDACITY SELF DRIVING CAR NANODEGREE PROGRAM:FINDING LANE LINES 

This is the first step in teaching a vehicle to visualize the environment where it has to ride.
The goal was to find the lan lines for this project.

1. The Approach:
   1.Firstly,i converted the image to HSV colorspace.

     It has advantage over Grayscale is that all the information is in the single channel which does not change with the changing lighting          conditions.

   2.Second step in this process is the use of GaussianBlur function.
     This helps in removing the noise and make the image smoothen.
     
   3.Masks for yellow and white as we have lane lines colored only as yellow and white.
     We apply masks on our image and try to remove everything else other  than the lane lines.
     
   4.Canny Edge Detection:
     Then edges are discovered by passing the image to the canny function.
     
   5.After the edges have been detected, only that portion of the image needs to be considered for further processing that has road lane          lines in view.
   
   6.Now that the image only has the canny edges for the lane lines portion and the rest of it blacked out, hough lines are drawn from those      detected edges.
   
   7.Now we will call  the dra_line() function to draw the lane lines from detected edges:
   
     a. To extrapolate the lines returned from the hough lines and create two single lines, two endpoints (x_min, y_min, x_max. y_max) for          the two lane lines and their corresponding slope values (positive_slope, negative_slope) and intercepts (positive_intercept,                negative_intercept) are needed. This forms the problem statement for the algorithm.
     b. The array of lines returned from the hough_lines() function is iterated upon and for each line, the slope is calculated and stored          in spearate arrays for positive and negative slopes.

     c. From whether the slope is positive or negative, it can be inferred if the line belongs to the left line of the lane or the right            line.

     d. To remove noisy lines pertaining to edges not belonging to any lane, but still within the lane area, a threshold is defined for the        value of the slope acceptable for the algorithm.

     e. For each line, the intercept is also calculated and stored.

     f. The y_max for both lane lines is the point at the bottom of the image, from where the lines start.

     g. The slope values for both lines can be calculated by taking the averages of the corresponding positive and negative slope values.           This also helps in removing some noise pertaining to the slope values.

     h. Similarly, the intercept for both lane lines can be calculated by taking the mean of the stored intercepts.

     i. The y_min can be found out by comparing all the y values in all the lines and taking the minimum value.

     j. Now x_min and x_max can be found out by just fitting all the peviously found parameters in an equation of the line.

     k. The lines can now be drawn over the lane lines.
   
2.Reflection:
     Use of HSV colorspace makes our pipeline more robust as now it can handle varying lighting conditions.
   
3.Shortcomings:
     lane lines are jittery so another Improvements can be made to the draw_line algorithm to make better use of information from previous frames of the video while processing.