# Unigine::Plugins::IG::SymbolPolyline Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


## SymbolPolyline Class

### Members

---

## void addPoint ( float x , float y )

Sets the point in the coordinates of the plane.
### Arguments

- *float* **x** - Horizontal offset from the plane's origin.
- *float* **y** - Vertical offset from the plane's origin.

## void setFill ( bool value )

Toggles filling of the figure created by lines on and off.
### Arguments

- *bool* **value** - true to make the figure filled, otherwise false.

## void setClosed ( bool value )

Enables and disables connection of the last point with the first point that makes the line closed.
### Arguments

- *bool* **value** - true to make the figure looped, otherwise false.

## void setVertexOrderStrip ( bool value )

Toggles on and off creation of a triangle strip � a connected series of filled triangles formed from an ordered set of vertices. The first triangle is formed from the first three vertices. Each successive triangle is formed from the last two vertices and the next vertex in the set.
### Arguments

- *bool* **value** - true to enable a triangle strip, false to disable it.
