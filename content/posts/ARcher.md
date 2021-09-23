---
title: "ARcher"
date: 2021-09-21T14:06:18+03:00
featured_image: "/images/ARcher - Project Image.jpg"
draft: false
---
Motivation
===============

After creating many VR projects, I thought it was a good idea to move to AR, since it also fascinated me. My first idea for an AR project came from my favourite game the **Binding of Isaac** and especially platform games such as **Mario** since I am a big fan of them.
The main concept behind this project was to create a non linear platform game. For main components I used the cards from a deck.
Each card would serve as a platform with a level attached to it. When I was creating this project I utilized 4 cards: : 1) Ace of Spades 2) Two of Spades 3) Eight of Spades 4) Five of Hearts.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/ARCher%20-%20Cards.JPG)

Implementation
===============

Each of these cards contained a different platform with different kind of interactions. 

Ace of Spades
---------------

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/ARCher%20-%20Ace%20Of%20Spades.JPG)
In this card we summon the first stage and our hero, the ARcher. The hero starts without anything but
when he picks the arrow that is close to him, he will then gain a crossbow. Apart from the crossbow,
another button appears on the screen, this button when triggered, enables the player to shoot in the
direction that he is facing to. In the first level there are three things (two appear in this screenshot),
the spikes and the platform and a star pick up (not visible due to being VFX and have to be selected).
When the player touches the spikes he dies and after 2 seconds he will be respawned. To where he
respawns is dependent on which checkpoint he last touched. The checkpoints are the platforms where
we see our player standing in the above screenshot. 
The way the player moves is what makes it possible to play this game and these kinds of AR-Games. Because it is a combination of physical and non-physical movement. We need this kind of movement because when we are developing in AR and we are using physics based movement,
even a slight glitch could cause the player to be thrown away. So in order to check when or not to enable or disable physics, we fire a raycast from the bottom of our player. If it detects ground, then we are disable gravity in order to move. When the raycast is not detecting anything, it means that 
our player is in the air and thus we have to enable gravity so that it creates a realism that our player falls. The code snippet that does that is the following:
```C#
 if(!Physics.Raycast(transform.position, Vector3.down, Mathf.Infinity))
        {
            heroRigidbody.constraints = RigidbodyConstraints.None;
            heroRigidbody.useGravity = true;
            heroRigidbody.isKinematic = false;
        }
        else
        {
            heroRigidbody.constraints = RigidbodyConstraints.FreezePositionY;
            heroRigidbody.constraints = RigidbodyConstraints.FreezeRotationX | RigidbodyConstraints.FreezeRotationZ;

            heroRigidbody.useGravity = false;
            heroRigidbody.isKinematic = true;
        }
```
I have to point also that our hero and the enemies are prefabs that are animated and they are not just moving around the scene like static objects. They have a complex animator components and trees that are shown in the next picture:
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/ARCher%20-%20Animation%20Tree.JPG)

Two of Spades
---------------

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/ARCher%20-%20Two%20Of%20Spades.JPG)
The second card of our game we introduce the first enemy variation, the frightfly. These flies move
way too fast and it is very difficult to bypass without shooting them first. Shooting them also is no easy
task. In order to pass this level, the player must avoid or kill the fireflies and as well as evade the spikes.
The fireflies move arround two constant points where we set in our inspector and their controller is:

```C#
float lerpPercentage = Mathf.PingPong(Time.time, repeatTime) / repeatTime;

            transform.position = Vector3.Lerp(startingPosition.position, finalPosition.position, lerpPercentage);
            if (Vector3.Distance(transform.position, startingPosition.position) < 0.1f)
            {
                flyAnimator.SetBool("Fly forward", true);
                transform.LookAt(finalPosition);

            }
            else if (Vector3.Distance(transform.position, finalPosition.position) < 0.1f)
            {
                transform.LookAt(startingPosition);

            }
```

Eight of Spades
---------------

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/ARCher%20-%20Eight%20Of%20Spades.JPG)
This level is a little more tricky than the others. It is almost impossible for the player to pass without
shooting the piranha plants. These plants are able to detect the player when in close proximity and
they quickly kill him. The piranha plants check the proximity of the player and they attack him when it gets close to them.
```C#
 if (!isDead && timeBeforeBites < 0f)
        {
            if (Vector3.Distance(transform.position, player.transform.position) <= lookRadius)
            {
                transform.LookAt(player.transform);
                piranhaPlantAnimator.SetTrigger("Bite Attack");
            }

        }
        else if (!isDead && timeBeforeBites > 0f)
        {
            timeBeforeBites -= Time.deltaTime;
        }
```

Five of Hearts
---------------

![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/ARCher%20-%20Five%20Hearts.JPG)
Our last card for our demo, the Five Of Hearts. It includes our last enemy, the peashooter where it
functions like a turret gun. According to which direction it is facing it is shooting projectiles.

Videos:
---------------

{{< youtube EQx3Q7t3PC8 >}}

{{< youtube 2uzIrKo4wMw >}}


