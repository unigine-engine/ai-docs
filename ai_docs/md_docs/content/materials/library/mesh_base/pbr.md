# Physically Based Materials


PBR (Physically Based Rendering) material is a surface material which simulates more realistic reflections and a lighting model. Beyond that, it is easier to create content, because it has few settings that greatly facilitates artists' work.


To understand how the physically based material (*PBM*) works and why it is better than the *[mesh_base](../../../../content/materials/library/mesh_base/index.md)* material you should figure out physical properties of materials in real life. The essential thing of *PBM* is that all materials are divided into two main groups: metals and dielectrics (nonconductors).


## What We See


### Diffuse


**Diffuse** reflection (also known as **diffuse light**) is an effect of reflection of light from a surface in all directions at many different angles.


![](385273376_cdcade755e_z.jpg)

*Apple one (flickr.com) /CC BY-SA 2.0*


All [dielectrics](#dielectrics) have this effect.


### Reflection


**Reflection** (also known as **specular light**) is an effect of light reflection, when the light is reflected on the opposite side with the same angle at which it has fallen on a surface.


Both [metals](#metals) and [dielectrics](#dielectrics) have that effect.


![](green_christmas_balls_sm.jpg)

*Green Christmas Balls(christmasstockimages.com) /CC BY 3.0*


Ambient reflection is simulated by using cubemaps while light source reflection is calculated by using **BRDF** formula that describes the behavior of the glint on the surface. Before the *BRDF*, the Blinn-Phong was used which is a simplified version of *BRDF*. Now the more physically correct *BRDF* that is used is called **GGX**.


### Dielectrics


**Dielectrics** (also known as **insulators**) are materials with diffuse scattering and reflection with low intensity. Reflections on dielectrics are colored the same color as the ambient. Dielectrics include fabric, plastic, wood, paint and so on.


For example, due to diffuse scattering, we see the color of plastic surfaces. And due to reflection, we see glares on these surfaces.


![](background-71698_640.jpg)

*Background Play Balls(pixabay.com) /CC0 Public Domain*


### Metals


**Metals** are materials without diffuse scattering, but with an intensive [reflection](#reflection). The diffuse scattering of metals is close to 0, which is black. We see metals only due to reflected light which is colored the surface color.


For example, gold has black diffusion and intensive reflection of yellow color, copper has intensive reflection of red color, silver has intensive reflection of white color.


![](1024px-BB_copper_and_nickel_plated.jpg)

*Steel BBs coated with copper and zinc(en.wikipedia.org) /CC BY-SA 3.0*


### Fresnel Effect


Another important concept is the **Fresnel effect**. The less the angle of light incidence on the surface, the stronger the intensity of the reflection of this light would be.


![](fresnel_chart.png)


At the angle of 90 degrees (perpendicularly to a surface), different materials reflect with different light intensity. Dielectrics reflect from 0.05 to 30 percent of the light, while metals reflect from 55 up to 95 percent.


At the angle of 0 degrees, all materials are capable of reflecting 100 percent of the light.


### Albedo


Albedo consists of the diffuse and reflected light. In other words, albedo defines the color of the surface. We see red plastic as red, gold we see as yellow, blue paint we see as blue, steel we see as gray.


![](albedo.jpg)

*MPC Vought F7U-3 Cutlass Jet Aircraft(flickr.com) /CC BY 2.0*


*Thunderbolt (Vajra; Tibetan: Dorje). Gilt copper alloy(flickr.com)/ Public domain*


*Painting blue(flickr.com) /CC BY 2.0*


*Silver & stainless steel(flickr.com) /CC BY-SA 2.0*


### Roughness


If we look at most materials under the microscope, we will see that their surfaces consist of a large amount of small particles which affect the light reflection from the surface. In other words, the surface is rough.


![](Filter_paper_roughness.jpg)

*A scan of filter paper magnified 840 times under a scanning electron microscope(commons.wikimedia.org) /CC BY 2.0*


Because of the roughness of the surface, light rays bounce in different directions, and the rougher the surface, the bigger the deflection amplitude of the light rays is. Consequently, the bigger the deflection amplitude, the more �blurry� the image is.


### Energy Conservation


Physically correct render also considers the energy conservation. That means both diffuse and reflection light intensity should not be greater than the intensity of the light that drops on the surface. Thus, the more the reflection intensity, the less the diffuse light intensity (diffuse light is becoming darker). Only dielectrics have this effect, because metals have black diffuse reflection.


![](energy_conservation.png)


### Microfiber


Another important parameter of UNIGINE *PBR* material is microfiber, that simulates the napped surface.


![](8123597848_4c1cdf8aa8_z.jpg)

*Yellow Microfiber Sponge(flickr.com) /CC0 1.0*


That nap (pile) is made of a large amount of strands with small length. If we create a napped surface (fur, fluffy material) as a geometry, it will be impossible to handle that surface in real time. Microfiber parameter of the *PBR* material simulates the light reflection on the napped surface. The point is the engine creates shading between strands of fur. But when the light is perpendicular to the microfiber surface, the surface become brighter. Because of this effect, a velvet sphere surface will be highlighted along borders.


![](11676379593_cfc49eb449_z.jpg)

*Green Velvet(flickr.com) /CC BY 2.0*
