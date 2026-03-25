# Adding New Controller Interactions


UNIGINE VR System uses a list of OpenXR extensions to support various VR controllers. This list is defined in an auto-generated XML file located at:


**SDK Path:** *<SDK_INSTALLATION>/data/core/openxr/controller_interactions.xml*


This file typically looks like the following:


```xml
<controller_interactions>
<extension name="XR_VARJO_xr4_controller_interaction" />
<extension name="XR_FB_touch_controller_pro" promotedto="1.1" />
</controller_interactions>

```


This `XML` is automatically generated based on the official OpenXR Specification, ensuring it always reflects the most current set of supported controller interaction extensions.


Sometimes, new controller interaction extensions become available before they appear in the engine's SDK. In such cases, you're not stuck waiting for the next update and can define your own set of controller extensions.


To do this, create a custom `XML` file with the same structure and name (`openxr_controller_interactions.xml`) and place it in your project's *configs* folder:


```xml
<controller_interactions>
<extension name="XR_VENDOR_custom_controller_interaction" />
</controller_interactions>

```


The engine will automatically detect and merge these user-defined extensions with the default list from the SDK.
