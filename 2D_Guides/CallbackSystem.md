# [Callback system](https://learn.unity.com/course/2d-roguelike-tutorial/tutorial/add-a-food-resource?version=6.0)
Adapted from Unity's [Create a 2D Roguelike Game](https://learn.unity.com/course/2d-roguelike-tutorial?version=6.0) tutorial

A [callback system] is used to call methods when a given event happens (e.g. when a turn passes in a turn-based game).  
The example below is a basic example from Unity's tutorial, which enables us to trigger various actions during each turn of the turn-based game.

1. Set up a `System.Action` callback, using the C# keyword `event`
```
public event System.Action OnTick;
```

2. Inside the TurnManager's `Tick()` method, include the following:
```
OnTick?.Invoke()
```
* `Invoke()` calls all methods registered to `OnTick`
* `?` tests whether `OnTick` is null; if not, it will call `Invoke()`

3. Add the method to be performed each turn to `OnTick`, e.g.:
```
void Start()
{
   TurnManager = new TurnManager()
   TurnManager.OnTick += OnTurnHappen;
   …
}

void OnTurnHappen()
{
   // Something that should happen each turn
}
```
