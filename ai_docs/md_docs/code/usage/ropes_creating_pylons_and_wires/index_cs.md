# Creating Pylons and Wires Using Ropes (CS)


![A Wire Attached to Pylons](pylons_wire.png)

*A Wire Attached to Pylons*


This example shows how to create a wire using a rope body and attach it to pylons. A tutorial teaching how to reproduce the same scene in UnigineEditor can be found here.


```csharp
// AppWorldLogic.cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
    class AppWorldLogic : WorldLogic
    {
        // World logic, it takes effect only when the world is loaded.
        // These methods are called right after corresponding world script's (UnigineScript) methods.

        ObjectDummy dummy1;
        ObjectDummy dummy2;
        ObjectMeshDynamic pylon1;
        ObjectMeshDynamic pylon2;
        ObjectMeshDynamic rope;
        PlayerSpectator player;

        /// method, creating a named pylon with a specified radius and height at pos
        ObjectMeshDynamic create_pylon(String name, float radius, float length, vec3 pos)
        {
            // creating a cylinder dynamic mesh
            ObjectMeshDynamic OM = Primitives.CreateCylinder(radius, length, 1, 6);

            // setting parameters
            OM.WorldTransform = new dmat4(MathLib.Translate(pos));
            OM.SetMaterialParameterFloat4("albedo_color", new vec4(0.1f, 0.1f, 0.0f, 1.0f), 0);
            OM.Name = name;

            return OM;
        }

        /// method, creating a named dummy body of a specified size at pos
        ObjectDummy createBodyDummy(String name, vec3 size, vec3 pos)
        {
            // creating a dummy object
            ObjectDummy OMD = new ObjectDummy();

            // setting parameters
            OMD.WorldTransform = new dmat4(MathLib.Translate(pos));
            OMD.Name = name;

            //assigning a dummy body to the dummy object and adding a box shape	to it
            new BodyDummy(OMD);
            OMD.Body.AddShape(new ShapeBox(size), MathLib.Translate(0.0f, 0.0f, 0.0f));

            return OMD;
        }

        /// method, creating a named rope with specified parameters at pos
        ObjectMeshDynamic createBodyRope(String name, float radius, float length, int segments, int slices, dmat4 tm)
        {
            // creating a cylinder dynamic mesh
            ObjectMeshDynamic OMD = Primitives.CreateCylinder(radius, length, segments, slices);

            // setting parameters
            OMD.WorldTransform = tm;
            OMD.SetMaterialParameterFloat4("albedo_color", new vec4(0.5f, 0.5f, 0.0f, 1.0f), 0);
            OMD.Name = name;

            //assigning a rope body to the dynamic mesh object and setting rope parameters
            BodyRope body = new BodyRope(OMD);
            body.Mass = 1.0f;
            body.Radius = 0.25f;
            body.Friction = 0.5f;
            body.Restitution = 0.05f;
            body.Rigidity = 0.05f;
            body.LinearStretch = 0.5f;

            return OMD;
        }

        /* .. */

        public override bool Init()
        {
            // setting up player
            player = new PlayerSpectator();
            player.Position = new dvec3(0.0f, -23.401f, 15.5f);
            player.SetDirection(new vec3(0.0f, 1.0f, -0.4f), new vec3(0.0f, 0.0f, -1.0f));
            Game.Player = player;

            // creating dummy objects to attach a rope to and placing them on the top of each pylon
            dummy1 = createBodyDummy("fixpoint1", new vec3(0.5f, 0.5f, 0.5f), new vec3(-12.0f, 0.0f, 15.0f));
            dummy2 = createBodyDummy("fixpoint2", new vec3(0.5f, 0.5f, 0.5f), new vec3(12.0f, 0.0f, 15.0f));

            // creating pylons
            pylon1 = create_pylon("Pylon1", 0.3f, 17, new vec3(-12.2f, 0.0f, 7.0f));
            pylon2 = create_pylon("Pylon2", 0.3f, 17, new vec3(12.2f, 0.0f, 7.0f));

            // creating a rope
            rope = createBodyRope("MyRope", 0.05f, 24, 96, 6, new dmat4(MathLib.Translate(0.0f, 0.0f, 15.0f) * MathLib.RotateY(-90.0f)));

            // creating 2 particles joints to attach the rope to dummy bodies
            new JointParticles(dummy1.Body, rope.Body, dummy1.Position, new vec3(0.55f));
            new JointParticles(dummy2.Body, rope.Body, dummy2.Position, new vec3(0.55f));

            return true;
        }

        /* .. */

    }
}

```
