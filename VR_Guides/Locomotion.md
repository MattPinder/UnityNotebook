# Setting up locomotion in VR
This assumes that you already have an XR Rig set up as described in Unity's VR tutorials.  
**Note:** Changes have been made to the required components, presumably in the transition to Unity 6. Old instructions are struck through but kept in this document for reference.

## Locomotion
~Add a **Locomotion System** component to the XR Rig object in the hierarchy, and drag the XR Rig object into the Locomotion system's **XR Origin** box~  
Add a **Locomotion Mediator** component to the XR Rig object in the hierarchy; this will also add an **XR Body Transformer** component automatically

## Snap Turning
~Add a **Snap Turn Provider (Action-based)** component to the XR Rig, then drag the XR Rig’s Locomotion System component into the Snap Turn Provider’s **System** box~  
Add a **Snap Turn Provider** component to the XR Rig, drag the XR Rig’s Locomotion **Mediator** component into the Snap Turn Provider’s Mediator box, then set the Left- and Right Hand Turn Inputs to **XRI LeftHand Locomotion/Snap Turn** and **XRI RightHand Locomotion/Snap Turn**, respectively

## Teleportation
~Add a **Teleportation Provider** component to the XR Rig, then drag the XR Rig’s Locomotion System component into the Teleportation Provider’s **System** box~
Add a **Teleportation Provider** component to the XR Rig, then drag the XR Rig’s Locomotion Mediator component into the Teleportation Provider’s **Mediator** box
