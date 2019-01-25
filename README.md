# C Sharp Object Pooling for Spawning
Game Objects Pooling scripts in C#

## **How To Use?**
###### Step 1
- Import **_PoolManager_** and **_PoolObject_** script to your project
- Create an empty game object as a spawn manager, **attach PoolManager script to the manager object**. Example, *EnemySpawnManager* in Unity's hierarchy.
- Create a custom spawner/spawn manager class. Example, *EnemySpawner* class. **Attach to spawn manager object as well**.

###### Step 2
Declare a PoolManager object in spawner class.
```
PoolManager poolManager;
```

###### Step 3
Declare a single/array of game objects - for developer to drag in object prefab to spawn
```
public GameObject[] objPrefabs;
```

###### Step 4 (optional) - spawn objects at specific locations
Declare an single/array of transform (position) - for developer to drag in pre-created empty gameobjects (to indicate spawn point)
```
public Transform[] spawnPoint;
```

###### Step 5
Initialize pool it at spawner class's Start() Function
```
poolManager = GetComponent<PoolManager>();
        //objPrefabs.Length indicate the pool manager to spawn same X amount for each objPrefabs dragged in Unity's inspector
        for (int x = 0; x < objPrefabs.Length; x++)
        {
            //this line do the game object instantiations, which objPrefab and how many to spawn
            poolManager.CreatePool(objPrefabs[x], 500);
        }     
```

## All Set! Now your game has tons of prefabs to be instantiate everytime the game start!
Note: They are all in inactive state at first!

----------------------
# To Use A Game Object From The Pool (inactive -> active)
Just use this code to set the object (inactive currently) to active.
```
poolManager.ReuseObject(objPrefabs[prefabToSpawnIndex], spawnPoint[posToSpawn], spawnPoint[posToSpawn].rotation);
```
**Note: prefabToSpawnIndex** and **posToSpawn** are to defined earlier before this line. If you wish to spawn random prefab and position, then add this two lines before **_ReuseObject()_**:
```
prefabToSpawnIndex = Random.Range(0, objPrefabs.Length);
posToSpawn = Random.Range(0, spawnPoint.Length);
```
----------------------
# To Stop Using A Game Object From the Pool (active -> inactive)
Simply use ```GameObject.SetActive(false)``` at respective script.



end.
