# FMod Node


![](../img/fmod.png)

### Description

Outputs the floating point remainder of the division of the two input values A and B. The operation for vector data types is done per-component.


If A and B have a different number of components, a cast is performed to match the one with the greater number of components.


Division operation is not commutative so the order of values is important.


Beware that division by 0 occurs if the B value is zero and its result is defined by implementation.
