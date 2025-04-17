# Setting up object interaction haptics/audio in VR
This assumes that you already have an XR Rig set up as described in Unity's VR tutorials.  
**Note:** Changes have been made to the required components, presumably in the transition to Unity 6. Old instructions are struck through but kept in this document for reference.

## Haptics
~Under each controller's **Ray/Direct Interactor** component, expand the **Haptic Events** fold-out, check the relevant boxes to determine *when* there’s feedback, and set the relevant Intensity and Duration~  
1. Add a **Simple Haptic Feedback** and **Haptic Impulse Player** component to each controller
2. In the **Simple Haptic Feedback** component, set the controller itself to both **Interactor Source** and **Haptic Impulse Player**, then check the relevant boxes to determine *when* there’s feedback, and set the relevant **Intensity** and **Duration**
3. In the **Haptic Impulse Player** component, under **Haptic Output**, use the ⠇button to select **Input Action**, use the + button beside it to **Add Binding**, then navigate to **XR Controller > XR Controller (Left/RightHand) > Usages > Haptic**
* Note: The default for Haptic Output is Input Action Reference; if setting the Input System’s Haptic Device here, haptics won’t work and the console will log multiple errors

## Audio
~Under each controller's **Ray/Direct Interactor** component, expand the **Audio Events** fold-out, check the relevant boxes to determine *when* there’s feedback, and set the relevant audio clip~  
Add a **Simple Audio Feedback** component to each controller, check the relevant boxes to determine *when* there’s feedback, and set the relevant audio clip
* Audio Source can apparently be left blank
