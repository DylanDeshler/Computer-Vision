# Introduction
I initially tried using DETR to count the number of planes in an image, but that failed hilariously, see below. I figured I would need to pick more in distribution images to get good results, so instead I decided to count the number of people in a bar. I chose this because it would be a simple and nifty application for tracking popularity/activity of a bar overtime and in comparisson with other bars. It would be simple to set up a camera in the bar (given permission) or outside facing the door.

<img src="failed_planes.png" alt="drawing" width="512"/>
It detects 7 cars, 1 airplane, and 1 person 1.

,Below is an examples it misses one person (incorrectly counting two people as one), but generally its reasonablly accurate.

<img src="people_bar_1.png" alt="drawing" width="512"/>


