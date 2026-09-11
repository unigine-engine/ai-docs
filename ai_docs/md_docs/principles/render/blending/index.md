# Alpha Blending


**Alpha blending** is a process of combining an image with the background to create an appearance of partial or full transparency.


## Blending Formula


To get the resulting color by alpha blending the following formula is used:

 ColorRes = ColorSrc * Src + ColorDest * Dest
**ColorSrc** corresponds to the polygon color (source image), and **ColorDest** corresponds to screen buffer color (destination image). **ColorRes** is the resulting color.


If a color has the Alpha component that equals to 0, it will be transparent. With the Alpha value of 1, the Red, Green and Blue values are added to create a color. To compute the color in semitransparent areas, linear interpolation is used.


As well as the Alpha component, RGB values are also normalized.


## Values of Src and Dest Multipliers


The multipliers Src and Dest can have the following values:


| Name | Description |
|---|---|
| None | No blending is used |
| Zero | The RGBA components of the corresponding color are multiplied by zero |
| One | The RGBA components of the corresponding color are multiplied by one |
| Src color | The RGBA components of the corresponding color are multiplied by these factors (per component): (**mR, mG, mB, mA**) |
| One minus src color | The RGBA components of the corresponding color Components of each material color are multiplied by these factors (per component): (**1�-�mR, 1�-�mG, 1�-�mB, 1�-�mA**) |
| Src alpha | The RGBA components of the corresponding color are multiplied by **mA** |
| One minus src alpha | The RGBA components of the corresponding color are multiplied by **1�-�mA** |
| Dest color | The RGBA components of the corresponding color are multiplied by these factors (per component): (**bR, bG, bB, bA**) |
| One minus dest color | The RGBA components of the corresponding color are multiplied by these factors (per component): (**1�-�bR, 1�-�bG, 1�-�bB, 1�-�bA**) |
| Dest alpha | The RGBA components of the corresponding color are multiplied by **bA** |
| One minus dest alpha | The RGBA components of the corresponding color are multiplied by **1�-�bA** |


Where mR, mG, mB, mA are normalized material red, green, blue, and alpha values correspondingly;
 bR, bG, bB, bA are normalized background red, green, blue, and alpha values correspondingly.


## Possible Combinations


Depending on the combination of the multipliers *Src* and *Dest*, the following effects are achieved:


### 1


***Src* = None**
 ***Dest* = None**


Means there is no alpha blending for the material. The object is rendered completely opaque.


![](01.jpg)

*No alpha blending. A base for all further blending combinations*


### 2


***Src* = One**
 ***Dest* = One minus Src alpha**


**Result**: Alpha blending


- *Opaque* areas **(alpha�=�1)** receive material color.
- *Transparent* areas **(alpha�=�0)** receive screen buffer color.


The combination is used to create the effect of transparency basing on the alpha component.


![](02.jpg)

*Alpha blended particles*


### 3


***Src* = Src alpha**
 ***Dest* = One minus Src alpha**


**Result**: Standard alpha blending


