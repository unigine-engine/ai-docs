# ObjectOutliner Class


ObjectOutliner is a singleton utility class that manages outline rendering for objects in VR. It provides visual feedback by rendering colored outlines around objects when the player looks at or interacts with them.


The class supports outline redirection, allowing an outline to be displayed on a different node than the one being interacted with.


### See Also


- **[SocketOutliner](../../../../../api/modules/vr/components/objects/class.socketoutliner.md)**
- **[VRInteractable](../../../../../api/modules/vr/components/class.vrinteractable.md)**


## ObjectOutliner Class

---

## static get ( )

Returns the singleton instance of ObjectOutliner.
### Return value

Singleton instance.
## void renderOutlineForObject ( )

Renders an outline for the specified node during the current frame.
### Arguments

## void init ( )

Initializes the outliner system.
## void shutdown ( )

Shuts down the outliner system and releases resources.
## void redirectOutlineForNode ( )

Redirects outline rendering from one node to another.
### Arguments

## void clearRedirect ( )

Clears all outline redirections.
## void resetObjects ( )

Resets the list of objects to be outlined.
