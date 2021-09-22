---
title: "SocialVR"
date: 2021-09-22T10:28:02+03:00
draft: false
---
This project started by thinking about the value of sharing
an experience. One can capture a proof of a spatial existence or a temporal state or a way to express their social
identities. One may ask then how will this be transferable to the virtual world where VR users can live similar
shareable experiences from game achievements to purely
visually fascinating scenes? To answer this question, I
decided to focus on a particular phenomenon that thrived
on social media: selfies. Selfie as a concept may look new
as it’s intrinsic to the emergence of social media, but I
can date back its origin to self-portraits but also to standard portraits. Self-portraits were based on this particular
idea of taking control of the take which makes the picture
an active action and a decision to create a content to be
shared. In portraits, I find a more elaborate “mise-enscène” which is an important aspect that we find also in
selfies.The selfie phenomenon is based on these two rules :
an active take in a special scene. I wanted our project to
be a way to transfer this mechanism to the virtual world.
By the immersive properties of VR, I can say that the
user is actually transported in space-and-probably time
and is living new experiences that are comparable to travelling and sightseeing and are at their core sharable to
everyone (VR-accustomed or not).
First of all, I am not using the regular OVRCameraRig
but OVRPlayerController, this gives us the ability to move
more freely in the scene, since the controller joystick can be
used. The player contains a head and also two controllers
are shown. The left one is the controller that he/she can
interact with and the right one contains the two displays,
one for the in-game feed and the web camera feed.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/SocialVR%20-%20In-game%20and%20Camera%20feed.JPG)
When the user takes a photo we need to find a way to display it. I use cannons to throw the photos in front of the
player. These cannons follow the player, always face his
direction and they are placed in a circular diameter.When
a photo is taken, then they fire their photos to appear in
front of him/her. The main theme in our scene is giants
and they are scattered throughout the area. Our application contains three main scenes that the user can interact
with, I will explain them going from the simplest one to
the most complex one. The first scene is called the Lava
Giant. There is a lava area that contains a Lava giant, although he may seem dangerous he is only carefully watching the user as he/she passes by. There is no interaction
with this scene, just the giant is moving his body the way
in the direction that the user walks. In the second scene,
magic happens, literally. The second area of our game is
the complete opposite of a lava area, it is a snowy area.
In this area, there is a skull that has flaming eyes. When
the user touches the skull with the left controller then a
series of particle effects start to appear. After they finish
a second skull giant appears and he is constantly casting
a magic spell.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/SocialVR%20-%20Giant%20casting%20spell.JPG)
The last scene is staged in an oasis. When the user sees
the oasis he/she can make out two things: A sword with
energy that is drawn in it and two giants facing each other.
One of them is an earth golem or the protector of the oasis
and the other one is a demon.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/SocialVR%20-%20Two%20gians%20classing.JPG)
