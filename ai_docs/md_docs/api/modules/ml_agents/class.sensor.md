# MLAgents::Sensor Class

**Inherits from:** ComponentBase


Sensor is the base class for the components that contribute observation blocks of their own, separately from what the agent writes in its **[observe()](../../../api/modules/ml_agents/class.agent.md)** method.


A sensor is picked up automatically when it sits on the agent node or below it, so a sensor is added to an agent by adding the component to a child node - no code on the agent side. Sensors are laid out in the observation vector by *Order* first and node name second, which keeps the layout stable no matter what order the engine happens to initialize the nodes in.


The demo ships two ready sensors, **[RaySensor](../../../api/modules/ml_agents/class.raysensor.md)** and **[CameraSensor](../../../api/modules/ml_agents/class.camerasensor.md)**. Inherit from Sensor to add one of your own.


```cpp
#include <ml_agents/Sensor.h>

class SpeedSensor: public MLAgents::Sensor
{
public:
    COMPONENT_DEFINE(SpeedSensor, MLAgents::Sensor);
    COMPONENT_INIT(init, MLAgents::InitOrder::SENSOR);

    int getObservationSize() const override { return 1; }

    void write(MLAgents::ObservationWriter &obs) override
    {
        obs.write(current_speed);
    }

private:
    void init() {}
    float current_speed = 0.0f;
};

```


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Sensor Name | *String* |  | Name of the observation block in the specification sent to the trainer. Empty uses the node name |
| Order | *Int* | 0 | Sensors are laid out in the observation vector by (order, node name) |


### See Also


- **[MLAgents::RaySensor](../../../api/modules/ml_agents/class.raysensor.md)**
- **[MLAgents::CameraSensor](../../../api/modules/ml_agents/class.camerasensor.md)**
- **[MLAgents::ObservationWriter](../../../api/modules/ml_agents/class.observationwriter.md)**


## Sensor Class

---

## virtual getObservationSize ( )

Returns how many values the sensor contributes to the observation. It has to be a constant: the observation layout is fixed once, at initialization, and a model accepts only the exact number of values it was trained on.
### Return value

Number of values this sensor writes. Returns 0 unless overridden.
## virtual void getObservationShape ( )

Returns the shape of the observation block. The default is a flat vector of **getObservationSize()** values; override it for a sensor whose data has dimensions of its own, as a camera does.
### Arguments

## virtual getDataType ( )

Returns the data type the sensor writes. A three-dimensional block of UINT8 is what marks an observation as visual, which is what makes the trainer put a convolutional network in front of it.
### Return value

Data type of the block. Returns ObsDataType::FLOAT32 unless overridden.
## virtual void write ( )

Writes the numeric observation of the sensor. Override it for a sensor whose data type is FLOAT32.
### Arguments

## virtual void writeVisual ( )

Writes the raw bytes of a visual observation. Override it instead of **write()** for a sensor whose data type is UINT8.
### Arguments

## virtual void onEpisodeBegin ( )

Clears whatever state the sensor carries between episodes. **[CameraSensor](../../../api/modules/ml_agents/class.camerasensor.md)** drops the flag saying it holds a rendered frame, so the first decision of an episode never observes the last frame of the one before it.
## virtual void onDebugDraw ( )

Draws what the sensor currently sees. Called by the owning agent, so the session overlay switch and the agent's own debug draw flag turn these off along with everything else.
## virtual isOperational ( )

Excludes the sensor from the observation layout when it cannot work at all. **[CameraSensor](../../../api/modules/ml_agents/class.camerasensor.md)** returns false when the engine runs with no renderer to capture from, which is why a camera rules out the headless mode.
### Return value

true if the sensor can work; otherwise, false. Returns true unless overridden.
## virtual void bind ( )

Binds the sensor to the agent that collects it. Called during the agent initialization; override it to react to being attached.
### Arguments

## getSensorName ( )

Returns the *Sensor Name* parameter, or the node name when it is empty.
### Return value

Name of the observation block.
## getOwner ( )

Returns the agent that collects this sensor.
### Return value

Agent this sensor is bound to, or nullptr if it is not bound yet.
