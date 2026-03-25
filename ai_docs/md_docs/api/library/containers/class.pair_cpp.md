# Unigine::Pair Class (CPP)

**Header:** #include <UniginePair.h>


A pair container template. The class has the *first* and the *second* members that allow access to the corresponding elements of the pair.


## Pair Class

### Members

---

## Pair ( )

Default constructor that produces an empty pair.
## Pair ( const TypeFirst& f , const TypeSecond& s )

Constructor. Creates a pair of given elements.
### Arguments

- *const TypeFirst&* **f** - First pair element.
- *const TypeSecond&* **s** - Second pair element.

## void Pair ( const Pair <OtherFirst,OtherSecond>& o )

Replaces the pair with a given one.
### Arguments

- *const [Pair](../../../api/library/containers/class.pair_cpp.md)<OtherFirst,OtherSecond>&* **o** - Pair.

## void Pair ( Pair <OtherFirst,OtherSecond>& o )

Replaces the pair with a given one.
### Arguments

- *[Pair](../../../api/library/containers/class.pair_cpp.md)<OtherFirst,OtherSecond>&* **o** - Pair.

## void Pair ( OtherFirst&& f , OtherSecond&& s )

Replaces the pair elements with given ones.
### Arguments

- *OtherFirst&&* **f** - First pair element.
- *OtherSecond&&* **s** - Second pair element.

## Pair <TypeFirst, TypeSecond> & operator= ( Pair <OtherFirst,OtherSecond>& o )

Assignment operator for the pair.
### Arguments

- *[Pair](../../../api/library/containers/class.pair_cpp.md)<OtherFirst,OtherSecond>&* **o** - Pair to be assigned.

## void swap ( Pair& o )

Swaps two pairs.
### Arguments

- *Pair&* **o** - Pair to swap.

## bool operator== ( const Pair <OtherFirst,OtherSecond>& o ) const

Checks if both elements of pairs are equal.
### Arguments

- *const [Pair](../../../api/library/containers/class.pair_cpp.md)<OtherFirst,OtherSecond>&* **o** - Pair.

### Return value

true if pairs are equal; otherwise false.
## bool operator!= ( const Pair <OtherFirst,OtherSecond>& o ) const

Checks if two pairs are not equal.
### Arguments

- *const [Pair](../../../api/library/containers/class.pair_cpp.md)<OtherFirst,OtherSecond>&* **o** - Pair.

### Return value

true if pairs are not equal; otherwise false.
## bool operator< ( const Pair <OtherFirst,OtherSecond>& o ) const

Checks if the pair is less than a given one: compares the first elements and only if they are equal, compares the second elements.
### Arguments

- *const [Pair](../../../api/library/containers/class.pair_cpp.md)<OtherFirst,OtherSecond>&* **o** - Pair.

### Return value

true if the pair is less than a given one; otherwise false.
## bool operator> ( const Pair <OtherFirst,OtherSecond>& o ) const

Checks if the pair is greater than a given one: compares the first elements and only if they are equal, compares the second elements.
### Arguments

- *const [Pair](../../../api/library/containers/class.pair_cpp.md)<OtherFirst,OtherSecond>&* **o** - Pair.

### Return value

true if the pair is greater than a given one; otherwise false.
## bool operator<= ( const Pair <OtherFirst,OtherSecond>& o ) const

Checks if the pair is less than or equal to a given one: compares the first elements and if they are equal, compares the second elements.
### Arguments

- *const [Pair](../../../api/library/containers/class.pair_cpp.md)<OtherFirst,OtherSecond>&* **o** - Pair.

### Return value

true if the pair is less than or equal to a given one; otherwise false.
## bool operator>= ( const Pair <OtherFirst,OtherSecond>& o ) const

Checks if the pair is greater than or equal to a given one: compares the first elements and if they are equal, compares the second elements.
### Arguments

- *const [Pair](../../../api/library/containers/class.pair_cpp.md)<OtherFirst,OtherSecond>&* **o** - Pair.

### Return value

true if the pair is greater than or equal to a given one; otherwise false.
