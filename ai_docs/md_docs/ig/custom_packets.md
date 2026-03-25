# Processing User-Defined Packets

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


Simulations often require extended communication, which is not covered by standard packets included in a certain communication standard or protocol (DIS, CIGI, etc.). So, custom (user-defined) packets are needed.


Such custom packets make it possible to extend basic functionality and add more flexibility to the system (e.g. when you need to display some avionics data).


UNIGINE IG enables you to define and process custom (user-defined) packets. The workflow is simple and similar for all communication protocols:


- Set a callback on receiving a certain packet. When IG receives a packet from the network, it creates an object of the appropriate class and passes it to the callback function.
- Inside the callback function, read and interpret the data of the class instance passed to it (depending on what was written to the packet on the host).
- Create and send a corresponding response packet, if necessary.


## User-Defined CIGI Packets


Just like with all other types of packets, to receive user-defined ones, we should add a callback for `CIGI_OPCODE >= 201` (in accordance with *[CIGI ICD](http://cigi.sourceforge.net/specification.php)*). On receiving such a packet, the callback shall be executed with *CigiHostUserDefined * packet* passed to it.


The *[CigiHostUserDefined](../api/library/plugins/ig/cigi/class.icigihostuserdefined_cpp.md)* class has the *[getData()](../api/library/plugins/ig/cigi/class.icigihostuserdefined_cpp.md#getData_uchar_ptr)* method, which returns a set of bytes to be read and interpreted by the user (depending on what was written to the packet on the host).


The same situation is with sending packets. First, we ask the *CIGIConnector* to create a packet with a certain *CIGI_OPCODE*. If the code is equal to 201 or greater, a *CigiIGUserDefined* instance shall be returned. You can set bytes to be sent by calling the *[CigiIGUserDefined::setData()](../api/library/plugins/ig/cigi/class.icigiiguserdefined_cpp.md#setData_const_uchar_ptr_int_void)* method.


> **Notice:** Bytes are read and written starting from the 2nd byte (not from the 4th). If you want to align bytes starting from the 4th one, you should add a couple of bytes in the beginning. The CIGI ICD recommends to start reading/writing bytes starting from the 4th one (see Data before the **Data Block 1** shown in the images below), although it is mentioned, that it is possible to start from the 2nd.


![General User-Defined Packet Structure](userpacket_cigi.png)


Below is an example of working with user-defined CIGI packets:


```cpp
using namespace Plugins;

int AppWorldLogic::init()
{
	// ....

	int index = Engine::get()->findPlugin("CIGIConnector");
	// check CIGIConnector plugin load
	if (index != -1)
	{
﻿
		// getting the CIGI interface
		cigi = Unigine::Plugins::IG::CIGI::Connector::get();
               // adding a callback for OPCODE = 202
		cigi->addOnReceivePacketCallback(202, MakeCallback(this, &AppWorldLogic::on_recv_user_packet));
	}
	return 1;
}

// ....

void AppWorldLogic::on_recv_user_packet(Unigine::Plugins::IG::CIGI::CigiHostPacket  * host_packet)
{
	Log::error("AppWorldLogic::on_recv_user_packet\n");
	CigiHostUserDefined * packet = dynamic_cast<CigiHostUserDefined *>(host_packet);

	unsigned char * request_data = packet->getData();  // read
	// ...
        // creating a new IG user packet with opcode 203
	CigiIGPacket * response_packet = cigi->createIGPacket(203);
	CigiIGUserDefined * user_defined = dynamic_cast < CigiIGUserDefined *>(response_packet);

	user_defined->setData(response_data, size_of_data); // write
	cigi->addIGPacket(response_packet);
}

```


## Custom DIS PDUs


In case of using DIS, custom Protocol Data Units (PDUs) are processed the same way as [user-defined CIGI packets](#custom_cigi).


> **Notice:** Basic level of DIS support is implemented using the KDIS library v2.9.0, `DIS_VERSION 7`, so don't forget to download it from [here](https://sourceforge.net/p/kdis/code/ci/2-9-0/tree/) and add an additional include directory in your project to the `KDIS/include/` folder.


Below is an example of working with custom PDUs:


```cpp
#include <PDU/Header.h>
#include <DataTypes/EntityType.h>
#include <PDU/Entity_Info_Interaction/Entity_State_PDU.h>
using namespace Plugins;
// ...

int AppWorldLogic::init()
{
	// ....

	int index = Engine::get()->findPlugin("DISConnector");

	// check DISConnector plugin load
	if (index != -1)
	{
		// getting the DIS interface
		dis = Unigine::Plugins::IG::DIS::Connector::get();
        // adding a callback for all packets

		dis->addReceivePacketCallback(KDIS::DATA_TYPE::ENUMS::Entity_State_PDU_Type, MakeCallback(this, &AppWorldLogic::on_recv_entitystate_packet));
        dis->addReceivePacketCallback(KDIS::DATA_TYPE::ENUMS::Other_PDU_Type, MakeCallback(this, &AppWorldLogic::on_recv_other_packet));

	}
	return 1;
}

// ....

void AppWorldLogic::on_recv_entitystate_packet(KDIS::PDU::Header *pdu)
{
	if (pdu->GetPDUType() == KDIS::DATA_TYPE::ENUMS::Entity_State_PDU_Type)
	{
		KDIS::PDU::Entity_State_PDU *entity_state_pdu = static_cast<KDIS::PDU::Entity_State_PDU *>(pdu);

		auto location = entity_state_pdu->GetEntityLocation();
		auto linear_velocity = entity_state_pdu->GetEntityLinearVelocity();
		auto appearance = entity_state_pdu->GetEntityAppearance();
		// ...
	}

}
void AppWorldLogic::on_recv_other_packet(KDIS::PDU::Header *pdu)
{
    // ...
}

```


> **Notice:** The callbacks receive only packets with the Exercise ID, as well as Site ID, matching on the server and IG. These parameters are set in the [configuration file](../ig/config.md#dis_tags).
