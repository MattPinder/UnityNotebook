# Coroutines and IEnumerators

See Unity tutorial [here](https://learn.unity.com/tutorial/coroutines)

* Coroutines are used when you want to trigger an event either over time or with a delay
* Coroutines use memory in an inefficient way, however, so should be used infrequently and with care

## How to structure a coroutine
1. Create a method that contains `StartCoroutine()`
2. Create a method with return type `IEnumerator` that is called by the above method
3. Ensure that the IEnumerator method contains a line with `yield return X`, e.g.:
  * `yield return null;`, which triggers the coroutine every frame
  * `yield return new WaitForSeconds(X);`, which triggers the coroutine every X seconds

## Example syntax
```
using System.Collections;

	public float defaultDuration;

	public void StartFadeOut()
	{
		StartCoroutine(FadeOut(defaultDuration));
	}

	// ...

	private IEnumerator FadeOut(float duration)
	{
		float elapsedTime = 0.0f;

		while (alpha >= 0.0f)
		{
			SetAlpha(1 - (elapsedTime / duration));
			elapsedTime += Time.deltaTime;
			yield return null;
		}
	}
```

## Other notes
* `yield return`
  * `yield return` doesn't have to be at the end of the function
  * Multiple `yield return`s can be included in a single function
* `StopAllCoroutines()` can be used to stop all coroutines running on the script it's attached to