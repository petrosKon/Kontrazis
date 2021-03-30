---
title: "IGD900 - Harmful VR"
date: 2021-03-29T21:53:14+01:00
draft: false
---

Have you ever played VR and accidentally hit your hand over a wall? Have you ever played VR and managed to break something in your house?
As it turns out, you are not alone, it is not uncommon when using VR you may sometimes hit or break something. There is even a popular term on Youtube called **VR Fails** that yield way too many results and videos with a huge amount of views.
This introduction was to describe to you what we wanted to explore with this project. An application that would be able to cause **Harm** to the user.
But this harm is for a good reason, we needed to point out parameters that would make an application marked as "Harmful".
First of all, we discussed over different types of harm from physchological to physical harm and discussed different ideas for an application.
I would have two ideas, a horror game made in VR and with the use of jump scares it could induce harm to the user or a way to inflict physical harm. I went with the latter.
The whole application was developed purely in Unity and it was made for the Oculus Quest specifically.
When I first started this application, it was a simple catch a ball game, where one user could throw balls to the player and the other would try to grab them.
It was developed and run in one machine, a pc or a laptop and the player in the laptop would see the user in VR and in real-life.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Catch-A-Ball%20Game%20Simple.PNG)
The picture above shows the result. The green circle is the depiction of the user's stationary boundary. The red circle is the depiction of the edges of the stationary boundary. The green arrow shows where the user is currently looking and the transparent green circle is the cursor with which the user in pc throws a ball.
We released then that this depiction of the guardian was not enough. Thus, we wanted to see the guardian that the player is drawing.
The script that was able to do that, was the following:
```C#
  bool configuredBoundaries = OVRManager.boundary.GetConfigured();
            if (configuredBoundaries)
            {
                //Get all boundary points
                boundaryPoints = OVRManager.boundary.GetGeometry(BoundaryType.OuterBoundary);

		 //render points with walls boundaries
                for (int i = 0; i < boundaryPoints.Length; i++)
                {
                    #region Wall Boundaries
                    if (i % distanceBetweenWalls == 0)
                    {
                        Vector3 positionBetweenBoundariesAndPlayer = new Vector3(boundaryPoints[i].x + spawnedVRPlayer.transform.position.x, 1f, boundaryPoints[i].z + spawnedVRPlayer.transform.position.z);
                        boundaryPoints[i] = positionBetweenBoundariesAndPlayer;
                        GameObject wallObject = PhotonNetwork.Instantiate("Wall Object", boundaryPoints[i], Quaternion.identity) as GameObject;
                        wallObject.transform.parent = guardianMapper.transform;

                        yield return null;

                    }
                    #endregion
                }
```
What this snip of code basically does is get all the points of the guardian that Oculus gives us. But we realise that this code didn't worked when the Oculus Quest Link was enabled, so we needed to find another way to create our experience. 
So, in order to solve that problem, I designed a multiplayer game. One player would be able to player from PC and control as previously said the balls that was throwing to our player and the other player would playr from VR.
This multiplayer experience was created using **Photon**, a framework that makes the development of multiplayer experiences real fast.
When a player enter the application then he/she automatically joins a room that is assigned by me. In order to be able to stream the data from the Oculus to the other player we use the following script:
```C#
  void MapOculusPositions(Transform target, XRNode node)
    {
        InputDevices.GetDeviceAtXRNode(node).TryGetFeatureValue(CommonUsages.devicePosition, out Vector3 position);
        InputDevices.GetDeviceAtXRNode(node).TryGetFeatureValue(CommonUsages.deviceRotation, out Quaternion rotation);

        target.localPosition = position;
        target.rotation = rotation;
    }
```
We get the position and location directly from Unity's Input system and we stream that data to the player in the monitor. We need both the position and rotation so that we know where our VR player is at any given time.
Instead of just creating and implementing the multiplayer functionality, we also changed our scene, so that it seems more realistic to our player.
The result of previously mentioned application is shown below:
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Catch-A-Bottle.PNG)
The new is clearly a bar and not an empty space. Instead of the user catching I would throw the to the user bottles so it doesn't feel mundane. Last but not least, the wooden sticks you are seeing is the guardian that we are drawing using the code we described above.
But with thorough testing we realised something, that the "catching" movement was not enough to make the player try to get out of the boundary and we needed a new mechanism.
So instead of catching I introduced slicing. The game then would feel very similar to the popular game **Fruit Ninja VR** and a lot more functionality would be added.
Before diving into the new implementation, I need to add more things about the sychronization of the game. The main idea is that where the user in pc clicks a projectile would be fired following a curve. This is accomplished by using this script:
```C#
  LaunchData CalculateLaunchData()
    {
        float displacementY = target.y - this.transform.position.y;
        Vector3 displacementXZ = new Vector3(target.x - this.transform.position.x, 0, target.z - this.transform.position.z);
        float flightTime = Mathf.Sqrt(-2 * trajectoryHeight / gravity) + Mathf.Sqrt(2 * (displacementY - trajectoryHeight) / gravity);
        Vector3 velocityY = Vector3.up * Mathf.Sqrt(-2 * gravity * trajectoryHeight);
        Vector3 velocityXZ = displacementXZ / flightTime;

        return new LaunchData(velocityXZ + velocityY * -Mathf.Sign(gravity), flightTime);
    }
```
Now we will talk about our new scene, the fruit slicing one. We found out during experimentation that the more present the user is in the application, more are the chances that he/she will collide with the guardians, then we proceeded to add couple of things.
First of all, we changed the scenery. The slicing is made using katanas and what is the best environment for a Katana? **Japan**. So, this is our new environment:


