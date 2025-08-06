# Data Structures

## Arrays

Arrays are represented by **square brackets**

### Defining arrays

```
public string[] myArray;

public string[] myArray = new string[] { "hello", "there", "General", "Kenobi" };
```

### When to use arrays
* When there are a **fixed number of elements**
* When there is a **fixed order of elements**

## Lists

Lists are represented by angle brackets

Lists require the namespace `System.Collections.Generic`

### Defining lists

```
public List<string> myList;

public List<string> myList = new List<string>() { "hello", "there", "General", "Kenobi };
```

### When to use lists
* When the number of elements is being changed
* When the order of elements is not important

## Dictionaries

Dictionaries are represented by angle brackets

Dictionaries require the namespace `System.Collections.Generic`

### Defining dictionaries

```
public Dictionary<int, string> myDictionary;

public Dictionary<int, string> myDictionary = new Dictionary<int, string>()
{
	{ 1, "hello" },
	{ 2, "there" }
};
```

### When to use dictionaries
* When you want to pair values together