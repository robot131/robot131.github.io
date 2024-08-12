---
layout: archive
title: The 16th National Smart Car Competition
---

## *Date*: 06/22/2021

The time I spent with my teammates on preparing the smart car competition is one of the most unforgettable experience during my stage of undergraduate. The experience not only equipped me with practical knowledge and skills, but also led us to find each other who had a common goal. After the competation, except a member who didn't do anything, the rest four of us become very good friends. You can also find a photo of us taken in our Undergraduate Graduation Ceremony in the first photo of [this page](/news/BA_gra.md).

In this page, I will review the entire process of the competition and describe in detail the part I was responsible for. The rest parts are arranged as follows: first, I will introduce the task we are expected to complete in the competation, and figure out which part I was in charge of, second, I will break down my responsibilities into smaller steps, and describe the goal of each step and the methods that I utilized, then, a video of the whole-loop test is performed to show the achievement of our group, finally, photos of our group and the certificate of the competation are shown.

## Task Description

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

The game last for a period of time, and you should accomplish as much circles as you can to gain more points.





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



