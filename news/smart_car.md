---
layout: archive
title: The 16th National Smart Car Competition
---

Backward Links: [Interests & Skills](../_pages/interests&skills.md) / [About Me](../_pages/about.md) / [Education](../_pages/education.md) / [Research](../_pages/research.md)

### *Date*: 06/22/2021

The time I spent with my teammates on preparing the smart car competition is one of the most unforgettable experience during my stage of undergraduate. The experience not only equipped me with practical knowledge and skills, but also led us to find each other who had a common goal. After the competation, all os us become very good friends. You can also find a photo of us taken in our Undergraduate Graduation Ceremony in the first photo of [this page](../news/BA_gra.md).

In this page, I review the entire process of the competition and describe in detail the part I was responsible for. The rest parts are arranged as follows: first, I will introduce the task we are expected to complete in the competition, then the division of labor is given, third I will describe the basic function I should achieve and break down my responsibilities into smaller parts, and describe the goal of each part and the methods that I utilized, then a video of the whole process test is performed, finally, photos of our group and the certificate of the competation are shown.

<span id="jump_top"></span>

## Quick Links: 

+ [Task Description](#jump1) 
+ [Division of labor](#jump2)
+ [The Computer Vision Part](#jump3)
  + [Traffic light recognition and distance estimation](#jump3_1)
  + [Lane recognition](#jump3_2)
+ [Whole process test](#jump4)
+ [Our team and the certificate](#jump5)


## Task Description <span id="jump1"></span>

Our competition topic is aerospace intelligent logistics, and the task is transporting specially designed goods on a pre-built track. Fig.1 shows the schematic of the race track, and the smart car that we utilized is shown in the top left corner. As marked in Fig.1, the race track consists several parts of areas. In the preparation period, the smart car is place in the debug area, and two participants of the team are allowed to bring one laptop each to test and control the smart car remotely. Other three participants are set in the embarkation area, the delivery area and next to traffic light, respectively. The process of a whole circle can be summarized as: 
+ Place the smart car into the waiting area and wait for the start signal
+ The game begin. The car first go to the embarkation area and stop. The participant there load a cargo model on the car.
+ Move forward and stop in front of the stop line.
+ If the color of the traffic light is green or yellow, the car could simply go through this area. If the color is red, the car should wait until the traffic light turns green or yellow.
+ Pass the tunnel and speed bump and arrives the delivery area.
+ Stop for a while.The participant there unload the cargo model.
+ Keep going and get across the roadblocks to arrive at the start of the S road.
+ Pass the S road without touching the boundary lines (the redline and the blue line in Fig.1).
+ Move to the waiting area and a whole circle complete.

<img src="/news/smart_car_imgs/road.png">

#### Fig.1 The schematic of the race track and the utilized smart car 

It should be emphasized that the test and debug operation are only allowed in the preparation period. When the game start, no extra operation is allowed expect restarting. Thus, the smart car should move automatically during the entire match. The competition is based on a points system, and the actions that you can *get points* including: 
+ Move to the delivery area automatically (2 points),
+ Stop in the delivery area (2 points),
+ Pass the traffic light correctly (3 points),
+ Move to the delivery area (3 points),
+ Pass the roadblocks (2 points),
+ Pass the S road correctly (5 points),
+ Move to the waiting area (1 points).

The deduction items including: 
+ Pass the traffic light incorrectly or press the stop line when stopping (-3 points),
+ Press the boundary lines when passing the S road (-1 points).

The game last for a period of time, and you should accomplish as much circles as you can to gain more points. To meet all the requirements and accomplish the race, the car is equipped with a monocular camera on the head and a laser SLAM on the back, as shown in the top left corner of Fig. 1. We use the laser SLAM to construct the model of the race track before the game start and to measure the surrouding distance during the game to avoid the car crashing to the edge of the track. The pictures the camera takes are used to correct the movement locus during the S road and to decide whether the car should stop in front of the traffic light. An NVIDIA® Jetson Nano is used as the main control board to recieve messages from the laser SLAM and the camera and output conmmands to the motors. 

[Back to the top](#jump_top)

## Division of labor <span id="jump2"></span>

According to the competation goals and the basic constitution of the smart car, the whole task is divided into five parts corresponding to five members:
1. Debug and maintain the electrical and mechanical structure of the smart car
2. Light up the camera and process the pictures recorded during moving, and give proper messages to the main control board
3. Use the laser SLAM to construct the model of the race track before the game start, and to measure the surrouding distance during the game. Then send the distance information to the main control board
4. Recieve the messages from the camera and the laser SLAM, and use the messages to give motion orders to the motor to move the car correctly
5. Make a visual Interface on the laptop that can interact with the car, give orders to the car, and check the status of the car during the game

The part that I was responsible for is the second item, the computer vision part. Later, our group leader who was in charge of the laser SLAM and I also took over the forth item and solved the parts that were relevant to each of us.

[Back to the top](#jump_top)

## The Computer Vision Part <span id="jump3"></span>

During the competition, I was mainly responsible for the computer vision part, and it could then be divided into two tasks: traffic light recognition and distance estimation, lane recognition. The following two sections will discribe the details of the method utilized and show the results achieved. All the code in this part was accomplised in Python.

### Traffic light recognition and distance estimation <span id="jump3_1"></span>

To recognize the color of the traffic light, we should utilize the difference between them. The most obviouse difference is the color, and that was the scheme that we started with. But soon we found that the color of oringe and red were so close that sometimes the car would confuse them. Later we noticed that the position of the traffic light is also a feature that could be utilized. As long as we located the center of the green light and calculate its radius, other lights could then be found accordingly. As for judging which light is on, we simply use a threshold segmentation method, and the threshold value was pre-calibrated. 

Since the imaging sensor we used is a monocular camera, it is hard to estimate the distance without any prior. Hence, special QR code patterns with fixed size were installed below the traffic light, and the distance from the camera to the patterns could then be estimated. A picature of the result of the traffic light recognition and distance estimation is shown in Fig. 2. The first line shows the 3D distance (unit: cm), while the second line give the current color of the traffic light that is on.

<div align=center><img src="/news/smart_car_imgs/traffic_light.png" width="600"></div>

### <div align=center> Fig.2 The result of the traffic light recognition and distance estimation </div>

### Lane recognition <span id="jump3_2"></span>

We regarded the lane recognition as a image segment problem, and trained a neural network to solve it. The architecture of the utilized Unet++ is shown in Fig.3. The input of the network is a picture with the lane taken from the camera, and the output is a picture of a divided lane line. 

<div align=center><img src="/news/smart_car_imgs/Unet.png" width="600"></div>

#### Fig.3 The architecture of the utilized Unet++

To make the network effective and robust, we used about 1,300 image pairs taken from two different scens to train the network. After 50 epochs of training, the network was then installed on the car to recognize the lane in real time. A video of testing is shown in Video. 1. 

<video src="/news/smart_car_videos/test_line.mp4" autoplay="true" controls="controls" width="600">
</video>

#### Video.1 A video to show the result of lane recognition 

[Back to the top](#jump_top)

## Whole process test <span id="jump4"></span>

Here we exhibit a video recorded during our preparation for the competation. We can see that all the functions works correctly and the car accomplised a whole circle without any error.

<div align=center>
<video src="/news/smart_car_videos/test_whole.mp4" autoplay="true" controls="controls" width="600">
</video>
</div>

#### Video.2 Whole process test

[Back to the top](#jump_top)

## Our team and the certificate <span id="jump5"></span>

After a semester of effort, we finnaly won the first prize of the northern division. The following photos are the teams of our school and the certificate of mine. Our team is on the left of the first photo.

<img src="/news/smart_car_imgs/smart_car.png">

#### Fig.4 Our team and the certificate

[Back to the top](#jump_top)

Backward Links: [Interests & Skills](../_pages/interests&skills.md) / [About Me](../_pages/about.md) / [Education](../_pages/education.md) / [Research](../_pages/research.md)


