# Fixed-Wing Template - Host Control Mode


The host control mode is available, if the template is launched with a CIGI or DIS connector enabled. In this case the internal template logic is disabled, and the aircraft is created and controlled by the host system.


## Enabling Host Control


To enable the host control mode, use one of the following startup commands depending on the selected protocol:


```text
-extern_plugin UnigineCIGIConnector
-extern_plugin UnigineDISConnector

```


> **Notice:** Although this template supports the aircraft control via a host system, it is recommended to use the [Image Generator template](../../../ig/index.md) for more consistent and reliable operation.
