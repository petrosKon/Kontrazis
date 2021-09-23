---
title: "Animal_run_2d"
date: 2020-07-20T11:13:36+03:00
featured_image: "/images/Animal Run/Animal Run - Project Image.jpg"
draft: false
---
Motivation
===============

This is was my first game that I completed by myself, without working in a company, in Unity. The purpose of that game is to create an endless runner using animals as characters. The choice of animals was due to the fact that this game 
is integrated into a social media for pets.

Implementation
===============

The first thing we needed to do was to create an endless scroller, meaning that the animal would have to run indefinetely. In order to do that we continuously update the position of our and as well as the camera's in order to follow the player.
Each animal has a player controller that determines the starting speed and then it increases an fixed amount according to how much it moved.
The next thing we need to do is to spanwn the platforms in the correct position. The correct position means that the player is able to jump and it is not too far away and or the platforms are not coinciding.
So in order to do that, the first thing we do is get the platforms' width that we already defined and put them into a list.

```C#
  platformWidths = new float[theObjectPools.Length];

        for (int i = 0; i < theObjectPools.Length; i++)
        {
            platformWidths[i] = theObjectPools[i].pooledObject.GetComponent<BoxCollider2D>().size.x;
        }

        minHeight = transform.position.y;
        maxHeight = maxHeightPoint.position.y;
```

Then we proceed to generate a new platform on a random point using the following code:


```C#
if (transform.position.x < generationPoint.position.x)
        {
            //comment to create a continuous platform
            distanceBetween = Random.Range(distanceBetweenMin, distanceBetweenMax);

            platformSelector = Random.Range(0, theObjectPools.Length);

            heightChange = Mathf.Clamp(transform.position.y + Random.Range(-maxHeight, maxHeight), minHeight, maxHeight);

  //we change the position of the generation point
            transform.position = new Vector3(transform.position.x + (platformWidths[platformSelector] / 2) + distanceBetween,
                heightChange,
                transform.position.z);

            GameObject newPlatform = theObjectPools[platformSelector].GetPooledObject();

            newPlatform.transform.position = transform.position;
            newPlatform.transform.rotation = transform.rotation;
            newPlatform.SetActive(true);
            //Debug.Log(newPlatform.transform.position);

            //prevents spawn on small platforms
            if(!newPlatform.name.Contains("3") && !newPlatform.name.Contains("4"))
            {
                if (Random.Range(0f, 100f) < randomEnemyThreshold)
                {
                    GameObject newEnemy = enemiesPool[Random.Range(0, enemiesPool.Length)].GetPooledObject();

                    float enemyXPos = Random.Range(-platformWidths[platformSelector] / 3, platformWidths[platformSelector] / 3);
		}
	    }
 transform.position = new Vector3(transform.position.x + (platformWidths[platformSelector] / 2),
            transform.position.y,
            transform.position.z);

            // Instantiate(thePlatforms[platformSelector],transform.position,transform.rotation);
        }
    }
}	
```

What this code does is basically spawns platforms in the correct positions and also prevent spawn overlap. In order to make our game more interactive we also used some pickups and enemies. In both our enemies and pickups and platforms
we are using **object pooling**, to reduce the number of objects in the scene and avoid unecessary data overflows.

```C#
 public GameObject GetPooledObject()
    {
        for(int i = 0; i < pooledObjects.Count; i++)
        {
            if (!pooledObjects[i].activeInHierarchy)
            {
                return pooledObjects[i];
            }
        }

        GameObject obj = Instantiate(pooledObject) as GameObject;   //casting it as a GameObject
        obj.SetActive(false);
        pooledObjects.Add(obj);
        return obj;
    }
```

Now we are going to talk about our pick-ups. There are many types of pick-ups. Most of them are different fruits that give you points according to their rarity and two power-ups. The first one being double point score and the second one invicibility for a short period of time.
![alt text](https://raw.githubusercontent.com/petrosKon/Kontrazis/master/static/images/Animal%20Run/Animal%20Run%20-%2001%20-%20Pick-ups.JPG)
The next thing we are to describe is our enemies. There are 4 types of enemies. A cactus, spikes, a woodtrap and a Bird. Each of them are static enemies and they appear at the platform.
We have also to make sure that since the enemies have a certain length that they are not placed in platforms that they are smaller of them and as a result kill the player.

