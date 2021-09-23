---
title: "Stabbing Post-Its VR"
date: 2021-04-30T09:14:42+03:00
featured_image: "/images/Post it images/Stabbing Post-its - Project Image.jpg"
draft: false
---
Motivation
===============

Brainstorming with post-its can be a fun and creative way to come up with new ideas, from silly ones to more serious ones. These sessions can provide powerful insights to problems that will appear and as well as ways to tackle them. So, as a team we found a new way to brainstorm with post-its but this time in the virtual world and more specifically using Oculus Quest. 
![alt text](https://github.com/petrosKon/Kontrazis/blob/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%201.png?raw=true)
In order to explore how brainstorming with post-its work we first did a first brainstorming session about what we need to do if we opened a cafeteria. Then after that we proceeded to make another post-its brainstorming session in order to see what we were going to create in the virtual environment. This time as a template we used **Miro**.
This project was created on par with a designer in order to embellish it and make it more appealing to users.

Design 
===============

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%202.png)
First, we define our objects, post-its, walls, etc.. so we can understand more about them and as well as the actions we do with them. After defining the main elements of our project, we then proceeded to find different and awesome ways to interact with Post-Its.The most prevalent ideas were either stabbing the post-its with swords or suck the post-its with a vacuum, but after discussion we both agreed to stab the post-its. The next step is to define how this application would function and what are its main aspects. We concluded that we are going to use many swords and each sword should act as a group post-it that defines a certain category. After that, we sketched the flow of actions within our scene.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%203.png)
This is our main scene, the user has in front of him/her a list of post-its. He can not pick them up whatsoever. The only thing that has the ability to move a post-it is the sword, where the user must pick it from the stone that is in front of him/her.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%204.png)
After the user has choose the post-its that he/she wants to categorize, in order to name he/she must place the sword above his head and speak the name.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%205.png)
When a sword stabs a post-it, then it is attached to the sword in a circular display, the player can see the post-its by browsing through them. After the user leaves the sword then it returns to a special position with the collected post-its.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%206.png)

Prototyping & Implementation
===============

Sword & Notes
---------------

After all the elements of the project have been agreed we then proceeded into creating the Unity environment. 
The first milestone of our journey is to create the swords so that they can be grabbed by our player. In order to do that we used an asset called AutoHand VR. With this asset we are able to realistically grab the swords (and not just attach them to our hands) as well as, it provides UnityEvents on each action (grabbing, letting go of the trigger etc). This provided an easy as well as efficient way for us to create our interactions.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%207.png)
The second task is to find a way to grab and arrange the post-its around the sword. In order for a sword to effectively pierce a post-it, we used a collider at the edge, this is done in order to avoid triggering the post-its with every corner of the sword. 
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%208.png)
The next thing we added is a way for our post-its to circulate around the sword.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%209.png)
After that we need to determine the sword’s and the post-it it contains, final positions. These positions determine where the sword and the post-its are gonna land when the user releases it. We created a wall that functions as a sword and post-it holder.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%2010.png)
After some iterations, we realised that this type of wall display created a lot of problems, because after a sword was released, it was really hard to grab it again. So we implemented a new method, with a different display method, that was easier for the user to grab the sword.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%2011.png)
The last thing we added is the ability to take swords out of a stone instead of just the swords floating in front of the player. After a sword is released from the stone, a visual effect will play and another one will appear at its place.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%2012.png)

Labeling the Swords - Speech Recognition
---------------

To add names to groups we decided early on to use speech recognition. It is a more immersive experience then typing, and finding a good way to type in VR could be a project by itself. The only free and on-device speech recognition software we found was PocketSphinx. The code is copied from the linked github repository and fit to our scene.
We started with the following concept: The user lifts the sword up over their head and says the name they want to give the group. To let the user know what is happening and what they had to do, we wanted to add some feedback. If the user lifts the sword a beam appears, their controller vibrates, and a voice asks the user how their group should be named. After the speech analysis, depending on the result, the voice approves by saying: “Your group has a new name”. If the speech could not be recognized the voice asks the user to try again. 
Later we also made sure that the user can only change the name of one group at a time. Because the user can hold two swords this was necessary. 

Final Version
===============

Our idea from the start was to have the user stand on an island, with the Post-Its in front of them, and the overview of created groups next to them.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%2013.jpg)
We have also added some trees, stones, and animated grass to make the environment more alive.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%2014.png)
The user has all the important elements, the sword spawner, the post-its, and the displays for the groups right next to them. This can be seen as a precaution to take into account that users might not have much space to walk around. It also makes looking at the unsorted Post-Its and at the groups easier. 
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Post%20it%20images/Stabbing%20Post-its%20-%2015.png)

Conclusion & Future work
===============


To conclude we must say that we successfully implemented everything that was on our list, we managed to transfer our ideas to sketches and to fully develop them in the virtual environment. Our implementation is still not perfect, some problems were not solved during our development.
The first thing is that there is no distinct way for the user to know, where the sword will go after letting it and sometimes it can cause confusion, because it may seem lost. Another thing is the speech recognition. The API that we are using is causing the main game to freeze for a little while and it can be annoying.
Apart from the problems, new features could be added so that they can make this application much more appealing. First of all, multiplayer functionality, where two or more users can collaborate in the same environment. Apart from that, we can see that our scene contains a discrete amount of post-its, it would be a helpful functionality if the user is able to create more or even change the color of them, so it can resemble as much as possible the way we do it in real life.

Video of the application:
---------------

{{< youtube yf8Abz3wlqI >}}
