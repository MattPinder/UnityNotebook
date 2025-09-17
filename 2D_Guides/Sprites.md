# Sprites
Tips on working with sprites, adapted from Unity's [2D Beginner: Adventure Game](https://learn.unity.com/course/2d-beginner-adventure-game?version=2022.3) tutorial

## [Drawing sprites based on their Y-axis position](https://learn.unity.com/course/2d-beginner-adventure-game/unit/game-environment-and-physics/tutorial/create-decorative-objects-using-sprites?version=2022.3#64d4b723edbc2a62a281ae28)

By adjusting Unity's draw settings, we can create more realistic effects with the player moving behind and in front of decorative sprites

1. In the project's **Renderer2D** Settings asset:
 * Under **General**, set **Transparency Sort Mode** to **Custom Axis**
 * Set the **Transparency Sort Axis** values to **X = 0**, **Y = 1**, **Z = 0**, so sprites are drawn based on their Y-axis position
2. In each sprite/prefab's **Sprite Renderer** component:
 * Set **Sprite Sort Point** to **Pivot** (the default, Center, means that it draws sprites based on their relative midpoints, which may not always be desired)
 * Click **Open Sprite Editor**, set the **Pivot** to **Bottom Center**, and click **Apply**

## [Tile sprites to avoid stretching](https://learn.unity.com/course/2d-beginner-adventure-game/unit/game-environment-and-physics/tutorial/create-decorative-objects-using-sprites?version=2022.3#64d4b9b9edbc2a62609f2a84)
When resizing decorative sprites, it can sometimes be desirable to tile them, rather than stretching and distorting them

1. Ensure the sprite prefab you're working with has its **Transform > Scale** set to **(1, 1, 1)**
2. In the **Sprite Renderer** component:
 * Set the **Draw Mode** to **Tiled** (the default, Simple, causes stretching when sprite size is changed)
 * Set the **Tile Mode** to **Adaptive** (the default, Continuous, adds more tiles as the sprite is stretched, but continuously, so you can end up with partial repeats of the sprite)
3. Find the sprite's original Texture 2D file in the Project window, set its **Mesh Type** to **Full Rect**, and click **Apply**