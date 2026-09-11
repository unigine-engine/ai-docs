# Unigine::Plugins::IG::IGIntersection Structure

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


This data structure stores the result of an intersection (intersection point coordinates as well as normal and texture coordinates, intersected object and surface index, intersection mask) and has the following set of parameters:


| **surface** | Intersected surface number. |
|---|---|
| **mask** | Intersection mask. |
| **object** | Intersected object. |
| **point** | Coordinates of the intersection point. |
| **normal** | Normal of the intersection point. |
| **texcoord** | Texture coordinates of the intersection point. |


The **IGIntersection** structure is declared as follows:


```cpp
struct IGIntersection
{
	int surface;
	unsigned int mask;
	Unigine::ObjectPtr object;
	Unigine::Math::Vec3 point;
	Unigine::Math::vec3 normal;
	Unigine::Math::vec4 texcoord;
};

```
