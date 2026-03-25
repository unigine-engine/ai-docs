# CigiComponentControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiComponentControl Class

### Enums

## CIGI_COMPONENT

| Name | Description |
|---|---|
| **CIGI_COMPONENT_ENTITY** = 0 | Entity component class. |
| **CIGI_COMPONENT_VIEW** = 1 | View component class. |
| **CIGI_COMPONENT_GROUP** = 2 | View Group component class. |
| **CIGI_COMPONENT_SENSOR** = 3 | Sensor component class. |
| **CIGI_COMPONENT_REG_WATER** = 4 | Regional Water component class. |
| **CIGI_COMPONENT_REG_TERRAIN** = 5 | Regional Terrain component class. |
| **CIGI_COMPONENT_REG_WEATHER** = 6 | Regional Weather component class. |
| **CIGI_COMPONENT_GLOBAL_WATER** = 7 | Global Water component class. |
| **CIGI_COMPONENT_GLOBAL_TERRAIN** = 8 | Global Terrain component class. |
| **CIGI_COMPONENT_GLOBAL_WEATHER** = 9 | Global Weather component class. |
| **CIGI_COMPONENT_ATMOSPHERE** = 10 | Atmosphere component class. |
| **CIGI_COMPONENT_CELESTIAL** = 11 | Celestial component class. |
| **CIGI_COMPONENT_EVENT** = 12 | Event component class. |
| **CIGI_COMPONENT_SYSTEM** = 13 | System component class. |
| **CIGI_COMPONENT_SYMBOL_SURFACE** = 14 | Symbol Surface component class. |
| **CIGI_COMPONENT_SYMBOL** = 15 | Symbol component class. |

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

CIGI component class. One of the [CIGI_COMPONENT_*](#CIGI_COMPONENT_ENTITY) values.
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
## unsigned int getData3 ( ) const

Returns the value of the **Data 3** parameter specified in the packet.
### Return value

**Data 3** parameter value.
## unsigned int getData4 ( ) const

Returns the value of the **Data 4** parameter specified in the packet.
### Return value

**Data 4** parameter value.
## unsigned int getData5 ( ) const

Returns the value of the **Data 5** parameter specified in the packet.
### Return value

**Data 5** parameter value.
## unsigned int getData6 ( ) const

Returns the value of the **Data 6** parameter specified in the packet.
### Return value

**Data 6** parameter value.
