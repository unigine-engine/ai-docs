# CigiArticulatedShortControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiArticulatedShortControl Class

### Members

---

## int getEntityID ( ) const

Returns the entity ID specified in the packet.
### Return value

Entity ID.
## int getPartID1 ( ) const

Returns the articulated part 1 ID specified in the packet.
### Return value

Articulated part 1 ID.
## int getPartID2 ( ) const

Returns the articulated part 2 ID specified in the packet.
### Return value

Articulated part 2 ID.
## int getPartEnabled1 ( ) const

Returns the value of the **Articulated Part 1 Enable** parameter specified in the packet.
### Return value

**Articulated Part 1 Enable** parameter value: 1 if the articulated part is enabled; otherwise, 0.
## int getPartEnabled2 ( ) const

Returns the value of the **Articulated Part 2 Enable** parameter specified in the packet.
### Return value

**Articulated Part 2 Enable** parameter value: 1 if the articulated part is enabled; otherwise, 0.
## int getSelect1 ( ) const

Returns the value of the **DOF Select 1** parameter specified in the packet.
### Return value

**DOF Select 1** parameter value.
## int getSelect2 ( ) const

Returns the value of the **DOF Select 2** parameter specified in the packet.
### Return value

**DOF Select 2** parameter value.
## float getDOF1 ( ) const

Returns the value of the **DOF 1** parameter specified in the packet.
### Return value

**DOF 1** parameter value.
## float getDOF2 ( ) const

Returns the value of the **DOF 2** parameter specified in the packet.
### Return value

**DOF 2** parameter value.
