# CigiComponentShortControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiComponentShortControl Class

### Members

---

## int getInstanceID ( ) const

Returns the instance ID specified in the packet.
### Return value

Instance ID.
## int getComponentID ( ) const

Returns the component ID specified in the packet.
### Return value

Component ID.
## int getComponentClass ( ) const

Returns the component class specified in the packet.
### Return value

CIGI component class. One of the [CIGI_COMPONENT_*](../../../../../api/library/plugins/ig/cigi/class.icigicomponentcontrol_cpp.md#CIGI_COMPONENT_ENTITY) values.
## int getComponentState ( ) const

Returns the value of the **Component State** parameter specified in the packet.
### Return value

**Component State** parameter value. One of the [CIGI_STATE_*](../../../../../api/library/plugins/ig/cigi/class.cigi_connector_cpp.md#CIGI_STATE_DISABLED) values.
## unsigned int getData1 ( ) const

Returns the value of the **Data 1** parameter specified in the packet.
### Return value

**Data 1** parameter value.
## unsigned int getData2 ( ) const

Returns the value of the **Data 2** parameter specified in the packet.
### Return value

**Data 2** parameter value.
