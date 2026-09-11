# Lamp Component

**Inherits from:** ComponentBase, EventSlot


Lamp is a component that controls a light source based on a received float signal. When a signal with a non-zero value is received, the lamp turns on by modifying the emission parameters of its material. When the signal is zero, the lamp turns off.


The component implements the **[EventSlot](../../../../api/modules/vr/components/class.eventslot.md)** interface to receive float values from an **[EventSignal](../../../../api/modules/vr/components/class.eventsignal.md)** source (e.g., a **[Generator](../../../../api/templates/template_vr/objects/class.generator.md)**).


### See Also


- **[EventSlot](../../../../api/modules/vr/components/class.eventslot.md)**
- **[Generator](../../../../api/templates/template_vr/objects/class.generator.md)**


## Lamp Class

---

## void receiveFloat ( )

Receives a float value and updates the lamp state accordingly.
### Arguments
