# Assorted Useful C# Functions

## [Mathf.Approximately](https://docs.unity3d.com/ScriptReference/Mathf.Approximately.html)
Syntax: `Mathf.Approximately(float a, float b);`
* Compares two floats, and returns `true` if they are similar
* Similarity is defined as whether they are within the smallest possible float value ([Epsilon](https://docs.unity3d.com/ScriptReference/Mathf.Epsilon.html)) of each other
* **This is more reliable than using `==`, as a small loss in precision can otherwise throw off a computation**

## Using [return;](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/jump-statements#the-return-statement) in an if-statement
Syntax:
```
public void SomeFunction()
{
   if (condition)
   {
      return;
   }

   DoSomething();
   DoSomethingElse();
}
```
* A `return` statement terminates execution of a function
* In the above example, if the condition is met, then `DoSomething()` and `DoSomethingElse()` will not be executed, as `SomeFunction()` will terminate
* **How is this any better than an `if (!condition){DoSomething()}` function?**

## [Static class members](https://learn.unity.com/course/2d-beginner-adventure-game/unit/heads-up-ui-display/tutorial/display-character-health-on-the-ui?version=2022.3#64d4e6b4edbc2a6b0b70610a)
If there is only one GameObject with a given script attached (e.g. a UI handler script), then we can make a static member of the class so all references are to that instance.
* **Clarify the benefits of this!**

```
using UnityEngine;

public class LoremIpsum : MonoBehaviour
{
   public static LoremIpsum instance { get; private set; }

   private void Awake()
   {
      instance = this;
   }

   public void SomeFunction()
   {
	…
   }
}
```
* In this first code block, we save [`this`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/this) (the current instance of the `LoremIpsum` class) to the `instance` property

```
using UnityEngine;

public class PlayerController : MonoBehaviour
{
   …

   private void SomeOtherFunction()
   {
      LoremIpsum.instance.SomeFunction();
   }
}
```
* In this second code block, we access the static `LoremIpsum` instance's `SomeFunction()` function

## Start an animation from a random frame
If you have multiple GameObjects with an idle animation, and want them all to start out-of-sync so they don't idle in unison, attach the script below to each of the GameObjects.  
Code from the [Unity forums](https://discussions.unity.com/t/using-cycle-offset-feature-inside-of-animator/172679/3)
```
using UnityEngine;

// Script for randomising the starting frame of an object's idle animation
// Code from https://discussions.unity.com/t/using-cycle-offset-feature-inside-of-animator/172679/3
public class RandomStartingFrame : MonoBehaviour
{
    private Animator m_Animator;

    void Start()
    {
        m_Animator = GetComponent<Animator>();

        // Set a random part of the animation to start from
	// (replace 'Floating' with the name of your idle animation)
        float randomStartPos = Random.Range(0, m_Animator.GetCurrentAnimatorStateInfo(0).length);
        m_Animator.Play("Floating", 0, randomStartPos);
    }
}
```

## [Time.timeScale](https://docs.unity3d.com/6000.2/Documentation/ScriptReference/Time-timeScale.html)
The `Time.timeScale` function lets us adjust how fast time passes in the application. This is useful for pause menus:
```
public void PauseGame()
{
   // Pause time
   Time.timeScale = 0;

   // Show the pause screen
   pauseScreen.SetActive(true);
}

public void UnpauseGame()
{
   // Unpause time
   Time.timeScale = 1;

   // Hide the pause screen
   pauseScreen.SetActive(false);
}
```

## Playing an animation before an object is destroyed
If an animation is coded to play directly before a GameObject is destroyed, the destruction will interrupt the animation
```
m_Animator.SetTrigger("SomeTrigger");
Destroy(gameObject);
```

This can be counteracted by overriding an aspect of the animation state ([as described here](https://discussions.unity.com/t/delete-object-after-animation-2d/100143))
1. Create a new C# script called `DestroyOnExit` or similar, with the following code
```
public class DestroyOnExit : StateMachineBehaviour
{
    public override void OnStateEnter(Animator animator, AnimatorStateInfo stateInfo, int layerIndex)
    {
        Destroy(animator.gameObject, stateInfo.length);
    }
}
```
This will set the animated GameObject to be destroyed after the length of time of the animation
2. In the GameObject's Animator, select the relevant state, click **Add Behaviour** in the Inspector, and add the new `DestroyOnExit` script
3. In the GameObject's main controller script, ensure that you remove `Destroy(gameObject);`, as this is now handled by the Animator