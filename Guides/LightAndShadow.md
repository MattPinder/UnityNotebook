# Settings affecting light
To see various light-related displays in the Scene view, check the dropdown beside Debug Draw Mode

## Types of light
* **Directional Light** - see below
* **Point Light** - sends light in all directions from the source (e.g. lamps)
* **Spot Light** - sends light in a cone from the source (e.g. flashlights)
* **Area Light** - sends light in a rectangle (e.g. strip lights)
  * Area lights must be baked
* **Emissive materials** - materials that give off light

## Light Modes
* **Realtime** - Light from this source is calculated in realtime
* **Baked** - Light from this source is calculated beforehand, and baked into the lightmap 
* **Mixed** - Combines realtime shadows with baked light
  * Requires more processing power, but improves the quality of shadows

## General settings found on light sources
* **Range** - how far the light reaches from the source
* **Intensity** - how bright the light is
* **Indirect Multiplier** - how bright light is as it bounces off of surfaces
  * Below 1, the light grows dimmer with each bounce, as in real life
  * Above 1, the light becomes brighter with each bounce
* **Colour** - the colour of the light
* **Mode** - select the source's light mode (see above)

## [Default Directional Light](https://learn.unity.com/pathway/creative-core/unit/lighting/tutorial/670fecabedbc2a008aa0a997?version=6)
This emulates the sun or moon in the scene
* Adjusting the **Rotation** mimics the position of the sun in the sky
* Can also adjust the Colour, Intensity, and Indirect Multiplier

## [Skybox](https://learn.unity.com/pathway/creative-core/unit/lighting/tutorial/670fecabedbc2a008aa0a997?version=6)
This emulates the sky and any surrounding environment (e.g. buildings, mountains) in the scene
* Can be either:
  * **Textured**: Using material textures
  * **Procedural**: Using properties of the material
* To make a custom procedural skybox:
  * Make a new Material, and assign it the **Skybox > Procedural** shader
  * Set the new Material in **Lighting > Environment > Skybox Material**
    * The Lighting tab is found under Window > Rendering > Lighting
* Custom skybox Material settings:
  * **Sun** - None/Simple/High Quality sun orb
  * ** Sun Size** - Slider for how large the sun appears (has no effect on brightness)
  * **Atmosphere Thickness** - Slider for how much light is absorbed by the atmosphere
    * Low settings are all black, high settings are very red
  * **Sky Tint** - Adjusts the colour of the sky
  * **Ground** - Adjusts the colour of the 'ground' (the void below the horizon)
  * **Exposure** - Slider for the sky's exposure
    * Low settings make the sky darker, high settings make it brighter

## Ambient light
Light that doesn't have a specific source
* Configured under **Lighting > Environment > Environment Lighting > Source**
* Can be provided by the skybox, or be a set colour/gradient
* **Skybox** settings
  * **Intensity Multiplier** - Slider controlling the brightness of the ambient light
* **Gradient** settings
  * **Sky Colour** - Adjusts the colour given off by the sky
  * **Equator Colour** - Adjusts the colour given off by the equator
  * **Ground Colour** - Adjusts the colour given off by the ground
* **Colour** settings
  * **Ambient Colour** - Adjusts a single ambient colour

## Emissive materials
Materials that give off light
* Create a new material, and set Surface Options > Workflow Mode to **Specular**
* Under Surface Inputs, enable the **Emission** property, and set the relevant colour and intensity

## Baked Lighting
Baking a lightmap such that much of the light and shadow are pre-calculated, as opposed to realtime lighting that requires more resources at runtime to calculate frame-by-frame
* GameObjects must be **Static** to be included in the baked lightmap
  * Non-Static objects cast and receive no shadows in the baked lightmap, for example
* To bake a lightmap:
  * Under **Lighting > Scene**, create a new Lighting Settings Asset
  * At the bottom of the Lighting > Scene menu, click **Generate Lighting**
