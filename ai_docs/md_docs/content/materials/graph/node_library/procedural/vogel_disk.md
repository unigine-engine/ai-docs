# Vogel Disk Node


![](../img/vogel_disk.png)

### Description

Generates a set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside.


- Count - number of points
- Index - index of the current point for the disk with the number of points equal to Count


If you want to get uniform distribution of coordinates for a circle, the Vogel Disk node fits perfectly. For example you can use it in a loop to generate UV coordinates offset for making a uniform circular blur effect. You can pass the current loop iteration index to Index and the maximum number of iterations to Count
