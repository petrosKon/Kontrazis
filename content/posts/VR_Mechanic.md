---
title: "VR_Mechanic"
date: 2021-09-20T08:42:22+03:00
featured_image: "/images/VR Engine.jpg"
draft: false
---

The main idea behind this project is the value that VR applications can offer for training purposes. We imagine that in the future, VR in combination with AR will be used in order to create training scenarios.
In our case we only use VR. The training scenario that we want the user to be accustomed to is the assembly and disassembly of an engine. For our example we are using this type of engine that is used mostly on
ships.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/VR%20Engine.JPG)
As I said in this scenario we need to train our user into the assembly and the disassembly of the engine. In order to create something like that we use something called a "Snap Zone". This "Snap Zone" functions 
as an area that indicates where a certain part fit or not. In order to integrate that to our application we used the **VRTK** plugin since it comes with many predefined objects especially concerning VR.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/VRTK%20Plugin.jpg)
The **VRTK** plugin is one of the most popular plugins for VR since it has many commonly used functionalities. In our project we use for the "Snap Zone" and as well as for the locomotion. In this VR project the locomotion technique
that we are using is teleportation. It is easy to integrate, since it is one of the most common in VR. The user is able to teleport using the right analog stick, select where he/she is going to land and according to how much he/she is rotating the 
stick, it determines how the user looks. The locomotion technique is similar to most techniques used in VR games, in order to avoid motion sickness.
In order for our teleportation to be effective, we added certain "targets" at the edges of our table. These targets serve as "cliping points" where the player is able to snap and teleport to.