# Toyota-Innovation-Challenge
An image recognition software that detects holes and failed stickers in the Toyota production process using neural networks and OpenCV. Languages and tools: Python, Javascript, OpenCV, YoloV5
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

We then tried to use the detectShapes function to find the contours of the image. However, the image was too complex and had to be simplified by the pointDetector function, which adds a filter to the image. At this point, our program could find the holes in static images. 
