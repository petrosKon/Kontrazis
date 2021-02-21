---
title: "First Lab: Roll a ball"
date: 2020-12-07T12:20:31+02:00
draft: false
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

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Player%20Components.PNG "Player components")

Then the next part we create is our environment, a.k.a the walls and we place them at the edge of our plane, so that our player can not pass through them.

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Walls-Environment.PNG "walls")

Next we move to our pickups, which are collactables that the player needs to pick up in order to win the game. We want to use the same type of pickup so we make a prefab of each. A prefab is an object that can be used multiple times into our scene and they share the same properties.
After creating prefab, we want our player trigger a condition whe he/she picks up an object.
In order to do so we user the function **OnTriggerEnter**, this is an override function which executes when an object is triggering with this object's collider. As a result we also mark the object's collider as trigger.
We override the **OnTriggerEnter** into our **PlayerController** script. But what happens if there is another object that has also a trigger as a collider but we do not want the same functionallity?
In order to avoid this problem, we specify a tag for our pickup, so that the right kind of actions happens when we touch this item.

```C#
 private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("pickup"))
        {
            other.gameObject.SetActive(false);
            count++;
            SetCountText();

        }
    }
```
With the specification of the tag for our pickup and the compareTag method we can specify what will happen if our player touches our object.
Last but not least, we also attach a script to our pickups so that they are not static and they rotate over time, in order to create an effect.
Time.delta is required so that our rotation is frame indipendant, because the Update functions runs on different frames depending on the computer's hardware.

```C#
  void Update()
    {
        transform.Rotate(new Vector3(15,30,45) * Time.deltaTime);
    }
```

Then for the last part, we need our UI in order to show the player the progress of how many items he/she has collected, we then put a canvas into our scene.
Then in the canvas we put a Text component (in our case TextMeshPro) and we change the anchor position to the top right.
As a result the text is position in the top right of our canvas.
We also put another text that is the text that is going to be displayed when the user collects the necessairy pickups and we call it **Win Text** which at first we **setActive(false)** in order to hide it.
And as a result we can we that even is since is grayed out in the inspector is also not showing in the project.

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Canvas%20%2B%20Text.PNG "Canvas and Text")

Last but not least, we create a certain condition that when the user graps more than 10 pickups then the **Win Text** will appear.

```C#
  private void SetCountText()
    {
        countText.text = "Count: " + count.ToString();
        if(count > 10)
        {
            winTextObject.SetActive(true);
        }
    }
```