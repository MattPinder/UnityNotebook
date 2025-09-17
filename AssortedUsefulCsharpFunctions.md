# Assorted Useful C# Functions

## `[Mathf.Approximately](https://docs.unity3d.com/ScriptReference/Mathf.Approximately.html)`
Syntax: `Mathf.Approximately(float a, float b);`
* Compares two floats, and returns `true` if they are similar
* Similarity is defined as whether they are within the smallest possible float value ([Epsilon](https://docs.unity3d.com/ScriptReference/Mathf.Epsilon.html)) of each other
* **This is more reliable than using `==`, as a small loss in precision can otherwise throw off a computation**