---
title: "Lab Homework 5: Superpower VR"
date: 2020-12-31T12:25:10+02:00
draft: false
---

To be honest the idea of the gesture recognition came to me when I first saw this video: https://www.youtube.com/watch?v=lBzwUKQ3tbw

So I wanted to create something around it, as well as experiment with it. The code I used in most of my project was from this tutorial, but I needed to deep dive into it and understand it, in order to create the **Superman VR**.
Now, first let's deep dive into the code of this video.
First of all, we create a list of **OVRBone** variables called **fingerbones**, this list contains all the bones of our hand. Our hand is referenced through the variable called **OVRSkeleton** and this is the field we are going to use in order to check for a gesture.
Gesture recognition as presented in the video is a form of continously searching for gestures. Since the movement of the hand is continuous, we need to constantly check if a gesture is made and if the current position of the fingers correspond to a gesture.
We create a **struct** called **Gesture** with the following fields:

```C#
public struct Gesture
{
    public string name;
    public List<Vector3> fingerDatas;
    public UnityEvent onRecognized;
}
```

It is easy to understand the name and the list of Vector3 that each gesture contains. Then we add an **UnityEvent**. **UnityEvents** are able to trigger functions when something particular happens and in our case, a gesture.
Then we create the following fields:

```C#
    [Header("Hand Skeleton")]
    public OVRSkeleton skeleton;

    [Header("List of Gestures")]
    public List<Gesture> gestures;

    [Header("DebugMode")]
    public bool debugMode = true;
```

The **OVRSkeleton** component is the one that we assign our hand. We also create a list of gestures that we are going to use in our application and last of all a debug variable that is going to be used in order to save our gestures.
The first step is to find a way to register our gestures and this is done through the **Save** function.

```C#
    void Save()
    {
        Gesture g = new Gesture
        {
            name = "New Gesture"
        };

        List<Vector3> data = new List<Vector3>();

        foreach (var bone in fingerbones)
        {
            data.Add(skeleton.transform.InverseTransformPoint(bone.Transform.position));
        }
        g.fingerDatas = data;
        gestures.Add(g);
    }
```

This function enables the user to Save a gesture, it is very easy to understand since it takes all the **OVRBone** components from the skeleton and we added to the list. Another thing to point out is that **skeleton.transform.InverseTransformPoint** adds the position that is relative to the parent's, hence the object's local position. We want this kind of information since it will be easier to compare the gestures.
We then add another field in our code called **threshold** and this field is very important, since it depicts how closely our hands need to match the gesture in order to trigger the **UnityEevent**.
If we put a very big number then even gestures that are close to one of our gestures will trigger, whereas if we put a low threshold then we will need the exact gesture. So the threshold value is going to be decided through trial and error. For the first part I found out that a good value is **0.05**.
As we made a way to save the gestures, then we need a way to trigger it. So we put this condition inside the **Update** function.
```C#
 if (debugMode && Input.GetKeyDown(KeyCode.Space))
        {
            Save();
        }
```
That basically says that if we have the debug mode on and press **Space** button while we are making a gesture, then it will be saved. The next gesture then will appear on the inspector. In order for it to appear on the inspector, we need to add the following field in the **Gesture** class.
```C#
[Serializable]
```
Then we need to copy the component values while in play mode and paste it when we stop the game, since we can not save anything while in Play mode.
I believe this could be done better, since it is not really recommended to save it that way. A proper way could be using Json Files to save all the data.
Now, we move to the part where we write the code that recognizes our gestures.
```C#
 Gesture Recognize()
    {
        Gesture currentGesture = new Gesture();
        float currentMin = Mathf.Infinity;

        foreach (var gesture in gestures)
        {
            float sumDistance = 0;

            bool isDiscarded = false;

            for (int i = 0; i < fingerbones.Count; i++)
            {
                Vector3 currentData = skeleton.transform.InverseTransformPoint(fingerbones[i].Transform.position);
                float distance = Vector3.Distance(currentData, gesture.fingerDatas[i]);
                if (distance > threshold)
                {
                    isDiscarded = true;
                    break;
                }

                // if the distance is correct we will add it to the first float we have created
                sumDistance += distance;
            }

            // if the gesture we made is not discarted and the distance of the gesture i minor then then Mathf.inifinty
            if (!isDiscarded && sumDistance < currentMin)
            {
                // then we set current min to the distance we have
                currentMin = sumDistance;

                // and we associate the correct gesture we have just done to the variable we created
                currentGesture = gesture;
            }
        }

        return currentGesture;
    }
```
It could seem complex at first, but it is really not. The basic principle behind this block of code is that we take the current position of the hand tracking fingers and we compare them with the already saved ones. If the total distance of all fingers is greater than our threshold then it is not the gesture.
Then this could would need to run all the time since hand tracking and gestures are constantly updated.
```C#
            Gesture currentGesture = Recognize();
            hasRecognize = !currentGesture.Equals(new Gesture());

            if (hasRecognize)
            {
                doneRecognizing = true;

                currentGesture.onRecognized?.Invoke();
            }
            else
            {
                if (doneRecognizing)
                {
                    Debug.Log("Not Recognized");
                    doneRecognizing = false;

                    notRecognize?.Invoke();
                }
            }
```

