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












