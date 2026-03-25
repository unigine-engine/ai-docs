# Blue Noise TAA Node


![](../img/blue_noise_taa.png)

### Description

This node generates blue noise based on input coords using a 16x16 constant blue noise array. You can specify the number of frames for the noise to change. It is a constant blue noise array with a frame-to-frame offset calculated using Golden Ratio.


The *TAA* postfix means that noise pattern changes from frame to frame when [TAA](../../../../../principles/render/antialiasing/taa.md) is enabled, and remains constant when TAA is disabled.
