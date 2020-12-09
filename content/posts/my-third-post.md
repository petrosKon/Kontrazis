---
title: "First Lab: Roll a ball"
date: 2020-12-07T12:56:47+02:00
draft: true
---

The point of the first lab is to create a roll a ball game. This example is compromised of different elements : 1) The player 2) The environment 3) Pickups - Different Objects.
First of all, we create our environment, a plane which is empty and it is located in the (0,0,0) position. This is the plane in which we are going to create our game.
We also assign a material to our plane so that it is not appear empty and appear a little colorful to the user playing it.

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Ground.png "Ground")

The next step is to create a player. The player in our situation is a sphere that is positioned in Y-Axis 0.5 points above 0, this is why we want our player to just touch the plane.
We also assign a material to our player, in our case it is red.

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Player.png "Player")

Next we have to find a way to move our player, this is done thought the Unity's input manager, a package that we inserted through the package manager. Then we define the type of movement of our player, which is a Vector2 which correspond to which keys are pressed.
In order for our player to move we have to add the rigidbody component, so that when the keys are pressed, we add a constant force.

After the player movemement is being set up we move to change the position of the camera as well as how it moves according to the player.
Last but not least, in our player script, we also attach the text that is going to change as well as the winning text if the user reaches the desired score.
Finally we have the following components attached to our player.