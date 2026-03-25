# Unigine::ConcaveConvexCompare Class (CPP)

**Header:** #include <UnigineMathLibConcave.h>


The structure is used to compare convex shapes volumes. It can be passed to sort functions as a comparison method.


## ConcaveConvexCompare Class

### Members

---

## int operator() ( const Convex* c0 , const Convex* c1 )

Compares the volume of two convex shapes.
### Arguments

- *const Convex** **c0** - First shape.
- *const Convex** **c1** - Second shape.

### Return value

1 if the first shape's volume is greater than the second shape's volume; otherwise 0.
