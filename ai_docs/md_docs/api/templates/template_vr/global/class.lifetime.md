# Lifetime Component

**Inherits from:** ComponentBase


Lifetime is a component that automatically deletes its node after a specified duration. It starts a timer on initialization and removes the node when the lifetime expires.


Useful for temporary objects such as projectiles, particle effects, decals, or any spawned entity that should exist for a limited time.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| lifetime | *Float* | Time in seconds before the node is deleted. Default: 1.0. |
