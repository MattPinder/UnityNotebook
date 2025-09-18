# [Particle System](https://learn.unity.com/course/2d-beginner-adventure-game/unit/enhance-and-polish/tutorial/create-2d-particle-effects?version=2022.3)
Guide to using Unity's **Particle System** in a 2D experience, adapted from the [2D Beginner: Adventure Game](https://learn.unity.com/course/2d-beginner-adventure-game?version=2022.3) tutorial

1. Prepare the spritesheet as described for the tileset in the [Tilemaps](Tilemaps.md) tutorial
2. In the Hierarchy, right-click and add **Effects > Particle System** (and pause the particle simulation that starts)
3. In the Inspector, open **Particle System > Texture Sheet Animation**:
 * Set the **Mode** dropdown to **Sprites**
 * Add a field for each of the desired sprites, and add each sprite to the list
 * Set **Start Frame** to **Random Between Two Constants**, set the first to **0** and the second to the number of sprites added above (the number will change to a float just below that value)
 * Select **Frame Over Time**, right-click the key frame on the right, and click **Delete Key**, resulting in a flat line
4. Use the **Shape** module to adjust the size and shape of the area that the particles spawn in
5. For added randomness, adjust the **Start Lifetime**, **Start Speed**, and **Start Size** parameters, making them **Random Between Two Constants**
6. For a more natural fade-out:
 * Adjust the **Colour over Lifetime** module such that the end point has an alpha of 0
 * Adjust the **Size over Lifetime** to shrink to zero over time
7. Turn the **Particle System** into a prefab, which can now be added as a child to any relevant GameObjects
 * If the GameObject is moving, set the Particle System's **Simulation Space** to **World**, so that the particles move relative to worldspace, not the parent GameObject