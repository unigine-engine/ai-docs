# Simulation

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Speed Boat

This sample demonstrates how to simulate dynamic wake foam behind a moving boat using a combination of ***[Orthographic Decals](../../../objects/decals/ortho/index.md)*** and ***[Particle Systems](../../../objects/effects/particles/index.md)***. The foam effect responds to the boat's velocity in real time:


- **Decal size** is adjusted based on the area covered by particles
- **Particle lifetime, spawn rate, and velocity** are scaled proportionally to the boat's speed.


A **[Beaufort](../../../objects/objects/water/water_object.md#creating_waves)** slider allows control over sea state - from calm (0) to stormy (8) - to observe how foam reacts in different wave conditions. This setup is ideal for adding convincing surface wake and motion trails to ships or watercraft in real-time environments.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/simulation/speed_boat*
