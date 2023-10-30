# Toyota-Innovation-Challenge
An image recognition software that detects holes and failed stickers in the Toyota production process using neural networks and OpenCV. 

Languages and tools: Python, Javascript, OpenCV, YoloV5

Link: https://colab.research.google.com/drive/1U448IPP_-P75PB83NxzppfkuUijySi_o?usp=sharing

DevPost: https://devpost.com/software/toyota-innovation-challenge

## Background:

Toyota is developing a system that will automatically install round stickers over vehicle body holes to prevent damage. The automated system will apply the individual stickers over the designated holes. Our goal is to design an inspection system to: 
1. Confirm the presence of all 7 stickers applied by the robot
2. Confirm the stickers fully cover the body holes
3. Confirm that the stickers are flush with the surface
4. The total inspection time for all 7 stickers should not exceed 15 seconds

## First attempts:

We first attempted to write code to find the holes in static images. To do this, we used the houghCircleDetector function in OpenCV to display circles over the holes. After changing the sensitivity parameters of the function, our code managed to find some holes in the image, but either found too many holes or too few holes. 

![Detect Circles](https://github.com/asyf16/Toyota-Innovation-Challenge/blob/2b89e1a95978d776624e5367fa786eb1f981b16c/Pictures/circle.png)


We then tried to use the detectShapes function to find the contours of the image. However, the image was too complex and had to be simplified by the pointDetector function, which adds a filter to the image. At this point, our program could find the holes in static images. 

![Filtered](https://github.com/asyf16/Toyota-Innovation-Challenge/blob/2b89e1a95978d776624e5367fa786eb1f981b16c/Pictures/filter.png)
![Contours](https://github.com/asyf16/Toyota-Innovation-Challenge/blob/2b89e1a95978d776624e5367fa786eb1f981b16c/Pictures/contour.png)

## Live feed:
After testing our code on static images, we attempted to connect to a live feed camera. Using Python and Java, we processed the output from the live feed and implemented our previous processes on the frames. We first use a point detection filter to simplify the image and then use a shape detection filter to find the holes and stickers. At this point, the program could recognize shapes that are similar to circles. 

![Holes](https://github.com/asyf16/Toyota-Innovation-Challenge/blob/e3bbd591aad2b738c0253d50b681905018f968d4/Pictures/image.png)

## Detect stickers: 

We stored the coordinates of the detected circles in an array. If the circle is not symmetric (the length and width are not the same within the margin of error), it is classified as a failed sticker. This works with a live video and in 3 degrees freedom. We then calculate the average radius of all circles, excluding the failed stickers. Circles with a radius less than the average are classified as a hole.

https://github.com/asyf16/Toyota-Innovation-Challenge/assets/144833617/eba978f1-0901-42a1-bbad-8e76ce6e5ed7

## Detect wrinkles:
Another challenge is to detect wrinkles in stickers. We are working on using houghLineDetection to find lines during the live stream. We plan to compare the coordinates of the lines found to see if they are inside any of the circles. If the lines are in the circles, the value of a boolean variable “inLine” will change and a "wrinkled" label will display on the screen. Currently, our program is able to find a list of the central coordinates of the wrinkles in the live stream.

Input:

![Screenshot (39)](https://github.com/asyf16/Toyota-Innovation-Challenge/assets/144833617/906920d2-fa30-4415-a21d-3ddbde63004b)

Output:

![Screenshot (40)](https://github.com/asyf16/Toyota-Innovation-Challenge/assets/144833617/27cd1147-e32e-4cb9-be96-527a8508dc01)

Coordinates:

[384.5, 414.0]

Live stream test:

![Screenshot (42)](https://github.com/asyf16/Toyota-Innovation-Challenge/assets/144833617/66042635-b969-413f-83ae-7b4d3151286f)

## Evaluation:

Our approach and scope changed throughout the challenge. We began by using filters and color space changes to identify the circles. We then switched to the Hough Circle Transform which worked adequately for single test images but could not be generalized without tuning its parameters. Our current solution leverages point and shape detection along with checking the size of the stickers to determine if we are looking at a hole, sticker, or partially covered hole. We are also attempting to solve the problem using YoloV5 and a Neural Network to recognize stickers. However, this requires a lot of training images. While our current solution works well, if we were to undertake this project again, we would work with a neural network from the start. It would serve as a more general solution and could be continually improved on by creating more layers and more training data.
