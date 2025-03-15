# [Shaders](https://learn.unity.com/pathway/creative-core/unit/shaders-and-materials/tutorial/66fc2483edbc2a205badc80d?version=6)
"A shader is a script that applies the properties contained in a material to render the meshes of your 3D objects to the 2D image on your screen. Each shader is written for a specific render pipeline."

## [Shader Graph](https://learn.unity.com/pathway/creative-core/unit/shaders-and-materials/tutorial/66fc4313edbc2a0023a2538a?version=6)
To create more dynamic effects, Shader Graph can be used to create custom shaders
* Accessed by creating a new **Shader Graph > URP > Lit Shader Graph** (or other applicable type) in the Project window, and double-clicking it
* This topic is not easy to summarise, so I recommend going through the above-linked tutorial for more details on its basic usage

# Materials

## Surface Input maps
* **Base Map** - X, with a colour picker to select the material's overall colour
  * Base Map textures can be 3- or 4-channel (with or without transparent alpha sections)
  * If they are tiled textures (i.e. repeating), the repetition can be adjusted using **Tiling** and **Offset**, at the bottom of Surface Inputs
* **Specular/Metallic Map** - used to control how metallic/shiny a material looks
  * Specular Map is 3 channel (RGB); Metallic Map is 1 channel (greyscale)
* **Normal Map** - sets the apparent direction of each pixel to simulate texture (3 channel)
* **Height Map** - sets the apparent height of each pixel to simulate depth (1 channel; green only if given as 3 channel)
* **Occlusion Map** - adds shadows to certain areas (1 channel)
* **Emission** - enabling this and adding an Emission Map creates a glow in specified areas

## Detail Input maps
These are used to give additional detailing by applying **microsurface maps**
* **Mask** - an alpha channel map shielding certain areas from the Base/Normal detail maps
* **Base Map**
* **Normal Map**

## [Specular and Metallic Workflows](https://learn.unity.com/pathway/creative-core/unit/shaders-and-materials/tutorial/66fc273fedbc2a242a3549f9?version=6)
Two methods of making a material look metallic, which can be toggled under **Surface Options > Workflow Mode**
* Specular Workflow makes an object look metallic in a way more consistent with real physics
  * Adjusting the **Smoothness** makes the object shinier
  * Higher Specularity (?) makes the colour approach white
  * Setting colours other than white/the Base Map colour can produce interesting effects
* Metallic Workflow makes an object look metallic, but in a simpler way that doesn't strictly follow real physics
  * Adjusting the **Metallic/Smoothness** sliders make the surface more or less reflective

## [Transparent and Translucent effects](https://learn.unity.com/pathway/creative-core/unit/shaders-and-materials/tutorial/66fc3c6dedbc2a001f6c1bad?version=6)
* Under the Material's **Surface Options > Surface Type** dropdown, we can toggle between Opaque and Transparent
* Enabling **Preserve Specular Lighting** shows realistic light reflections on the transparent surface
* Setting **Render Face** to Both means both sides of the object will be shown (otherwise, we can see through to the missing back half!)
* Transparency can be adjusted in the **alpha channel* of the Base Map
* If a material's Base Map has sections intended to be transparent, enabling **Alpha Clipping** reveals a Threshold slider that lets us render these grey areas transparent (e.g. applying a leaf-shaped texture to an otherwise square Plane)

## [Bump Mapping](https://learn.unity.com/pathway/creative-core/unit/shaders-and-materials/tutorial/66fc3e33edbc2a0023b51792?version=6)
Adding details to a surface using maps, rather than generating a complex, high-poly mesh
* Uses Normal Maps and Height Maps
  * **Normal Maps** give the direction that each pixel faces, encoded in RGB values
  * **Height Maps** give the relative height of each pixel, encoded in a single channel (greyscale)

## [Occlusion Mapping](https://learn.unity.com/pathway/creative-core/unit/shaders-and-materials/tutorial/66fc4160edbc2a0023a25353?version=6#66fc4160edbc2a0023a25356)
As light can reflect oddly or not give the desired effect, occlusion maps can be used to add shadow to the intended areas, to give added depth

## [Fixing materials](https://learn.unity.com/pathway/creative-core/unit/shaders-and-materials/tutorial/66fc25f4edbc2a1d1d970f04?version=6#66fc25f4edbc2a1d1d970f08)
If materials appear pink/purple, it likely means it was intended for a different render pipeline
* To fix a single broken material:
  * Set the Material's Shader to one compatible with the project, e.g. **Universal Render Pipeline/Lit**
  * If this fails, select the Material, then click **Edit > Rendering > Materials > Convert Selected Built-in Materials to URP**
* To fix multiple broken materials:
  * Open **Window > Rendering > Render Pipeline Converter**
  * Ensure that the dropdown is correctly set (most likely the default, **Built-in to URP**)
  * Enable **Material Upgrade**, then click **Initialize Converters**
  * Select the material(s) you want to fix, then click **Convert Assets**