# List of keywords (access modifiers, return types, etc.) and when to use them
**Note**: This list is partial, primarily based on keywords encountered during the Unity Learn tutorials.
* See [the Microsoft website](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/) for a more complete list.

**Note 2**: This list currently considers only **variables** and **methods**; I'll update it as my own understanding improves.

#### `public`
`public int x;`  
No restrictions on access; can be viewed in the Unity Inspector and accessed by other scripts.
* Use with variables and methods

#### `private`
`private int x;`  
Most restrictive keyword; can only be accessed within the class in which it was declared.
* Use with variables and methods

#### `[SerializeField]`
`[SerializeField] int x;`  
The variable will be visible and editable in Unity Inspector (like a public variable), but not accessible outside of its class (like a private variable).  
Useful if you need to adjust values in the Inspector but don't want other scripts accessing or editing it.
* Use with variables only

#### `protected`
`protected int x;`  
The variable is only accessible within its class (like private), or those inheriting from it (unlike private).
* Use with variables only

#### `readonly`
`public readonly int x;`  
The value of a 'readonly' is set once and then remains frozen (a 'runtime constant').
* Use with variables only

#### `const`
`public const int x = 42;`  
The value of a `const` is given straightaway, and is immutable afterwards (a 'compile-time constant').
* Use only for values that aren't going to change
* Not used with methods

#### `static`
Use `static` for global keywords, e.g. a function that you want to exist all the time
* [This section requires expansion]

#### `void`
`void SpawnObject()`  
Return type for methods that don't return a value, i.e. methods that only **do** something.
* Use with methods only

#### `virtual`
`public virtual string GetName()`  
Designates a method that can be overridden/modified in a derived child class.
* Use with methods only

#### `abstract`
`public abstract string GetName()`  
Designates a method that **must** be overridden/modified in a derived child class.
* Use with methods only

#### `override`
`public override string GetName()`  
Allows modification of a `virtual`- or `abstract`-type method.
* Use with methods only