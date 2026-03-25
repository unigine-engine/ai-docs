# Expression Node


![](../img/expression.png)

### Description

This node is used to write simple arithmetic operations as well as to change the number of data components, or as a swizzle. The contents to be put to each channel are separated with a comma.

## Usage Examples

**Example 1**

[![](../img/expression_ex_1.png)](../img/expression_ex_1.png)


- You can easily take only the Y channel from a Float4 by simply writing "`Y`". Thus, you'll have a Float4 -> Float conversion.
- You can swap channels of a Float4 value by writing "`Z,W,Y,X`".
- You can write simple arithmetic opreations like "`1-X`" or "`X*2`".
- The following expression will work as well: "`pow(X,Y)+2, lerp(X,Y,Z)`".
