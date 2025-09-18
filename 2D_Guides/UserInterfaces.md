# [User Interfaces](https://learn.unity.com/course/2d-beginner-adventure-game/unit/heads-up-ui-display/tutorial/create-a-health-display-with-ui-toolkit?version=2022.3)
Guide to using Unity's **UI Toolkit** system in a 2D experience, adapted from the [2D Beginner: Adventure Game](https://learn.unity.com/course/2d-beginner-adventure-game?version=2022.3) tutorial

## Creating a UI Document
This document is where the structure of the UI are stored

1. In a relevant Project directory, right-click and create a **UI Toolkit > UI Document**
2. Rename the UI Document, and double-click it to open the **UI Builder** window (and dock it)
3. In the Hierarchy, right-click and select **UI Toolkit > UI Document**, and set the UI Document from the previous steps as the **Source Asset**
4. In the UI Builder window, select the `.uxml` in the **UI Builder Hierarchy**, and in the **UI Inspector > Canvas Size** dropdown, tick **Match Game View**
5. In the **Canvas Background** dropdown, select the colour and transparency of the UI background

## Example - Health Bar
### Health bar background
1. Ensure that the UI Builder window/tab is expanded enough to see the **Library** in the bottom-left
2. Drag a **Library > Standard > Containers > VisualElement** from the Library into the Hierarchy, to contain the health bar background
3. With the health bar background selected in the Hierarchy, in **Inlined Styles > Background**:
 * Set **Image** to **Sprite**
 * Select a health bar background sprite in the **Image** box
 * Set **Scale Mode** to **scale-to-fit** (the icon on the right)
4. Under **Inlined Styles > Flex**, set **Grow** to **0**, so that the height can be set manually
5. Under **Inlined Styles > Size**, set the **Width** and **Height** appropriately, either as a percentage or by pixel value
6. In the UI Document's main Inspector, select the asset at **UI Document > Panel Settings**, then click this in the Project window to open its Inspector window
 * Set **Scale Mode** to **Scale with Screen Size**
 * Set **Scale Mode Parameters > Screen Match Mode** to **Match Width or Height**
 * Set **Reference Resolution** to a size appropriate to your screen (e.g. X 1920, Y 1080)
7. In the UI Builder, rescale the health bar background until it looks as intended

### Character portrait
1. As in step 2 of the previous section, drag a **VisualElement** container into the UI Builder Hierarchy, on top of the health bar background so that it becomes a child of that container
2. With the new character portrait container selected in the Hierarchy, in **Inlined Styles > Background**:
 * Set **Image** to **Sprite**
 * Select a character portrait sprite in the **Image** box
 * Set **Scale Mode** to **scale-to-fit** (the icon on the right)
3. Under **Inlined Styles > Position**, set the **Position** to **Absolute**
4. Resize the portrait in the Viewport to an appropriate size

### Health bar
1. As before, drag a **VisualElement** container into the UI Builder Hierarchy, on top of the health bar background so that it becomes a child of that container (not a child of the character portrait). This will be the **health bar container**
2. Add another container as a child object of the health bar container. This will be the **health bar** itself
3. With the **health bar** child element selected in the Hierarchy, in **Inlined Styles > Background**:
 * Set **Image** to **Sprite**
 * Select a health bar sprite in the **Image** box
 * Ensure **Scale Mode** is set to **stretch-to-fill** (the icon on the left; should be the default)
4. As objects are drawn from top to bottom in the UI Builder Hierarchy, drag the character portrait to the bottom (ensuring it remains a child of the health bar background but **not** of the health bar container)
5. Under **Inlined Styles > Position**, set the **Position** to **Absolute**
6. Resize the health bar **container** (not the health bar itself) in the Viewport, until it covers the appropriate part of the health bar background

### Coding the health bar
1. Attach a new C# script (UIHandler) to the UI Document in the main Hierarchy
2. Add the `using UnityEngine.UIElements;` namespace to the script
3. In Start(), get the attached UI Document component
```
UIDocument uiDocument = GetComponent<UIDocument>();
```
4. To access the health bar, use the `Q` ((query)[https://docs.unity3d.com/6000.2/Documentation/Manual/UIE-UQuery.html]) function:
```
VisualElement healthBar = uiDocument.rootVisualElement.Q<VisualElement>("HealthBar");
```
5. Add an instruction to resize the health bar based on the player's health
```
healthBar.style.width = Length.Percent(CurrentHealth * 100.0f);
```
6. For the full implementation of the above and the following steps, see the Unity tutorial
 * See also the tutorial on [adding a UI element for NPC dialogue](https://learn.unity.com/course/2d-beginner-adventure-game/unit/characters-and-interaction-mechanics/tutorial/display-character-dialogue-using-raycasting?version=2022.3)