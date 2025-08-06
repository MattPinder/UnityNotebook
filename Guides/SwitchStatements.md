# Switch Statements

[Switch statements](https://learn.unity.com/tutorial/switch-statements) are an elegant alternative to if-else.  

The response to each potential value of the given variable (given in the `switch` statement), we define a `case` containing what should happen if the variable equals that value.  
We terminate each `case` with a `break;` to break out of the switch statement.  
We end the switch statement with a `default` to catch any values not covered by a `case`.

```
switch (someVariable)
{
	case optionOne:
		// Do something
		break;
	case optionTwo:
		// Do something else
		break;
	case optionThree:
		// Do another thing
		break;
	default:
		// Optional catch-all for other values
		break;
}
```

These are often used with [enumerations](Enumerations.md).