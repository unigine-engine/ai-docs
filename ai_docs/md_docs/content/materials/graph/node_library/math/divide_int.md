# Divide Int Node


![](../img/divide_int.png)

### Description

Outputs the integer part of the division result of the two input values A and B. The operation for vector data types is done per-component.


If A and B have a different number of components, a cast is performed to match the one with the greater number of components.


Division operation is not commutative so the order of values is important.


Dividing by zero will result in infinity which often translates to unintended results.
