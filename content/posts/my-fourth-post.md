---
title: "VR Roll-A-Ball"
date: 2020-12-09T14:11:36+02:00
draft: true
---

The next part of our lab is to extend the roll a ball game into a VR Project where the user is able to grab the whole configuration and play it as a stationary roll a ball game (like the toys, the kids used to play).
First up, we export the roll-a-ball project that we just made into a **UnityPackage** file so that we can import it into our new project.
Then we create a new project and import the package we just created, the package will implement all the assets as well as functionallity of our previous game.
The first thing we are going to do next is import the **Oculus Intergration** from the Asset Store that comes with all the things that we want to build our project in VR. Then we proceed to import our **Roll-A-Ball UnityPackage** into our project.
After that we drag and drop and **OVRCameraRig** into our project and we and we open the tree and we put the left and right controller in below the **LeftHandAnchor** and **RightHandAnchor**

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Added%20Controller.PNG "Added controllers")

Then we change our canvas to **World Space** so it is rendered as a 3D object in order for our user to see it.

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Canvas%20World%20Space.PNG "Canvas World Space")

Then we proceed to attach the colliders as well as rigidbodies in each object, so that the user can pick up the whole roll-a-ball board. We add a collider to our roll-a-ball and we also add a layer marked as Selectable but the children of our roll-a-ball game are marked with another layer named: roll-a-ball.
The result of this implementation, is that the colliders wouldn't co-exist meaning, they won't intersect and cause the **OnTriggerFunction** to trigger each time.
In order to disable the triggering, we change that through the player settings.