* The following lightmap settings can be adjusted under **Lighting > Scene > Lightmapping Settings**
  * **Lightmap Resolution** - Improves the resolution of the lightmap, at the cost of baketime
  * These three settings affect the amount of light in the scene:
    * **Albedo Boost** - Slider controlling the amount of light bouncing between surfaces
      * Default of 1 is physically accurate
      * "Increasing this draws the albedo value towards white for indirect light computation"
    * **Max Bounces** - The number of times indirect light will bounce
      * Higher values are very useful for brightening indoor scenes
    * **Indirect Intensity** - Slider controlling the brightness of indirect light
      * Higher values are very useful for brightening indoor scenes
  * **Ambient Occlusion** - Enabling this simulates the effect of nearby objects blocking indirect light, to enhance realism
    * **Ambient Occlusion - Max Distance** - The maximum range at which ambient occlusion is applied

## [Light Probes](https://learn.unity.com/pathway/creative-core/unit/lighting/tutorial/670fe7e6edbc2a008aa0a838?version=6)
Light from a baked source doesn't interact correctly with dynamic objects in the scene; **Light Probes** store data about light within empty spaces, to alleviate this issue
* Can be relatively efficient at runtime compared to real-time lights
* Arrange them in a 3D 'volume' within the area where dynamic objects will be moving

## [Reflection Probes](https://learn.unity.com/pathway/creative-core/unit/lighting/tutorial/670fea75edbc2a005b5b672d?version=6)
If reflective materials aren't reflecting properly (e.g. reflecting the skybox rather than the surroundings), then set Reflection Probes to perform **Reflection Mapping**
* Add a Reflection Probe to the scene and place it next to the reflective object, such that the object is within the probe's zone of effect
* Set the probe's Type to **Baked**, and under Runtime Settings, enable **Box Projection**
* Adjust the probe's Box Size to include the relevant parts of the surroundings, then **Bake** the probe
  * This is a separate bake from the lightmap, unless auto-baking is enabled

## [Lightmap UVs](https://learn.unity.com/pathway/creative-core/unit/lighting/tutorial/670fe92cedbc2a008abe691a?version=6)
If a model is interacting weirdly with attempts to bake its lightmap, it may need to have its Lightmap UVs regenerated
* Under Project, select the model, and tick **Model > Geometry > Generate Lightmap UVs**
* Note that while this can be a quick fix, having the texture fixed by the artist is preferable

## Miscellaneous notes on Light

### Identify light sources
The **Light Explorer** tab, found under Window > Rendering > Light Explorer, allows identification and adjustment of all light sources in the scene

### [Colour space](https://docs.unity3d.com/Manual/color-spaces-landing.html)
If colours appear to be rendering weirdly, check the colour space setting under **Edit > Project Settings > Player > Other settings > Rendering > Colour Space**
* **Linear** is the default for the URP Template
* **Gamma** is the default for the 3D Template

# Settings affecting shadow
## [Rendering Pipeline Asset](https://learn.unity.com/pathway/creative-core/unit/lighting/tutorial/670fed07edbc2a009a507fa9?version=6)
Within the project's rendering pipeline asset, there is a **Shadows** section
* **Max Distance** - The maximum distance from the Camera at which shadows will be rendered
* **Depth Bias** - Slider controlling the distance shadows are pushed away from the light
  * Can address problems where some pixels on objects that should be lit are instead shadowed
* **Normal Bias** - Slider controlling the distance "at which the shadow casting surfaces will be shrunk along the surface normal"
  * Can address problems where some pixels on objects that should be lit are instead shadowed
* **Soft Shadows** - Enabling this makes shadows look smoother, but requires extra processing
* **Cascades Count** - A series of sliders that control the [shadow cascades](https://docs.unity3d.com/Manual/shadow-cascades.html) in the project
  * More cascades makes shadows sharper near the camera
  * As with Soft Shadows, this requires more resources to render

## Other shadow settings
* Under a GameObject's Mesh Renderer > Lighting, the **Cast Shadows** dropdown can be adjusted
  * Setting this to **Two Sided** means shadows can be cast from either side of the meshes; without this, one-sided shapes like planes won't cast shadows correctly
* To bake light correctly with window glass, set the glass's Cast Shadows to Off before baking, then turn it back On after baking
* If 'light leaks' are allowing light to pass through objects and affect their shadows, try adjusting the Directional Light
  * Under Shadows > Realtime Shadows, adjust the **Bias > Depth**, **Bias > Normal**, and **Near Plane** sliders (lowering them seems to help, but unsure if this has unforeseen consequences)
  * If this is a problem in the whole project, not just one scene, adjust it in the rendering pipeline asset instead (see above)