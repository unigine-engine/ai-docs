# CigiIGUserDefined Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


## CigiIGUserDefined Class

### Members

---

## void setPacketID ( int id )

Sets the ID of the user-defined packet.
### Arguments

- *int* **id** - ID of the user-defined packet.

## void setData ( const unsigned char * data , int size )

Sets the [user-defined data](../../../../../ig/custom_packets.md#custom_cigi).
> **Notice:** Bytes are read and written starting from the 2nd byte (not from the 4th). If you want to align bytes starting from the 4th one, you should add a couple of bytes in the beginning. The CIGI ICD recommends to start reading/writing bytes starting from the 4th one (see Data before the **Data Block 1** shown in the images below), although it is mentioned, that it is possible to start from the 2nd.


![General User-Defined Packet Structure](../../../../../ig/userpacket_cigi.png)


### Arguments

- *const unsigned char ** **data** - User-defined data.
- *int* **size** - Size of the packet.
