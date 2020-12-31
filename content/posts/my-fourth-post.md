---
title: "VR Roll-A-Ball"
date: 2020-12-09T14:11:36+02:00
draft: false
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

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Layers%20%26%20Colliders.PNG "Layers & Colliders")

Since we added our colliders and rigidbodies we then proceed to create our logic behind our grab. We create a new script called MySelect and we attach in each controller.
This code permits the user to grab into an object when he/she presses the **Index trigger button**.
We get the information of our index trigger using **OVRInput** and then inside our **Update** method we contiounsly check if the user presses the index trigger above a certain threshold which is over **>0.95f**.
The value that the index trigger provides us is a float and not a boolean so that it permits it to trigger our functions in different points.

```C#
triggerValue = OVRInput.Get(OVRInput.Axis1D.PrimaryIndexTrigger, controller);
```

The controller parameter is a parameter that we can modify in our inspector.
After the user pushes the button, then what we do is make this gameobject child of the transform of the object that is supposed to grab it. Making an object child is a simple way to simulating of grabbing an object, because the child's transform follows the parent's with an offset.
In order to properly change the transform of a gameobject since it contains a rigidbody, we disable the gravity component and we make it kinematic, so that the physics won't interrupt our grab.
Last but not least, we set the controller velocity and angular velocity equals to zero.

```C#
  Rigidbody rb = selectedObj.GetComponent<Rigidbody>();
                rb.isKinematic = true;
                rb.useGravity = false;
                rb.velocity = Vector3.zero;
                rb.angularVelocity = Vector3.zero;
```

We must also think what will happen if the user decides to release the trigger, then first of all we unparent the object. Secondly we enable again the gravity so that our object could be affected by the Unity physics engine.
Last but not least, we want the user to be able to throw the the whole system, this is done by grabbing the controllers velocity as well angular velocity the moment when the user releases the trigger button.

```C#
  rb.velocity = OVRInput.GetLocalControllerVelocity(controller);
  rb.angularVelocity = OVRInput.GetLocalControllerAngularVelocity(controller);
```

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Final%20Configuration.PNG "Final Configuration")