- *Opaque* areas receive material color, but they are darker and smaller in size, if compared to the [previous](#id_2) variant.
- The areas of alpha gradient fading are darkened.
- *Transparent* areas receive the screen buffer color.


![](03.jpg)

*Standard alpha blending. Notice the dark fringe*


### 4


***Src* = Src color**
 ***Dest* = One minus Src alpha**


**Result**:


- *Opaque* areas are also small and even darker and more contrast, if compared to the [second](#id_2) and [third](#id_3) variants.
- The areas of alpha gradient fading are darkened.
- *Transparent* areas receive the screen buffer color.


![](04.jpg)


### 5


***Src* = Src color**
 ***Dest* = One minus Src color**


**Result**:


- *Opaque* areas are small and of the inverted color.
- The areas of alpha gradient fading are darkened.
- *Transparent* areas receive the screen buffer color.
- Completely **black** diffuse material color will result in rendering in screen buffer color.


![](05.jpg)


### 6


***Src* = Src alpha**
 ***Dest* = One**


**Result**: Alpha-dependent color addition


- In overlapping *opaque* areas, the material color is added to itself. The areas are very small in size.
- *Transparent* areas receive screen buffer color.
- Completely **black** diffuse material color will result in rendering in screen buffer color.


![](06.jpg)


### 7


***Src* = Src color**
 ***Dest* = Dest alpha**


**Result**: almost the same as the [previous](#id_6) variant, but a little less bright and of less distinct material color


![](07.jpg)


### 8


***Src* = One**
 ***Dest* = One**


**Result**: Color addition


- In overlapping *opaque* areas the material color is added to itself.
- The areas of alpha gradient fading are bright and distinct.
- *Transparent* areas receive the screen buffer color.
- Completely **black** diffuse material color will result in rendering in screen buffer color.


This combination can be used to create halation, particles systems, and volume lights. In this blending mode, the darker the color of the object is, the more transparent it is visualized. By overlaying a lot of layers, overlighting occurs.


![](08.jpg)


### 9


***Src* = Zero**
 ***Dest* = Src color**


***Src* = Dest color**
 ***Dest* = Zero**


**Result** (for both variants): Multiplication


- *Opaque* areas receive screen buffer color multiplied by the material color.
- *Transparent* areas are black.


If all the material is semitransparent, this combination can be used to create the colored glass.


![](09.jpg)


### 10


***Src* = One minus Src color**
 ***Dest* = Dest alpha**


**Result**:


- With a non-white color, a completely opaque area seems small and receives the inverted color. In the area of alpha gradient fading, it changes into the summed color. Layers overlapping causes intensification of the color.
- If the diffuse material color is **white**, completely *opaque* core areas receive screen buffer color that changes into the summed color as alpha gradient fades.
- *Transparent* areas are of the screen buffer color.
- Changing the diffuse color multiplier changes the size of the core areas (ring size on the illustration).
- Completely **black** diffuse material color will result in rendering in screen buffer color.


![](10_double.jpg)

*Material diffuse color multipliers:1(on the left) and1.5(on the right)*


![](10_white.jpg)

*If the diffuse material color is white, the opaque core is of the screen buffer color. The diffuse color multiplier equals1.5*


### 11


***Src* = One minus Src color**
 ***Dest* = One minus Src color**


**Result**: similar to the [previous](#id_10) combination, with the following exceptions:


- With a non-white color, a completely opaque area that receives the inverted color seems bigger in size and darker. In the area of alpha gradient fading, the material color appears dull, tint, and barely visible.
- If the diffuse material color is **white**, completely *opaque* core areas receive black color that changes into the summed inverted color as alpha gradient fades.


And the following characteristics remain the same:


- *Transparent* areas are of the screen buffer color.
- Changing the diffuse color multiplier changes the size of core areas (ring size on the illustration).
- Completely **black** diffuse material color will result in rendering in screen buffer color.


![](11_double.jpg)

*Material diffuse color multipliers:1(on the left) and1.5(on the right)*


![](11_white.jpg)

*If the diffuse material color is white, the inverted opaque core is black*


### 12


***Src* = One minus Dest color**
 ***Dest* = Dest Alpha**


**Result**:


- *Opaque* areas are bright and of diffuse material color hue.
- The darker the screen buffer color, the more saturated the material color is.
- *Transparent* areas are of the screen buffer color.
- Completely **black** diffuse material color will result in rendering in screen buffer color.


![](12.jpg)


### 13


***Src* = One minus Dest color**
 ***Dest* = One minus Src alpha**


**Result**:


- In overlapping areas, inversion of the screen buffer color becomes more and more visible with increasing the number of layers.
- *Transparent* areas are of the screen buffer color.


![](13.jpg)


### 14


***Src* = One minus Dest color**
 ***Dest* = One minus Src color**


**Result**:


- In overlapping areas, the color is changed from the inverted to the background color and back again.
- *Transparent* areas are of the screen buffer color.
- Completely **black** diffuse material color will result in rendering in screen buffer color.


![](14.jpg)


### 15


***Src* = Dest color**
 ***Dest* = Dest alpha**


**Result**:


- This combination is more suitable for materials of **white** or bright (of high value) diffuse colors. Otherwise, the material color tint is not visible.
- *Transparent* areas are of the screen buffer color.


![](15.jpg)


### 16


***Src* = Dest color**
 ***Dest* = Dest color**


**Result**:


- *Opaque* areas receive the summed color of material and screen buffer.
- *Transparent* areas are of the multiplied screen color � darker and more saturated.
- In overlapping areas, the material color of both opaque and transparent (according to alpha component) areas is intensified.


![](16.jpg)