Then in our **Update** method, we continously check if a new gesture is made and if this gesture falls below a threshold, concerning the previous gestures,it is recognized.
Elsewhere, if it is not recognized, we create another **UnityEvent**.

Now we will move to the code that makes our **VR player** move around like our superhero. We record two gestures with the way described above.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Gesture%20-%20VR%20Superman.png "VR Superman")

and we need a second gesture in order for our player to stop.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Gesture%20-%20Stop.png "Stop Gesture")
Then we need two specify the relative position of the two axis, the **HMD** axis which is located in the **CenterEyeAnchor** as well as the **Hand** axis.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/HMD%20-%20Local%20Transform.png "HMD Local Axis")
We see in the above image that it is aligned with the world coordinates. Whereas the hand coordinates system looks like this.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Hand%20-%20Local%20Transform%20Upwards.png "Local hand axis")
We need these coordinates systems because, we want our player to start moving when he is doing a first but also when that fist is aligned with the **HMD** transform system. We can see that the transform systems point to different directions and as a result we take the following angles.
```C#
        float angleBetweenHandAndHMD = Vector3.Angle(skeleton.transform.right, hmdCenterEyeAnchor.transform.forward);
```
We take the right angle of our hand (red axis), because it is pointing backwards, when our hand is aligned. We then proceed to find an angle that is not too restrictive but as well as not too lose. The angle between the hand and **HMD** will enable to user to turn, when he/she turn both his/her hand as well as its head.
We then take another angle.
```C#
        float angleBetweenYAxisAndHMD = Vector3.Angle(skeleton.transform.up, hmdCenterEyeAnchor.transform.up);
```
This angle is set so that the user would be able to initialize the locomotion technique only when he/she holds the hand upwards and not downwards.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Hand%20-%20Local%20Transform%20Downwards.png "Hand Backwards")
```C#
        if (angleBetweenHandAndHMD > angleThresholdHandAndHMD && angleBetweenYAxisAndHMD < angleThresholdYAxisAndHMD)
        {
            startingSpeed += (0.03f + Time.deltaTime);

            if (startingSpeed > maxSpeed)
            {
                startingSpeed = maxSpeed;
            }

            cameraTransform.transform.position += hmdCenterEyeAnchor.transform.forward * startingSpeed * Time.deltaTime;
	}
```
These lines of code are the locomotion technique using our hand. We have a starting speed and then gradually increase the speed of our player. We also set a max speed so that the player doesn't go too fast or too slow.
Then we update the **HMD** according to where the hmd is looking and in correspondance with the hand position and as the result the player moves forward.
These functions are placed in the inspector.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Inspector%20Gesture%20Recognizer.PNG "Gesture Recognizer")
Last but not least, we have to also need to stop the movement when the user does the stop gesture. This is pretty simple to do, since we do not need to do anything, since the only way to update our speed is by doing the superman fist.
When the player stops then, we just set the value of the starting speed to 1.
```C#
    public void StopMovement()
    {

        startingSpeed = 1f;
    }
```
This is all the code as well as logic for our locomotion technique, also we can see a final implementation in this video:

https://www.dropbox.com/s/kqynksk9aepcyvg/2%20-%20Evaluation%20of%20Locomotion%20Technique.mp4?dl=0