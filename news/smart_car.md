---
layout: archive
title: The 16th National Smart Car Competition
---

## *Date*: 06/22/2021

The time I spent with my teammates on preparing the smart car competition is one of the most unforgettable experience during my stage of undergraduate. The experience not only equipped me with practical knowledge and skills, but also led us to find each other who had a common goal. After the competation, except a member who didn't do anything, the rest four of us become very good friends. You can also find a photo of us taken in our Undergraduate Graduation Ceremony in the first photo of [this page](/news/BA_gra.md).

In this page, I will review the entire process of the competition and describe in detail the part I was responsible for. The rest parts are arranged as follows: first, I will introduce the task we are expected to complete in the competation, and figure out which part I was in charge of, second, I will break down my responsibilities into smaller steps, and describe the goal of each step and the methods that I utilized, then, a video of the whole-loop test is performed to show the achievement of our group, finally, photos of our group and the certificate of the competation are shown.

## Task Description

Our competition topic is aerospace intelligent logistics, and the task is transporting specially designed goods on a pre-built track. Fig.1 shows the schematic of the race track, and the smart car that we utilized is shown in the top left corner. 

<img src="/news/smart_car_imgs/road.png">

#### Fig.1 The schematic of the race track and the utilized smart car

As marked in Fig.1, the race track consists several parts of areas. In the preparation period, the smart car is place in the debug area, and two participants of the team are allowed to bring one laptop each to test and control the smart car remotely. Other three participants are set in the embarkation area, the delivery area and next to traffic light, respectively. After testing and debugging, the smart car will then placed into the waiting area to wait for the start signal. Once the game begin, the car first go to the embarkation area and stop for a while. The participant there then load a cargo model on the top of the car. Then the car continue moving forward and stop in front of the stop line. Whether the car should keep moving depends on the current color of the traffic light. If the color is green or yellow, the car could simply go through this area. If the color is red, the car should wait until the traffic light turns green or yellow. After that, the car pass the tunnel and speed bump and arrives the delivery area. It will stop for a while in this area and the participant there will unload the cargo model in the meanwhile. The car then keep going and get across the roadblocks to arrive at the start of the S road. In the S road area, the car should moving without touching the boundary lines (the redline and the blue line in Fig.1). Since there is a guide line in the middle of the S road, participants can use this guide line as a reference. After passing the S road, a whole circle is complete. 

It should be emphasized that the test and debug operation are only allowed in the preparation period, and when the game start, no extra operation is allowed expect restarting. Thus, the smart car should move automatically during the entire match. The competition is based on a points system, and the actions that you can get points including: move to the delivery area automatically (2 points), stop in the delivery area (2 points), pass the traffic light correctly (3 points), move to the delivery area (3 points), pass the roadblocks (2 points), pass the S road correctly (5 points), move to the waiting area (1 points). The deduction items including: pass the traffic light incorrectly (-3 points), press the boundary lines when passing the S road (-1 points). The game last for a period of time, and you should accomplish as much circles as you can to gain more points.





## The Computer Vision Part


### Traffic light recognition and distance estimation


<img src="/news/smart_car_imgs/traffic_light.png" width="500"/>


### Lane recognition


<img src="/news/smart_car_imgs/Unet.png" width="500"/>


https://github.com/user-attachments/assets/03e4ecc3-9eb0-4c74-91b5-f68ad660a289

## Whole loop test


https://github.com/user-attachments/assets/b7304829-a17c-441c-bbd5-a186440ad3b0


## Our group and the certificate



<img src="/news/smart_car_imgs/smart_car.png">



