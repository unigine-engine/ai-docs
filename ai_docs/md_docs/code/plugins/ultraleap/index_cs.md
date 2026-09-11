# Tracking Hands and Fingers With Ultraleap Plugin (CS)


## Overview


**Ultraleap** plugin allows you to track hands and fingers in your UNIGINE-based application.


> **Notice:** The plugin is available only on *Windows*.


The *Ultraleap* system recognizes and tracks hands and fingers. The device operates in an intimate proximity with high precision and tracking frame rate and reports discrete positions and motion.


The *Ultraleap* controller uses optical sensors and infrared light. The sensors are directed along the Y axis � upward when the controller is in its standard operating position � and have a field of view of about 150 degrees. The effective range of the *Ultraleap* Controller extends from approximately 25 to 600 millimeters above the device (1 inch to 2 feet).


![](leap_view.jpg)

*Ultraleapcontroller's view of your hands*


Detection and tracking work best when the controller has a clear, high-contrast view of an object's silhouette. The *Ultraleap* software combines its sensor data with an internal model of the human hand to help cope with challenging tracking conditions.


## Coordinate System


The *Ultraleap* system uses the UNIGINE world space coordinates.


If you willing to use the *Ultraleap* device without the Varjo's HMD, you have to manually provide correct transformation matrix for each device separately:


```csharp
Mat4 camera_imodelview = camera.IModelview;
Mat4 camera_offset = camera.Offset;

Transform = camera_imodelview * camera_offset;

```


> **Notice:** Depending on your application, you might require to manually provide correct HMD Position that was updated during the plugin update **before the plugin swap event** using the [BeginSwap](../../../api/library/engine/class.engine_cs.md#getEventBeginSwap_Event) event (native VR plugins already do this internally).


## Hands


The **hand** model provides information about the identity, position, and other characteristics of a detected hand, the arm to which the hand is attached, and lists of the fingers associated with the hand.


Hands are represented by the *[Hand](../../../api/library/plugins/ultraleap/class.ultraleaphand_cs.md)* class.


![](palm_vectors.png)

*Handnormalanddirectionvectors define the orientation of the hand*


> **Notice:** More than two hands can appear in the hand list for a frame if more than one person's hands or other hand-like objects are in view. However, it is recommended to keep at most two hands in the *Ultraleap* Controller's field of view for optimal motion tracking quality.


## Arms


An **arm** is a bone-like object that provides the orientation, length, width, and end points of an arm. When the elbow is not in view, the *Ultraleap* controller estimates its position based on past observations as well as typical human proportion.


Arms are represented by the *[Arm](../../../api/library/plugins/ultraleap/class.ultraleaparm_cs.md)* class.


## Fingers


The *Ultraleap* controller provides information about each **finger** on a hand. If the whole or part of a finger is not visible, the finger characteristics are estimated based on recent observations and the anatomical model of the hand. Fingers are identified by type name, i.e. *thumb, index, middle, ring, pinky*.


Fingers are represented by the *[Finger](../../../api/library/plugins/ultraleap/class.ultraleapfinger_cs.md)* class.


![](fingers.png)

*Fingertip positionanddirectionprovide the position of a finger tip and the general direction in which a finger is pointing*


## Bones


Each finger has a set of **bones** describing the position and orientation of corresponding anatomical finger bones. All fingers contain four bones ordered from base to tip.


Bones are represented by the *[Bone](../../../api/library/plugins/ultraleap/class.ultraleapbone_cs.md)* class.


![](bones.png)

*Palm and all its finger bones*


The bones are identified as:


- **Metacarpal** � the bone inside the palm connecting the finger to the wrist (except the thumb).
- **Proximal Phalanx** � the bone at the base of the finger, connected to the palm.
- **Intermediate Phalanx** � the middle bone of the finger, between the tip and the base.
- **Distal Phalanx** � the terminal bone at the end of the finger.


> **Notice:** Such model for the thumb does not quite match the standard anatomical naming system. A real thumb has one less bone than the other fingers. However, for ease of programming, the *Ultraleap* thumb model includes a zero-length metacarpal bone so that the thumb has the same number of bones at the same indexes as the other fingers. As a result the thumb's anatomical metacarpal bone is labeled as a proximal phalanx and the anatomical proximal phalanx is labeled as the intermediate phalanx in the *Ultraleap* finger bone model.


## See Also


**Ultraleap API:**


- The *[Ultraleap](../../../api/library/plugins/ultraleap/class.ultraleap_cs.md)* interface article for more details on managing Ultraleap via API
- The *[Ultraleap](../../../api/library/plugins/ultraleap/class.ultraleapdevice_cs.md)* interface article for more details on managing Ultraleap devices via API
- The *[Ultraleap Arm](../../../api/library/plugins/ultraleap/class.ultraleaparm_cs.md)* class article for more details on managing arms via API
- The *[Ultraleap Bone](../../../api/library/plugins/ultraleap/class.ultraleapbone_cs.md)* class article for more details on managing finger bones via API
- The *[Ultraleap Finger](../../../api/library/plugins/ultraleap/class.ultraleapfinger_cs.md)* class article for more details on managing fingers via API
- The *[Ultraleap Hand](../../../api/library/plugins/ultraleap/class.ultraleaphand_cs.md)* class article for more details on managing hands via API


## Implementing Unigine Application with Ultraleap Support


To use the *Ultraleap* plugin in your UNIGINE application, perform the following:


1. Download the *[Ultraleap SDK](https://www.leapmotion.com/setup/desktop/windows)* and install *Ultraleap* device drivers.
2. To **add the plugin to a new project**, start by [creating a project](../../../sdk/projects/index_cs.md#creation) from a template. In the project creation dialog, open *Advanced Settings > Plugins*, enable the *Ultraleap* plugin, click *Add*, then select *Create New Project*. ![](add_plugin.png) For **existing projects**, in the SDK Browser, open the *My Projects* tab, and click the three-dot menu on the project card. Select *Configure*, then click *Plugins*, enable the required plugin, click *Add*, and finish with *Configure Project*. ![](../../../sdk/projects/other_actions.png)
3. Implement your application.
4. [Launch](#launch) the *Ultraleap* plugin on the application start-up.


## Launching Ultraleap


To launch the plugin, specify the `extern_plugin` command line option on the application start-up as follows:


```bash
main_x64d -extern_plugin UnigineUltraleap

```


If you run the application via UNIGINE SDK Browser, specify the command-line options given above in the *[Customize Run Options](../../../sdk/projects/index_cs.md#customize_run)* form.
