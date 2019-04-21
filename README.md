# Traffic_Counter

This project consists of applying computer vision techniques to develop a traffic counting system that can run on an Raspberrypi device with limited computational power.

a non-model based traffic counter was implemented in Python, using OpenCV to provide the necessary libraries to make the system work with BACKGROUND SUBTRACTION AND RUNNING AVERAGE Technique

Background subtraction is a method to detect movement based on the difference between the current frame of the video, and the empty background. This method requires that an image of the empty background is obtained before, which is not always available. With an empty background image, when a new frame appears, the computer can recognize if there has been any change.By taking the current frame and subtracting the background from it, pixel by pixel, the result will be a mask showing the changes. If the intensity of this mask surpasses a preset threshold, then it is considered as movement  This method also assumes that the camera is static, so that the only thing moving are the actual objects in movement.

One complication with this technique is the difficulty in obtaining an image of the background when there are no objects in the scene. Another problem is that background subtraction by itself is vulnerable to changes in the environment. For instance, as the day progresses, the lighting changes but the image of the empty background used as a reference is not being updated. As a result, every new frame will potentially be different enough that even if no object is moving, movement is detected

To deal with the problem of a constantly changing background, a different method was implemented: Running Average of the Background.This technique improves on background subtraction because an original empty background is not needed to make it work. Instead, every new frame is used to create a running average. The result is a mask that is more resistant to changes in the environment. Newer frames will change the average, and as a result, the background will be constantly adapting. However, this algorithm can have problems in situations  when an object stays in the background for a sufficiently long time and then leaves the scene. This will cause the object to be incorporated into the background

Steps : 
1.	Read the frame and convert it into grayscale to run the average of the background.The running average is obtained through OpenCV’s function cv.accumulateWeighted()

2.	The function cv2.absdiff() takes the background frame and the current frame and returns a new image consisting only of the pixels that changed. 

3.	The binary image is processed to eliminate noises using three OpenCV functions cv2.blur(), cv2.erode() and cv2.dilate().

4.	The next step in the process is to detect all the contours and finding the centroid of the bounding box.

5.	To decide how the counter should be increased, two points on the frame must be selected and a counter will be increased whenever an object crosses the line segment created by those points. 

