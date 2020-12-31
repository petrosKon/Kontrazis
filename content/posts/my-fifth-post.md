---
title: "3 Locomotion Techniques"
date: 2020-12-10T15:54:48+02:00
draft: false
---

My main motivation behind this course is to explore locomotion techniques using hand tracking. I believe future headsets won't rely on controllers to move around as well as interact with the environment. 
The first method I propose is a non-linear approach to movement, that is shown in the following diagram.

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Locomotion%20Technique%201.jpg "First Locomotion Technique")

The idea of this non-linear locomotion technique is that a user would grow up in an immense scale, then the avatar will be placed in the center of the track. A huge avatar will enable to player to see the whole track. With his/hers hand will draw a path along that track and the player stops drawing then he will revert back to normal size and follow the track that he/she already drew.
The reason I have not implemented this idea, is mainly because I thought it was off the time limit of the course. It would require rigorous implementation and the problems that may have arisen, would be greater than the other two implementations.

My second idea, is a gesture based locomotion techique. The user would do basic gestures and as a result, the VR camera will move accordingly.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Gesture%20-%20Poiting%20Forward.png "Pointing Forward")
For example the image above, shows a basic implementation. When the user points forward, he/she moves forward.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Gesture%20-%20Poiting%20Left.png "Pointing Left")
This gesture would enable user to move left for example and you can imagine how the rest it goes on.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Gesture%20-%20Poiting%20Upwards.png "Pointing Upwards")
But that locomotion technique, had some serious problem when I tried to implement it. First of all, it required the user to remember all these different gestures and it was easy to make a mistake. Then the track itself beautifuly demostrated a huge problem in this approach, an different aproach would have to be used on incline surfaces. An example would be a raycasting from the player's head to detect if the ground is inclined or declined in order to update the position of the player.
This is not that hard to implement, but I believe it would create glitches. So, when I was experimentating of a way to bypass this problem, I came up with another idea which is more linear as well as more fun!!
In VR we don't want to be boring individuals, we want something special, something different. The approach was not different or special but it made the user feel special. We are talking about a **Superman** locomotion technique.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Gesture%20-%20VR%20Superman.png "VR Superman")
As the user makes this gesture, then he/she will able to move forward and according to where he/she is looking the position changes. Also the hand have to be elongated forward so that it mimics superman's flying ability.
Then, he/she will be able to traverse the stage as being the superhero he/she ever wanted.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Superman%20-%20Flying.png "Flying Superman")