# Tilemaps
Information adapted from Unity's [2D Beginner: Adventure Game](https://learn.unity.com/course/2d-beginner-adventure-game?version=2022.3) tutorial

## Terminology

* **Tile**: An asset referencing a particular sprite
* **Tileset**: An image file containing multiple sprites, which can be sliced after importing into Unity
  * Also known as a **sprite sheet** or **sprite atlas**
* **Tile palette**: A window/tab for laying out tiles
* **Tilemap**: The layout of tiles in the scene

## From Tileset to Tile Palette to Tilemap
1. Import your tileset PNG file into Unity, and select it in the Project window
2. In the Inspector:
 * Set **Sprite Mode** to **Multiple**
 * Set the **Pixels Per Unit** to an appropriate value such that the tile fits into the Scene view grid cell (try 64? 100?)
 * Click **Apply**, then open **Sprite Editor**
3. In the Sprite Editor:
 * Open the **Slice** dropdown
 * Set **Type** to **Grid By Cell Count**
 * Set the **Column & Row** parameters such that the tileset is sliced correctly (previewed by a red grid on the image)
 * Click **Slice**, then **Apply**, and close the Sprite Editor
 * Check the Project window; there should be (column x row) sprites as children of the original image
4. Open the **Window > 2D > Tile Palette** window (and dock it)
 * Open the **No Valid Palette** dropdown, select **Create New Tile Palette**, name the new palette, and click **Create**
 * Save the new palette in an appropriate directory
 * Drag the tileset (the original image) from the Project window into the Tile Palette window, and save in the previous directory
 * Repeat Step C for all relevant tiles
5. In the Hierarchy:
 * Right-click and create **2D Object > Tilemap > Rectangular** (or whichever shape suits your project)
 * Select the new **Grid > Tilemap** child object, and set **Tilemap Renderer > Additional Settings > Order in Layer** to -10 (or a sufficiently large negative number), to ensure it is rendered *below* other entities in the scene
 * If you want to have multiple layers of tiles (e.g. if you have archways that the player should pass below), right-click the **Grid** parent object and create a new **2D Object > Tilemap > Rectangular** child object with a higher ** Order in Layer** value
6. In the Tile Palette, ensure that the dropdown at the top of the palette is set to the correct tilemap before painting on the scene (to ensure you don't paint an archway *under* the player, for example)

## Tilemap Collision
Adding collision to certain tiles can prevent the player from walking on water, walls, etc.
1. Select the Tilemap in the Hierarchy, and add both a **Tilemap Collider 2D** and a **Composite Collider 2D** component
* This will also add a Rigidbody 2D component, as a requirement of Composite Collider 2D
2. In the Tilemap Collider 2D component, set **Composite Operation** to **Merge**
3. In the Rigidbody 2D component, set **Body Type** to **Static**
4. In the Project window, select all tiles that should **not** have collision, and set the **Collider Type** dropdown to **None** in the Inspector (by default, tiles will have Sprite collision)