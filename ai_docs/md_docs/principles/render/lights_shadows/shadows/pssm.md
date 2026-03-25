# Parallel-Split Shadow Mapping


The Parallel-Split Shadow Mapping (PSSM) is an advanced shadow mapping technique, alleviating the some of the problems produced by the standard shadow map.


The idea of PSSM consists in splitting the view frustum into depth layers parallel to the view plane and rendering independent shadow maps for the split parts. Depending on the distance from the viewer, the points being mapped need different sampling frequency. It is hard to provide the sufficient sampling density in the whole range due to the complexity of the scene geometry. However, the splitting of the view frustum into smaller parts with different depth ranges optimizes the distribution of texture pixels and provides the increased sampling rates.


## PSSM creation


There are 4 basic steps in creating the parallel-split shadow map.


### Step 1. Splitting the view frustum into several depth parts.


The positions splitting the view frustum into parallel parts along the z axis are adjusted according to the chosen split algorithm and practical requirements of the application. The shadow map with higher resolution will be used for the part nearest to the viewer, and the ones with the lower resolutions for the parts further distanced.


![PSSMs distribution](pssm_distr.jpg)


Depending on the chosen parameters the distribution of the split parts can be small, when they are compact and densely positioned, and large, with split parts bigger and more stretched.


### Step 2. Splitting the light's frustum.


As in standard shadow mapping, it is necessary to know the light's view to calculate projection matrices when generating the shadow map. The light's frustum is split into several parts covering the corresponding view frustum split parts. It also includes the objects potentially casting shadows onto the part though being outside of it.


![PSSM range](pssm_range.gif)


The range scale specifies the exact extension of the light's frustum split parts. For example, choosing the larger scale allows the high objects (like trees or houses) to cast shadow onto the scene even if they are not directly included in it.


### Step 3. Rendering PSSMs.


Each shadow map is sequentially rendered with appropriate resolution and parameters for each split part.


### Step 4. Synthesizing Shadows.


With the PSSMs generated, the shadow effects can be synthesized for the whole scene. The algorithm is the same as used in standard shadow mapping. The only difference is selecting the correct shadow map from PSSMs when determining if a pixel is shadowed.


## Advantages and Disadvantages


Compared to the standard shadow mapping technique the parallel-split shadow mapping has the following advantages, which are important for large-scale virtual environments:


- Significant reducing of the aliasing errors due to increased sampling frequency in texture space.
- Successful handling of the dueling frusta case, when the light and view directions are nearly opposite.
- Fully exploiting available shadow map resolution while implementing better dynamic shadowing effects.
- Split scheme that does not require expensive scene analysis.


There also appear some difficulties by practical implementation of the PSSM:


- Multiple rendering passes are required for generating shadow maps and synthesizing shadows, trading performance cost for quality: in typical cases the number of polygons rendered using PSSM technique is much bigger compared to a standard shadow map.
- Storage strategy should be carefully chosen, otherwise, it can place considerable demand on the available interpolators.
- The splitting planes in PSSM introduce discontinuities that can interfere with texture filtering.


> **Notice:** Taking into account all the advantages and disadvantages of this technique, it is recommended to use PSSM only with global light sources that illuminate all the scene.
