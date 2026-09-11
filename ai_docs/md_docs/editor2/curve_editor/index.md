# Editing Curves


Some parameters have non-linear dependence. For example, some parameters of the Particle System (position, direction, angle, radius, color, etc.) may require to be changed over time to create a more natural behavior. Color correction requires input colors to be mapped to output values arbitrarily. To make such changes possible, the values for these parameters are set as curves.


**Curve Editor** allows adjusting these curves.


![](particles_curves_color_optimized.gif)


To configure a parameter as a curve, select either of the following:


![](parameter_selection.png)


| **Curve** | The parameter value changes over input value (e.g. time) based on the curve defined in Curve Editor. ![](curve.png) |
|---|---|
| **Between Curve** | There are two curves that define the limits, and a random value is taken at every moment of time within these limits. The parameter value changes over time based on this randomly generated set of values. ![](between_curve.png) |


In case of a color setting, there is a dropdown menu with a selection between a color and a curve.


To open Curve Editor, click on the curve preview widget.


![](widget.png)


A separate *Curve Editor* window opens for each parameter. The previously opened windows are not closed.


## Navigating in Curve Editor


The horizontal axis represents the input value, such as life time. The values are normalized and depend on the corresponding value of the node (for example [Life Time](../../objects/effects/particles/index.md#life_time)).


The vertical axis represents the range of available parameter values. The scale is controlled by **Max Value**.


![](max_value.png)


The curve view can be **zoomed in** and **out** along both axes by using the scroll wheel, or along either axis individually by using the corresponding display parameter.


![](zoom.png)


The curve view can be **panned** by dragging mouse while holding the middle button pressed or holding the *Ctrl* button and using the cursor keys.


If a parameter is adjusted via multiple curves, you can **hide** some of them via the corresponding checkboxes with color coding.


![](curve_visible.png)


## Adding and Editing Keys


Curves are edited via keys (points on the curve) by changing their position and manipulating their tangents.


To **add** a key, right-click on the curve at the point where the key should be placed and select *Add key*.


**Removing** a key can be performed by right-clicking on it and selecting *Remove key*.


The key **position** can be **changed**:


- by dragging the key around with the mouse
- by changing the values in the Key Parameters section on the right


**Multiple keys** can be **selected** by either of the following ways:


- Press down *Ctrl* and click the required keys.
- Click on an empty spot and drag to make the rectangular selection.


These two ways can be combined: for example, select keys using a rectangle, then press down *Ctrl* and click on the keys you want to add.


Unselecting keys from a rectangle is also done by clicking on them with the *Ctrl* key hold down.


To move all selected keys, press down the left mouse button on one of the keys and drag them around.


**Focusing** on selected keys is done by pressing F on the keyboard.


![Focusing on the selected keys](focus.gif)


To deselect all keys, just click anywhere.


## Editing Tangents


Each key has two tangents to control the curve shape to the left and to the right of the key.


![](tangents.png)


To edit a tangent, select a key, then select a tangent and drag it around.


When multiple keys are selected, you can also modify every single tangents.


## Curve Parameters


![](curves.gif)


To **select the whole curve**, click on it anywhere between the first and the last key.


When selected, the whole curve can be moved around.


To **deselect a curve**, click anywhere except for this curve and its keys.


For the curve, the following parameters are available:


- **Pre Infinity** � the behaviour of the curve prior to the first (leftmost) key.
- **Post Infinity** � the behaviour of the curve after the first (rightmost) key.


These parameters can be used to create loops, i.e. repeat the effect that you created before and after the explicit range defined by the keys.


For these parameters, the following options can be applied:


| **Clamp** | The value of the start or the end key is retained. Use this option if you don't want any changes before or after the effect created by the curve. ![](clamp.png) |
|---|---|
| **Loop** | The curve is tiled. The created effect is repeated. If the values of the first and the last key are different, the transition between the curves is abrupt. ![](loop.png) |
| **PingPong** | Every next curve section is a reflection of the previous curve section. The created effect is repeated in the forward-and-backward manner. ![](pingpong.png) |


The number of curves varies depending on the type of the controlled parameter: for example, angle has a single component (angle value), while direction has three (X, Y, and Z axes), a color may have up to four components (RGBA channels).


### Copying Curve Parameters


*Copy* and *Paste* operations are available when clicking the right-mouse button in the curve field.


![Copying and pasting the curve parameters](curve_copy_paste.gif)


Copying a curve containing n values to the one having more values will replace only the first n ones.
