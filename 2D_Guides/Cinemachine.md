# [Cinemachine](https://learn.unity.com/course/2d-beginner-adventure-game/unit/enhance-and-polish/tutorial/implement-a-dynamic-camera?version=2022.3)

Guide to using Unity's [**Cinemachine**](https://docs.unity3d.com/Packages/com.unity.cinemachine@3.1/manual/index.html) package for a following camera in a 2D experience, adapted from the [2D Beginner: Adventure Game](https://learn.unity.com/course/2d-beginner-adventure-game?version=2022.3) tutorial

## Setting up the camera

1. Ensure that the Cinemachine package is installed via **Package Manager**
2. Create a **Cinemachine > Targeted Cameras > 2D Camera** in the Hierarchy
3. In the 2D Camera's **Cinemachine Camera** component, expand the **Lens** menu and set **Orthographic Size** for the desired field of view (the Unity tutorial suggests 5)
4. In the 2D Camera's **Cinemachine Camera** component, drag the **PlayerCharacter** from the Hierarchy to **Tracking Target**

## Keeping the camera in-bounds

1. At the bottom of the Cinemachine Camera component, select **Add Extension > CinemachineConfiner2D**
2. In the Hierarchy, create an empty GameObject, and add a **Polygon Collider 2D** component
3. Edit the collider to define the boundaries of the camera's movement
* These points can be manually tidied up by expanding the **Polygon Collider 2D > Points > Paths > Element 0** dropdown and manually adjusting the points' coordinates
4. In the 2D Camera's **Cinemachine Confiner 2D** component, drag the previously-defined Polygon Collider 2D GameObject into the **Bounding Shape 2D** field
5. Add a new layer (e.g. 'Confiner') to the Polygon Collider 2D GameObject
6. Use the [LayerCollisionMatrix](README.md) to disable the 'Confiner' layer's interaction with **all** other layers

## Adjusting the camera bounds in code
If your level changes size, it may be necessary to redefine the bounds of the camera in scripts  
**Note**: these instructions assume you've been following the above-mentioned Unity tutorial, and are implementing the optional objective of making the stage larger each level (in this case, growing the stage by one square each level)  
It also assumes that the starting coordinates of the bounding box are: (-6.1, -2.1), (-6.1, 8.1), (11.9, 8.1), (11.9, -2.1)  
The camera acts weirdly if you try to set its bounding box *too* close to the camera start position, so a bit of wiggle room is required

1. In the `GameManager` script, add some variables to:
 * Contain camera confiner coordinates
 * Define the Cinemachine confiner and the bounding box
```
public class GameManager : MonoBehaviour
{
   // Fixed values denoting the initial values of the starting boundary
   private float m_minX = -6.1f;
   private float m_minY = -2.1f;
   private float m_maxXstart = 11.9f;
   private float m_maxYstart = 8.1f;

   // Changeable values denoting the growth of the bounding box
   private float m_maxX;
   private float m_maxY;

   // Set the Cinemachine camera in the Inspector
   public CinemachineConfiner2D cinemachineConfiner;

   // Set the Polygon Collider 2D in the Inspector
   public PolygonCollider2D cameraConfiner

   ...
}
```
2. Add a function to `GameManager` to change the size of the bounding box
```
private void ChangeCameraBounds()
{
   // Define the new bounding box
   Vector2[] cameraBounds = new Vector2[]
  {
      new Vector2(m_minX, m_minY),
      new Vector2(m_minX, m_maxY),
      new Vector2(m_maxX, m_maxY),
      new Vector2(m_maxX, m_minY)
  };

   // Send the new box coordinates to the camera confiner
   cameraConfiner.SetPath(0, cameraBounds);

   // Clear the previous bounding box so the Cinemachine has to recalculate from the new coordinates
   cinemachineConfiner.InvalidateBoundingShapeCache();
}
```
3. In the `StartNewGame()` function of `GameManager`, reset the bounding box to its original size
 * If you're also changing the board size, also reset the board size now (we'll implement this later)
```
public void StartNewGame()
{
   // Reset the following camera
   m_maxX = m_maxXstart;
   m_maxY = m_maxYstart;
   ChangeCameraBounds();

   ...

   boardManager.Clean();
   boardManager.ResetBoardSize();
   boardManager.Init();

   ...
}
```
4. In the `NewLevel()` function of `GameManager`, tick up the size of the bounding box
```
public void NewLevel()
{
   ...

   // Increase size of camera confiner, but keep its bottom-left point anchored
   m_maxX++;
   m_maxY++;
   ChangeCameraBounds();

   ...
}
```
**The steps below are for if you're also changing the board size, as well as the bounding box size**

5. Now in `BoardManager`, adjust the board size variables at the start of the script to include both current and starting dimensions
```
public class BoardManager : MonoBehaviour
{
   ...

   public int startWidth = 8;
   public int startHeight = 8;
   private int boardWidth;
   private int boardHeight;

   ...
}
```
6. At the bottom of `BoardManager`'s `Clean()` function, tick up the board dimensions so that it's ready to clean up the next (bigger) board
```
public void Clean()
{
   ...

   // Increase board size for next round
   boardWidth++;
   boardHeight++;
}
```
7. Add a function to `BoardManager` to reset board size when restarting the game
```
public void ResetBoardSize()
{
   boardWidth = startWidth;
   boardHeight = startHeight;
}
```