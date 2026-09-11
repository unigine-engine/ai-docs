# Events (CPP)


An **Event** lets a sequence call your game code at a chosen moment on the timeline. For example, at the frame an explosion goes off in a cutscene, the sequence fires an event and your code spawns the debris particles in response. The sequence sends a named signal at the point you place it, and your game code listens for that name and decides what happens - the sequence owns the timing, the code owns the action.


![](events.png)


An event has no effect in the scene on its own - it only fires the signal at the right frame. Something happens only when game code reacts to it.


There are two event channels: **Event** for a single instant, and **Event Range** for a span of time.


## Event


An **Event** channel fires a signal at a single moment. When the playhead reaches a key, the signal fires.


To author one, set the channel's **Custom Name** in its properties - on an event channel that field is the name your code listens for, and it is also the row's label. Then add a key at each moment the signal should fire. Each key carries an **Event Value** - an integer sent along with the signal, so code can tell apart events that share one channel name.


![](single_event.png)

*An Event channel namedMyCustomEvent, the name game code listens for. It fires twice: value20at frame 50, then value50at frame 200*


## Event Range


An **Event Range** channel models a *state* rather than an instant. Each interval has a start and an end: the signal fires **Begin** when the playhead enters the interval and **End** when it leaves - so one interval sends two signals of the same name, one at each edge. This is for something that stays active for a while, rather than happening at one frame.


![](event_range.png)

*An Event Range channel namedMyCustomEventRange. Its one interval runs from frame 50 to frame 200, sending Begin at the near edge and End at the far one*


You author it the same way - set the channel's **Custom Name** first - but place intervals instead of points: double-click empty track space to create a block, then drag its edges to the span you want. Each interval is a block on the timeline with its own span, its own mute toggle, and its own **Event Value**. Overlaps are allowed, and each interval fires its own Begin and End independently.


![](event_range_value.png)

*The interval's own properties.StartandDurationset the span, andEvent Valueis sent with both its Begin and its End*


## Reacting to Events from Code


An event does nothing until game code handles it. You add one callback to the [player](../../../../../editor2/tools/sequencer/runtime/index_cpp.md) running the file, and it receives *every* event that player fires - the callback is not tied to a single name. Each call gives you three values:


- **name** - the event name, used to filter which event this is.
- **payload** - the **Event Value** set on the key or interval in the sequencer.
- **phase** - whether this is a point event (POINT), the start of an interval (BEGIN), or its end (END).


Because one callback catches everything, you dispatch on the **name** yourself - check which event came in and act on it. This is by design: an artist can add a new event channel to the sequence without you having to change how you subscribe.


The examples below react to a footstep event and ignore the rest.


```cpp
// C++ component attached to the NodeSequencePlayer node in the scene.
#include <UnigineComponentSystem.h>
#include <UnigineAnimation.h>
#include <UnigineNodes.h>

using namespace Unigine;

class EventLogger : public ComponentBase
{
public:
    COMPONENT_DEFINE(EventLogger, ComponentBase);
    COMPONENT_INIT(init);

private:
    // Holds the subscription and drops it when the component is destroyed.
    EventConnections connections;

    void init()
    {
        // The NodeSequencePlayer node wraps the actual player - subscribe on that.
        NodeSequencePlayerPtr player_node = checked_ptr_cast<NodeSequencePlayer>(node);
        player_node->getPlayer()->getEventTriggered().connect(
            connections, this, &EventLogger::on_event);
    }

    // Called once for every event this player fires - filter by name here.
    void on_event(const char *name, int payload, int phase, const char *placement)
    {
        if (strcmp(name, "footstep") == 0)
            Log::message("Footstep! payload %d\n", payload);
    }
};

REGISTER_COMPONENT(EventLogger);

```


## When Events Fire


- An event fires **after** the frame has been applied, so the scene already holds the values of that moment when your code runs.
- Scrubbing the playhead and setting the time from code do **not** fire anything. They only move the anchor.
- A loop wrap is handled at the seam, so each cycle sends every event exactly once.
- A muted channel and a muted interval are silent, and so is a channel inside a muted folder.
- Stopping the player fires **End** for every interval still active, so a subscriber always gets its Begin and End in pairs.
- Two players running the same `*.seq` fire independently, each from its own playhead.


> **Notice:** Do not destroy the player from inside its own event callback. It is still walking its own state at that point.


## Reading State After a Seek


Since a seek fires nothing, code that tracks an interval state has to read it back rather than wait for a signal. The player answers with **queryActiveEventIntervals**, which takes a time, fills an internal list with every interval covering it, and returns how many there are. Each one is then read by index: its name, its **Event Value**, and its start and end.


The query walks the sequence the same way the firing does, so a state read back this way can never disagree with the signals you were sent.


## See Also


- [Runtime Playback](../../../../../editor2/tools/sequencer/runtime/index_cpp.md)
- [Clips](../../../../../editor2/tools/sequencer/clips/index.md)
