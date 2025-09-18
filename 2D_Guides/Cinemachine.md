# [Cinemachine](https://learn.unity.com/course/2d-beginner-adventure-game/unit/enhance-and-polish/tutorial/implement-a-dynamic-camera?version=2022.3)

Guide to using Unity's [**Cinemachine**](https://docs.unity3d.com/Packages/com.unity.cinemachine@3.1/manual/index.html) package for a following camera in a 2D experience, adapted from the [2D Beginner: Adventure Game](https://learn.unity.com/course/2d-beginner-adventure-game?version=2022.3) tutorial

## Setting up the camera

1. Ensure that the Cinemachine package is installed via **Package Manager**
2. Create a **Cinemachine > 2D Camera** in the Hierarchy
3. In the 2D Camera's **Cinemachine Camera** component, expand the **Lens** menu and set **Orthographic Size** for the desired field of view (the Unity tutorial suggests 5)
4. In the 2D Camera's **Cinemachine Camera** component, drag the **PlayerCharacter** from the Hierarchy to **Tracking Target**

## Keeping the camera in-bounds

1. At the bottom of the Cinemachine Camera component, select **Add Extension > CinemachineConfiner2D**
2. In the Hierarchy, create an empty GameObject, and add a **Polygon Collider 2D** component
3. Edit the collider to define the boundaries of the camera's movement
* These points can be manually tidied up by expanding the **Polygon Collider 2D > Points > Paths > Element 0** dropdown and manually adjusting the points' coordinates
4. In the 2D Camera's **Cinemachine Confiner 2D** component, drag the previously-defined Polygon Collider 2D GameObject into the **Bounding Shape 2D** field
5. Add a new layer (e.g. 'Confiner') to the Polygon Collider 2D GameObject
6. Use the [LayerCollisionMatrix](REAMD.md) to disable the 'Confiner' layer's interaction with **all** other layers

