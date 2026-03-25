# render_composite


A *render_composite* material allows you to apply the following full-screen postprocesses selectively (on per-material basis) rather then to the whole screen using the Auxiliary buffer:

- [DOF](../../../../editor2/settings/render_settings/camera_effects/index.md#dof)
- [Motion blur](../../../../editor2/settings/render_settings/camera_effects/index.md#velocity)


> **Warning:** This article is deprecated and will be updated in further UNIGINE updates.


![Render composite](render_composite.jpg)

*Material excluded from DOF*


### Usage


To apply *render_composite* material, follow these steps:

1. Set it (or a material inherited from it) in *Render settings* -> *[Composite](../../../../editor2/settings/render_settings/custom_composite/index.md#composite_materials)* shader field. ![Composite shader field](composite.png)
2. Make sure that *Main menu* ->*Render* tab -> *Auxiliary buffer* option is checked. ![Auxiliary buffer should be enabled](../postprocess/main_menu.png)
3. Go to the surface material. Set ***States*** tab ->*Passes* -> ***Auxiliary*** pass and set it***Default***. It means that the material is rendered into the auxiliary color buffer. ![Enable Auxiliary pass for the material that should be postprocessed](../postprocess/auxiliary_pass.png)


It is also possible to mask materials for two postprocesses using surface material -> Parameters -> Auxiliary Color (see [blur_mask](#blur_mask) and [dof_mask](#dof_mask) below).


## States


| auxiliary_mode | Specifies if the surface (with Auxiliary pass enabled) should be rendered with the additional color multiplier: - **Skip** - additional color is not rendered - **Overlay** - color multiplier is applied ![Overlay mode for Auxiliary buffer](overlay.jpg) *Overlay mode* |
|---|---|
| blur_mask | Mask to exclude objects from Motion blur. - **Skip** - all materials are rendered blurred. - **red** - materials that have Auxiliary Color with **non-zero Red** channel value are excluded from motion blur. - **green** - materials that have Auxiliary Color with **non-zero Green** channel value are excluded from motion blur. ![Overlay mode for Auxiliary buffer](blur_mask.jpg) *Yellow material is excluded from motion blur* |
| dof_mask | Mask to exclude objects from DOF effect. - **Skip** - all materials are rendered with DOF effect applied. - **red** - materials that have Auxiliary Color with **non-zero Red** channel value are rendered without DOF effect (non-blurred). - **green** - materials that have Auxiliary Color with **non-zero Green** channel value are rendered without DOF effect (non-blurred). ![Overlay mode for Auxiliary buffer](dof_mask.jpg) *Green material without DOF effect* |
