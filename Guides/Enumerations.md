# Enumerations

[**Enumerations**](https://learn.unity.com/tutorial/enumerations) can be used to predefine a subset of values that a constant can take.  
Used in conjunction with a `public` or `[SerializeField]`, we can create a dropdown to define this value in the Inspector.

```
// Define the list of possible values, and expose it to the Inspector as a dropdown
public enum myOption { optionOne, optionTwo, optionThree };
[SerializeField] private myOption _myOption;	// Or `public myOption _myOption`;
```

We can then refer to the defined value using `myOption.optionName` syntax.

```
if (someVariable == myOption.optionOne)
{
	// Do something
}
else if (someVariable == myOption.optionTwo)
{
	// Do something else
}
else if (someVariable == myOption.optionThree)
{
	// Do another thing
}
```
We can also use [switch statements](SwitchStatements.md) instead of if-else.

[This article](https://m-ansley.medium.com/enums-an-introduction-to-enumeration-types-with-unity-e4340c883da8) is another useful introductory resource for enumerations.