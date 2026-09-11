# Unigine::Plugins::IG::ComponentBaseInterface Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


All components that are required to work in IG should be inherited from this class. Its methods [saveState()](#saveState_const_BlobPtr_ref_void) and [restoreState()](#restoreState_const_BlobPtr_ref_void) are used only for ExtraSlaves that are connected not from the very beginning and have to start somewhere in the middle of simulation. These methods should be overriden for synchronization between the Syncker channels.


### Usage Example


The *WaterDropAircraftController* component described [here](../../../../../ig/custom_component.md) illustrates the use of [saveState()](#saveState_const_BlobPtr_ref_void) and [restoreState()](#restoreState_const_BlobPtr_ref_void): if Master has already discharged a certain portion of water and then a Slave is connected, the Slave won't discharge the total volume again � Master saves the current payload and sends it to the Slave, and the Slave discharges only the remaining volume of water.


```cpp
// WaterDropAircraftController.cpp

/.../

void WaterDropAircraftController::saveState(const BlobPtr &blob)
{
	// master logic
	// when new slave is connected
	blob->writeBool(open > 0);
	blob->writeFloat(normalize_flow);
	blob->writeFloat(current_payload);
}

void WaterDropAircraftController::restoreState(const BlobPtr &blob)
{
	// slave logic
	// new slave received these parameters
	open = blob->readBool();
	normalize_flow = blob->readFloat();
	current_payload = blob->readFloat();
}

```


The complete *WaterDropAircraftController* component code is provided [here](../../../../../ig/custom_component.md).


## ComponentBaseInterface Class

### Members

---

## void saveState ( const Blob Ptr & blob )


Saves the state of the component. Is used in code writing the component data to be synchronized to a blob on the Master. This method is used for synchronization of ExtraSlaves that are connected after the simulation has started and is triggered once at the Slave connection. Here's an example from the *[WaterDropAircraftController](../../../../../ig/custom_component.md)* component:


```cpp
void WaterDropAircraftController::saveState(const BlobPtr &blob)
{
	// master logic
	// when new slave is connected
	blob->writeBool(open > 0);
	blob->writeFloat(normalize_flow);
	blob->writeFloat(current_payload);
}

```


### Arguments

- *const [Blob](../../../../../api/library/common/class.blob_cpp.md)Ptr &* **blob** - Target Blob to which the current component data (its internal state, any parameters, commands, etc.) is to be saved.

## void restoreState ( const Blob Ptr & blob )

Restores the state of the component. Is used in code reading the data from the blob on Slaves. This method is used for synchronization of ExtraSlaves that are connected after the simulation has started and is triggered once at the Slave connection. Here's an example from the *[WaterDropAircraftController](../../../../../ig/custom_component.md)* component:


```cpp
void WaterDropAircraftController::restoreState(const BlobPtr &blob)
{
	// slave logic
	// new slave received these parameters
	open = blob->readBool();
	normalize_flow = blob->readFloat();
	current_payload = blob->readFloat();
}

```


### Arguments

- *const [Blob](../../../../../api/library/common/class.blob_cpp.md)Ptr &* **blob** - Source Blob from which the current component data (its internal state, any parameters, commands, etc.) is to be loaded.
