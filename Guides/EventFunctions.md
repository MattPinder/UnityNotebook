# Event functions in Unity
Incomplete list of predefined functions accessible to all MonoBehaviour scripts
* For more in-depth documentation, see the [Unity manual page](https://docs.unity3d.com/6000.0/Documentation/Manual/event-functions.html)

## Initialisation events

### `Awake()`
`Awake` is called when an object is activated, and **before** any `Start` functions

### `Start()`
"`Start` is called once before the first execution of `Update` after the MonoBehaviour is created" (from MonoBehaviour script template)
* The function is called once, straightaway

## Regular update events

### `Update()`
"`Update` is called once per frame" (from MonoBehaviour script template)
* "`Update` is called before the frame is rendered and before animations are calculated" (from Unity documentation)

### `FixedUpdate()`
Called once per frame, **before** `Update`
* Useful for physics-related code, e.g. movement of an object

### `LateUpdate()`
Called once per frame, **after** `Update`
* Useful for camera movement-related code, to prevent the camera from shuddering
* Also useful for code that overrides the effect of an animation (according to Unity documentation)

## Physics Events

### `OnCollisionEnter(Collision collision)`
Called when one object collides with another, provided both objects have a collider

### `OnCollisionStay(Collision collision)`
Called when one object remains in contact with another, provided both objects have a collider

### `OnCollisionExit(Collision collision)`
Called when one object leaves contact with another, provided both objects have a collider

### `OnTriggerEnter(Collider other)`
Called when one object collides with another, provided at least one object has 'Is Trigger' enabled on their collider

### `OnTriggerStay(Collider other)`
Called when one object remains in contact with another, provided at least one object has 'Is Trigger' enabled on their collider

### `OnTriggerExit(Collider other)`
Called when one object leaves contact with another, provided at least one object has 'Is Trigger' enabled on their collider



