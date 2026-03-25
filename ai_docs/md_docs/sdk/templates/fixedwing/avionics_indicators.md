# Fixed-Wing Template - Flight Instruments Simulation


The template contains a framework for simulating the following flight instruments implemented in components with the matching names:


| Component Name | Visual Representation At Runtime |
|---|---|
| Airspeed | ![](../modules/avionics_indicators/airspeed.png) |
| Altimeter | ![](../modules/avionics_indicators/altimeter.png) |
| Attitude | ![](../modules/avionics_indicators/attitude.png) |
| Variometer | ![](../modules/avionics_indicators/variometer.png) |
| Compass | ![](../modules/avionics_indicators/compass.png) |


These instruments display their corresponding values in real time, updating as the aircraft’s transformations change.


## Configuring Instruments


To visualize dynamic values correctly, the instruments must be configured as follows:


- **In the Editor**: assign the [appropriate property](#component) to the object. [![](../modules/avionics_indicators/editor_prop.jpg)](../modules/avionics_indicators/editor_prop.jpg)
- Configure the property [settings](../../...md) such as textures, size, and other parameters.
- **In the logic**: [changes to the corresponding **in_*** parameters](#logic) (such as `in_speed, in_altitude`) drive the visual updates of the instruments.


## Instrument Component Settings


| Render settings |  |
|---|---|
| Size | Resolution of the texture to be rendered on the instrument surface, in pixels. |
| Surface name | Name of the object surface, onto which the texture is assigned. |
| Texture name | Name of the object texture into which the instrument texture is rendered. |
| Settings (differ depending on the instrument) | Textures of the instrument background, and moving parts (arrows and plates) |
| Runtime parameters | Parameters that read runtime data and change the instrument readings accordingly. |


## Updating Values At Runtime


The runtime parameters exposed by this component can be modified at runtime:


```cpp
using namespace Unigine;

class TestComponent : public ComponentBase
{
public:
    COMPONENT_DEFINE(TestComponent, ComponentBase)
    COMPONENT_UPDATE(update)

    PROP_PARAM(Node, airspeed_node)

private:
    void init()
    {
        airspeed = getComponent<Airspeed>(airspeed_node);
    }

    void update()
    {
        if (!airspeed)
            return;

        auto player = Game::getPlayer();
        if (!player)
            return;

        auto velocity = player->getVelocity();
        airspeed->in_speed = velocity.length();
    }

private:
    Airspeed* airspeed = nullptr;
};

REGISTER_COMPONENT(TestComponent)

```


The whole list of **in_*** parameters is available in *AvionicsIndicatorsController*.


For more details on usage, see the `FlightLogic.cpp` file.
