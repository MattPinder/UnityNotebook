# Encapsulation, Getters and Setters
Note: much of the code and details below are derived from Unity Learn's tutorial (see [here](https://learn.unity.com/tutorial/encapsulation-in-object-oriented-programming-2?contentId=60b7b847edbc2a0020830745&missionId=5f779f1eedbc2a00201f3e5e&pathwayId=5f7e17e1edbc2a5ec21a20af&uv=6)), but organised here to aid my own memory in future

## Encapsulation
Making sure that code can only be used as intended, by making variables etc. available only to those processes that need them.  
This can often be accomplished by setting variables to `private`, so they cannot by altered by other scripts.

## Properties
`public static MainManager Instance { get; private set; }`  
Using **getters** and **setters** allows us to control 'read and write access' to a given variable, ad makes the variable a **property**.

The `{ get; private set; }` syntax is the simplest type - an **auto-implemented property** - which makes the variable read-only; other classes can **get** the value, but the `private` keyword means it can only be **set** from within the class.

## Setter validation
Setters can also be used to restrict how a value is set; for this, a **backing field** is required - "a private variable that stores the data exposed by the public property."

Example from Unity Learn: ensuring that a value can only be set as a positive number

```
private float m_ProductionSpeed = 0.5f;		// Private backing field
public float ProductionSpeed			// Public property
{
	get { return m_ProductionSpeed; }	// The getter returns the backing field
	set
	{
		if (value < 0.0f)
		{
			// Return an informative error if trying to set incorrectly
			Debug.LogError("You can't set a negative production speed!");
		}
		else
		{
			m_ProductionSpeed = value;	// The setter changes the backing field
		}
	}
}
```

The ProductionSpeed of a given entity can then be accessed and altered in other scripts using `variablename.ProductionSpeed`:

```
private ResourcePile m_CurrentPile = null;

m_CurrentPile.ProductionSpeed *= ProductivityMultiplier;
```