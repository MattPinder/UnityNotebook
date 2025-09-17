# [Sprite Animation](https://learn.unity.com/course/2d-beginner-adventure-game/unit/characters-and-interaction-mechanics/tutorial/create-2d-sprite-animations?version=2022.3)

## Setting up a new Animation Controller
1. Select the relevant GameObject/prefab, and add an **Animator** component
2. In an appropriate Project subfolder, create an **Animation > Animator Controller** for the GameObject/prefab
3. In the GameObject/prefab's Animator component, set the newly-created Animator Controller in the **Controller** box

## Creating a clip
1. Open **Window > Animation > Animation** (and dock it)
2. With the relevant GameObject/prefab selected, click **Create** in the Animation window, and save in a relevant folder
3. Adjust the Pixels per Unit if required (see [Sprites guide](Sprites.md))
4. Shift-select the relevant sprites for the clip and drag them into the Animation window
 * This should create an animation using the drag-and-dropped sprites
5. Click the **⋮** dropdown in the Animation window and select **Show sample rate**, then adjust the **Samples** to speed up/slow down the animation cycle
6. An animation can be flipped (e.g. a character walking right instead of left) by selecting **Add Property > Sprite Renderer > Flip X** and enabling it for all frames of the animation

## Blend Trees
Blend trees allow a different animation to be selected based on a parameter, such as playing a different walk animation depending on the player's move direction (the example from the Unity tutorial linked in the title, which will be followed here)

1. Open **Window > Animation > Animator** (and dock it)
 * This is a different window to the Animation window used in the previous section!
2. Ensure the relevant GameObject/prefab is selected, right-click in the layout area of the Animator window, and select **Create State > From New Blend Tree**
3. Double-click the new Blend Tree to view its Inspector, and set its **Blend Type** (e.g. 2D Simple Directional if we're dealing with horizontal and vertical movement)
4. In the Parameters tab on the left-hand side of the layout area, create two float parameters for **Move X** and **Move Y**
5. In the Inspector, set Move X and Move Y as the two **Parameters**
6. Assuming different animations for up/down/left/right movement, create four **Motion** fields, assign the relevant animation clips to each, and set relevant parameters for each direction (e.g. Pos X = -1, Pos Y = 0 for moving left)
 * By pressing Play in the **Blend Tree** preview at the bottom of the Inspector, and moving the red dot around the visualisation, we can see how these animations look
7. In the script which determines the GameObject/prefab's movement, define the object's Animator component
```
private Animator animator;

void Start()
{
   animator = GetComponent<Animator>();
}
```
8. In the same script, where movement is determined, set the floats within the animator appropriately. For example, if the object is moving vertically, with the `direction` variable determining up/down direction:
```
animator.SetFloat("Move X", 0);
animator.SetFloat("Move Y", direction);
```

## Animation transition settings
Selecting the transition (white arrow) between two animations reveals a number of settings:
* **HasExitTime** - if enabled, this setting forces the first animation to finish before transitioning to the second; if disabled, the transition occurs immediately when the conditions are fulfilled
* **Conditions** - the list of conditions that must be met before an animation transition will occur; these parameters must be passed to the Animator from scripts in the same fashion as Step 8 above (`animator.SetFloat`, `animator.SetTrigger`, etc.)
 * Trigger parameters, unlike Booleans, are expended when used; you set the trigger, the animation transition occurs, and the trigger becomes reset to False