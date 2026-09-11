# FlightModel

**Inherits from:** FlightModelBase


Template class that wraps FlightModelBase with typed Config and Input. Template parameters: C (config type, default FlightModelConfigBase) and I (input type, default FlightModelBasicInput).


### See Also


- **[FlightModelBase](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelbase.md)**
- **[FlightModelConfigBase](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelconfigbase.md)**
- **[FlightModelBasicInput](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelbasicinput.md)**
- **[MultirotorPhysical](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.multirotorphysical.md)**
- **[MultirotorLinear](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.multirotorlinear.md)**
- **[FixedWing](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.fixedwing.md)**


## FlightModel Class

---

## virtual void setUseExternalInput ( )

Sets whether the flight model uses external input.
### Arguments

## virtual isUseExternalInput ( )

Returns whether external input mode is enabled.
## virtual void setInput ( )

Sets the flight control input.
### Arguments

## virtual getInput ( )

Returns the current input.
## getObject ( )

Returns the object associated with this flight model.
## getBodyRigid ( )

Returns the rigid body associated with this flight model.
## virtual getActiveConfig ( )

Returns the active configuration.
## virtual getDefaultConfig ( )

Returns the default configuration.
## virtual getConfig ( )

Returns the configuration at the specified index.
### Arguments
