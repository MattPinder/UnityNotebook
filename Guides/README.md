# Short guides for implementing various features

## Set up an array of prefabs for random spawning
Logic derived from Unity Learn ((link to tutorial)[https://learn.unity.com/tutorial/6754617aedbc2a095b867ae0?uv=6&projectId=5cdcc312edbc2a24a41671e6])

This assumes you have:
* A Spawn Manager in your Hierarchy
* A `SpawnManager` script attached to the Spawn Manager object
* A set of prefabs you want to spawn at random

1. In `SpawnManager`, define a `public GameObject[] randomPrefabs` variable
2. Set the relevant prefabs in the Spawn Manager object's Spawn Manager component
3. In `SpawnManager`, above the `Instantiate` method for spawning the random enemy, determine a random index within the relevant range:
```
int prefabIndex = Random.Range(0, randomPrefabs.Length);
```
4. Within the Instantiate method, define the random prefab, its position(?), and its rotation using:
```
randomPrefabs[prefabIndex]
```

Example code for `SpawnManager`:
```
public class SpawnManager : MonoBehaviour
{
	public GameObject[] enemyPrefabs;

	void SpawnPrefab()
	{
		int prefabIndex = Random.Range(0, randomPrefabs.Length);
		Instantiate(randomPrefabs[prefabIndex], GenerateSpawnPosition(), randomPrefabs[prefabIndex].transform.rotation);
	}


```