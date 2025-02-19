# Short guides for implementing various features

## Set up an array of prefabs for random spawning
Logic derived from Unity Learn ([link to tutorial](https://learn.unity.com/tutorial/6754617aedbc2a095b867ae0?uv=6&projectId=5cdcc312edbc2a24a41671e6))

This assumes you have:
* A Spawn Manager object with a `SpawnManager` script attached
* A set of prefabs you want to spawn at random

1. In `SpawnManager`, define a `public GameObject[] randomPrefabs` variable
2. Set the relevant prefabs in the Spawn Manager object's Spawn Manager component
3. In `SpawnManager`, above the `Instantiate` method for spawning the random enemy, determine a random index within the relevant range:
```
int prefabIndex = Random.Range(0, randomPrefabs.Length);
```
4. Within the Instantiate method, define the random prefab, its position(?), and its rotation using `randomPrefabs[prefabIndex]`

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
}
```

## Set up a countdown timer
Adapted from [Unity Forums](https://discussions.unity.com/t/c-countdown-timer/37915/2), and implemented to solve [Challenge 5](https://learn.unity.com/tutorial/challenge-5-whack-a-food?uv=6&projectId=5cf96bdeedbc2a2b475972b3) of the Unity Learn 'Create with Code' tutorial pathway

This assumes you have:
* A Game Manager object with a `GameManager` script attached
* A TextMeshPro Text object to display the timer

1. Set up a couple of new variables in the `GameManager` script:  
```public TextMeshProUGUI timerText;```  
```private float timeLeft = X;```  
where X is the number of seconds the timer should last

2. Add the following IEnumerator method to your `GameManager` script:
```
IEnumerator StartCountdown()
{
	while (isGameActive)
        {
		if (timeLeft == 0)
		{
			GameOver();
		}
		timerText.text = "Time: " + MathF.Round(timeLeft);
		yield return new WaitForSeconds(1.0f);
		timeLeft--;
	}
}
```
This will trigger the Game Over state when the timer hits zero.
  * The order of the code has been adjusted from the original forum post, as other iterations led to odd behaviour, such as the timer text not updating when the timer hit zero.

3. Add `StartCoroutine(StartCountdown());` to `GameManager`'s `StartGame()` method.