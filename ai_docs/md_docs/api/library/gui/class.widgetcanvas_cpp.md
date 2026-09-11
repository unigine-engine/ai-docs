# Unigine::WidgetCanvas Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class enables to create a canvas on which lines, polygons, and text can be drawn. It performs clipping of the visible region while rendering.


The object of this class looks as follows:


![Canvas widget with polygons](../../../code/gui/ui/widgets/canvas.png)


> **Notice:** A polygon can be a triangle, a rectangle, a pentagon, and so on: it can have any number of sides. For example, if you add 4 points to the canvas via the *[addPolygonPoint()](#addPolygonPoint_int_vec3_int)* function, the 4-sided polygon will be drawn.


By default, all polygons are 2-sided, meaning that both sides of the polygon are visible at the same time. If it is necessary to make only one of them visible, you can [set the 2-sided flag](#setPolygonTwoSided_int_int_void) to 0.


To increase performance, you can use point indices instead of point coordinates. See the following functions for more details:


- *[addLineIndex()](#addLineIndex_int_int_int)*
- *[addPolygonIndex()](#addPolygonIndex_int_int_int)*


> **Notice:** - To reset the ID counter when re-drawing the widget canvas don't forget to call the [*clear()*](#clear_void) method.
> - The widget canvas doesn't perform depth testing. So, you will have to implement depth testing by using functions that set the rendering order for lines and polygons.


### See Also


- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -
  -


## WidgetCanvas Class

### Members

## int getNumPolygons () const

Returns the current number of polygons drawn in the canvas widget.
### Return value

Current number of polygons drawn in the canvas widget
## int getNumLines () const

Returns the current number of lines drawn in the canvas widget.
### Return value

Current number of lines drawn in the canvas widget
## int getNumTexts () const

Returns the current number of text strings drawn in the canvas widget.
### Return value

Current number of text strings drawn in the canvas widget
## void setTransform ( const Math:: mat4 & transform )

Sets a new transformation matrix applied to all primitives on the canvas widget.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation matrix applied to all primitives on the canvas widget

## Math:: mat4 getTransform () const

Returns the current transformation matrix applied to all primitives on the canvas widget.
### Return value

Current transformation matrix applied to all primitives on the canvas widget
## void setColor ( const Math:: vec4 & color )

Sets a new background color of the canvas widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The background color of the canvas widget

## Math:: vec4 getColor () const

Returns the current background color of the canvas widget.
### Return value

Current background color of the canvas widget
## void setTexture ( const char * texture )

Sets a new path to the texture used by default for new polygons added to the canvas widget.
### Arguments

- *const char ** **texture** - The path to the default texture for new polygons added to the canvas widget

## const char * getTexture () const

Returns the current path to the texture used by default for new polygons added to the canvas widget.
### Return value

Current path to the default texture for new polygons added to the canvas widget
---

## static WidgetCanvasPtr create ( const Ptr < Gui > & gui )

Constructor. Creates a new canvas widget and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - GUI, to which the canvas will belong.

## static WidgetCanvasPtr create ( )

Constructor. Creates a new canvas widget and adds it to the Engine GUI.
## void setImage ( const Ptr < Image > & image )

Sets the image used as the default texture for new polygons added to the canvas widget.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Texture image.

## Ptr < Image > getImage ( ) const

Returns the current default texture image used for new polygons added to the canvas widget.
### Return value

Texture image.
## int getLine ( int num ) const

Returns the canvas element ID of the line by its number.
### Arguments

- *int* **num** - Line number in range from 0 to the total number lines.

### Return value

Canvas element ID of the line.
## void setLineColor ( int line , const Math:: vec4 & color )

Updates the color of the specified line.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Line color.

## Math:: vec4 getLineColor ( int line ) const

Returns the current color of the specified line.
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

Line color.
## int getLineIndex ( int line , int num ) const

Returns the index of the point of the line segment by its number.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - The number of the index of the point of the line segment.

### Return value

Index of the point of the line segment.
## int getLineIntersection ( int x , int y , float distance ) const

Checks whether the specified point (e.g. the mouse cursor) intersects with lines drawn in the canvas widget.
### Arguments

- *int* **x** - X coordinate of the point.
- *int* **y** - Y coordinate of the point.
- *float* **distance** - Point radius acceptable for detecting intersection.

### Return value

Number of the first intersected line with the highest rendering order in the array of lines. If no intersections are found, -1 will be returned.
## void setLineOrder ( int line , int order )

Updates the rendering order of the given line (the higher the value, the later the line will be rendered atop other elements).
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **order** - Rendering order.

## int getLineOrder ( int line ) const

Returns the rendering order of the given line (the higher the value, the later the line is rendered atop other elements).
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

Rendering order.
## Math:: vec3 getLinePoint ( int line , int num ) const

Returns the coordinates of the specified line segment point.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - Number of the line segment point.

### Return value

Segment point coordinates.
## void setLineTransform ( int line , const Math:: mat4 & transform )

Updates the transformation matrix of the specified line.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## Math:: mat4 getLineTransform ( int line ) const

Returns the current transformation matrix of the specified line.
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

Transformation matrix.
## int getNumLineIndices ( int line ) const

Returns the total number of indices set for the points that form line segments.
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

The number of indices set for the points that form line segments.
## int getNumLinePoints ( int line ) const

Returns the number of the points that create line segments.
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

Number of line segment points.
## int getNumPolygonIndices ( int polygon ) const

Returns the total number of indices set for points of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

The number of indices set for points that form polygons.
## int getNumPolygonPoints ( int polygon ) const

Returns the number of points that form the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Number of polygon points.
## int getPolygon ( int num ) const

Returns the canvas element ID of the polygon by its index.
### Arguments

- *int* **num** - Polygon number in range from 0 to the total number of polygons.

### Return value

Canvas element ID of the polygon.
## int getPolygonBlendDestFunc ( int polygon ) const

Returns the blending mode of the destination color for the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Blending mode of the destination color (one of the BLEND_*).
## void setPolygonBlendFunc ( int polygon , int src , int dest )

Updates the blending coefficients for specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **src** - Blending mode for the source screen buffer color (one of the BLEND_*).
- *int* **dest** - Blending mode for the destination polygon color (one of the BLEND_*).

## int getPolygonBlendSrcFunc ( int polygon ) const

Returns the blending mode of the source screen buffer color for the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Blending mode of the source screen buffer color (one of the BLEND_*).
## void setPolygonColor ( int polygon , const Math:: vec4 & color )

Updates the color of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Polygon color.

## Math:: vec4 getPolygonColor ( int polygon ) const

Returns the current color of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Polygon color.
## void setPolygonImage ( int polygon , const Ptr < Image > & image )

Sets an image for a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to set.

## Ptr < Image > getPolygonImage ( int polygon )

Returns the current image set for a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Current image set for the specified polygon.
## int getPolygonIndex ( int polygon , int num ) const

Returns the index of the point of the polygon by its number.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - The number of the index of the point of the polygon.

### Return value

Index of the point of the polygon.
## int getPolygonIntersection ( int x , int y ) const

Checks whether the specified point (e.g. the mouse cursor) intersects with widget polygons.
### Arguments

- *int* **x** - X coordinate of the point.
- *int* **y** - Y coordinate of the point.

### Return value

Number of the first intersected polygon with the highest rendering order in the array of polygons. If no intersections are found, -1 will be returned.
## void setPolygonOrder ( int polygon , int order )

Updates the rendering order of the given polygon (the higher the value, the later the polygon will be rendered atop other elements).
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **order** - Rendering order.

## int getPolygonOrder ( int polygon ) const

Returns the rendering order of the given polygon (the higher the value, the later the polygon is rendered atop other elements).
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Rendering order.
## int addPolygonPoint ( int polygon , const Math:: vec3 & point )

Adds a new point to the polygon in the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Polygon point coordinates.

### Return value

Number of the added polygon point.
## int addPolygonPoint ( int polygon )

Adds a new point to the polygon in the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Number of the added polygon point.
## int addPolygonPoint ( int polygon , const Math:: vec3 & point , const Math:: vec2 & texcoord )

Adds a new point to the polygon in the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Polygon point coordinates.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **texcoord** - Texture coordinates for the point.

### Return value

Number of the added polygon point.
## void setPolygonPoint ( int polygon , int num , const Math:: vec3 & point )

Sets the coordinates of the specified polygon point.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Number of the polygon point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Polygon point coordinates.

## Math:: vec3 getPolygonPoint ( int polygon , int num ) const

Returns the coordinates of the specified polygon point.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Number of the polygon point.

### Return value

Polygon point coordinates.
## void setPolygonTexCoord ( int polygon , const Math:: vec2 & texcoord )

Updates the texture coordinates for the last added point of the polygon. Before calling this function, the point should be added with addPolygonPoint().
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **texcoord** - Texture coordinates for the point.

## void setPolygonTexCoord ( int polygon , int num , const Math:: vec2 & texcoord )

Sets the texture coordinates of the specified point of the polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Number of the polygon point.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **texcoord** - Texture coordinates of the point.

## Math:: vec2 getPolygonTexCoord ( int polygon , int num ) const

Returns the texture coordinates of the specified point of the polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Number of the polygon point.

### Return value

Texture coordinates of the point.
## void setPolygonTexture ( int polygon , const char * name )

Sets a texture from a file for the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *const char ** **name** - Path to the texture.

## const char * getPolygonTexture ( int polygon ) const

Returns the current texture set for a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Path to the texture.
## void setPolygonTransform ( int polygon , const Math:: mat4 & transform )

Updates the transformation matrix of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## Math:: mat4 getPolygonTransform ( int polygon ) const

Returns the current transformation matrix of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Transformation matrix.
## void setPolygonTwoSided ( int polygon , int two_sided )

Sets polygon two sided option.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **two_sided** - two sided option.

## int getPolygonTwoSided ( int polygon ) const

Gets polygon two sided option.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Returns two sided option.
## void setPolygonWrapRepeat ( int polygon , int repeat )

Sets texture tiling for a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **repeat** - Positive number to enable texture tiling; 0 to disable it.

## int getPolygonWrapRepeat ( int polygon ) const

Returns a value indicating if texture tiling is enabled for the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

1 if texture tiling is enabled; 0 if disabled.
## int getText ( int num ) const

Returns the canvas element ID of the text string by its number.
### Arguments

- *int* **num** - Number of the text element.

### Return value

Canvas element ID of the text string.
## void setTextAlign ( int text , int align )

Updates the alignment of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *int* **align** - Text alignment. One or a combination of the *[Gui::ALIGN_*](../../../api/library/gui/class.gui_cpp.md#ALIGN_BOTTOM)* values (TOP, BOTTOM, LEFT, RIGHT, CENTER).

## int getTextAlign ( int text ) const

Returns the current alignment of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text alignment. One or a combination of the *[Gui::ALIGN_*](../../../api/library/gui/class.gui_cpp.md#ALIGN_BOTTOM)* values (TOP, BOTTOM, LEFT, RIGHT, CENTER).
## void setTextColor ( int text , const Math:: vec4 & color )

Updates the color of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Font color.

## Math:: vec4 getTextColor ( int text ) const

Returns the current color of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Font color.
## int getTextHeight ( int text ) const

Returns the height of the given text element on the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text height in pixels.
## int getTextIntersection ( int x , int y ) const

Checks whether the specified point (e.g. the mouse cursor) intersects with a bounding box of widget text.
### Arguments

- *int* **x** - coordinate of the point.
- *int* **y** - coordinate of the point.

### Return value

ID of the intersected text lines array; otherwise, -1 is returned if no intersections are found.
## void setTextOrder ( int text , int order )

Updates the rendering order of the given text element (the higher the value, the later the text will be rendered atop other elements).
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *int* **order** - Rendering order.

## int getTextOrder ( int text ) const

Returns the rendering order of the given text element (the higher the value, the later the text is rendered atop other elements).
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Rendering order.
## void setTextOutline ( int text , int outline )

Sets a value indicating if the text should be rendered casting a shadow. Positive or negative values set the distance in pixels to offset the outline. The default is 0 (no outlining).
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *int* **outline** - Outline offset:

  - Positive values set offset in the bottom-right corner direction.
  - Negative values set offset in the top-left corner direction (the outline will overlap widget text).
  - 0 is not to use outlining.

## int getTextOutline ( int text ) const

Returns a value indicating if the text is rendered casting a shadow. Positive or negative values determine the distance in pixels used to offset the outline.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Positive value if the outline is offset in the bottom-right corner direction. Negative value if the outline is offset in the top-left corner direction. 0 if font is not outlined.
## void setTextPosition ( int text , const Math:: vec2 & position )

Updates the position of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **position** - Text position coordinates.

## Math:: vec2 getTextPosition ( int text ) const

Returns the current position of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text position coordinates.
## void setTextSize ( int text , int size )

Updates the font size of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *int* **size** - Font size.

## int getTextSize ( int text ) const

Returns the current font size of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Font size.
## void setTextText ( int text , const char * str )

Updates the text to be drawn in the given text element on the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *const char ** **str** - Text string.

## const char * getTextText ( int text ) const

Returns the current text drawn in the given text element on the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text string.
## void setTextTransform ( int text , const Math:: mat4 & transform )

Updates the transformation matrix of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## Math:: mat4 getTextTransform ( int text ) const

Returns the current transformation matrix of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Transformation matrix.
## int getTextWidth ( int text ) const

Returns the width of the given text element on the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text width in pixels.
## int addLine ( int order = 0 )

Adds a new line to the canvas widget. By default, it is rendered in white color.
### Arguments

- *int* **order** - Rendering order (the higher the value, the later the line will be rendered atop other elements).

### Return value

Canvas element ID for the added line.
## int addLineIndex ( int line , int index )

Adds an index for the point of the line segment in the canvas widget. Notice that before adding indices, you should add all points that form the line.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **index** - Index of the point of the line segment.

### Return value

The number of the added index in the array of line indices.
## int addLinePoint ( int line , const Math:: vec3 & point )

Adds a new segment to the line in the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Segment point coordinates.

### Return value

Number of the added line segment point.
## int addLinePoint ( int line , const Math::vec2& point )

Adds a new segment to the line in the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *const  Math::vec2&* **point** - Segment point coordinates.

### Return value

Number of the added line segment point.
## void setLinePoint ( int line , int num , const Math::vec3& point )

Sets a line segment in the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - Index of the point in the array of line points.
- *const  Math::vec3&* **point** - Line point coordinates.

## void setLinePoint ( int line , int num , const Math::vec2& point )

Sets a line segment in the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - Index of the point in the array of line points.
- *const  Math::vec2&* **point** - Line point coordinates.

## int addPolygon ( int polygon = 0 )

Adds a new polygon to the canvas widget. By default, it is rendered in white color. Texture tiling mode is disabled.
### Arguments

- *int* **polygon** - Rendering order (the higher the value, the later the polygon will be rendered atop other elements).

### Return value

Canvas element ID for the added polygon.
## int addPolygonIndex ( int polygon , int index )

Adds an index for the point of the polygon in the canvas widget. Notice that before adding indices, you should add all points that form the polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **index** - Index of the point of the polygon.

### Return value

The number of the added index in the array of polygon indices.
## int addText ( int order = 0 )

Adds a new text string to the canvas widget. By default, it is rendered in white color. If a font size is not set for the canvas widget, a default one is used. No shadow is cast from a text (no outlining). Text width and height on the canvas widget are equal to 0.
### Arguments

- *int* **order** - Rendering order (the higher the value, the later the text will be rendered atop other elements).

### Return value

Canvas element ID of the added text string.
## void clear ( )

Clears the canvas widget: deletes all drawn lines, polygons and text.
## void clearLineIndices ( int line )

Clears the array of indices set for points that form the given line.
### Arguments

- *int* **line** - Canvas element ID of the line.

## void clearLinePoints ( int line )

Deletes all points that make up a given line.
### Arguments

- *int* **line** - Canvas element ID of the line.

## void clearPolygonIndices ( int polygon )

Clears the array of indices set for points that form the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

## void clearPolygonPoints ( int polygon )

Deletes all points that make up a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

## void removeLine ( int line )

Removes the line from the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.

## void removeLineIndex ( int line , int num )

Removes the index with the given number from the array of the line indices.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - The number of the index in the array of the line indices.

## void removeLinePoint ( int line , int num )

Removes the segment of the line from the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - Number of the point to remove.

## void removePolygon ( int polygon )

Removes the polygon from the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

## void removePolygonIndex ( int polygon , int num )

Removes the index with the given number from the array of the polygon indices.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - The number of the index in the array of the polygon indices.

## void removePolygonPoint ( int polygon , int num )

Removes the point of the polygon from the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Polygon point coordinates.

## void removeText ( int text )

Removes the text from the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.

## void setPolygonGPUTexture ( int polygon , const Ptr < Texture > & texture )

Sets a GPU texture for the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - GPU texture

## Ptr < Texture > getPolygonGPUTexture ( int polygon ) const

Returns the current GPU texture for the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

GPU texture
## void setTextFont ( int text , const char * path )

Sets a new font to be used for the text with the given ID.
### Arguments

- *int* **text** - ID of the text.
- *const char ** **path** - Path to the font file (`.ttf`) to be used.

## void setTextPixelPerfect ( int text , bool pixel_perfect )

Sets the text with the given ID as pixel perfect.
### Arguments

- *int* **text** - ID of the text.
- *bool* **pixel_perfect** - true to make the text pixel perfect, otherwise, false.

## bool getTextPixelPerfect ( int text ) const

Returns a value indicating if the text with the given ID is pixel perfect.
### Arguments

- *int* **text** - ID of the text.

### Return value

true if the text is pixel perfect, otherwise, false.
## void setPolygonIntersection ( int polygon , bool intersection )

Specifies whether the polygon with the given ID will participate in the intersection check.
### Arguments

- *int* **polygon** - ID of the polygon.
- *bool* **intersection** - true to make the polygon participate in the intersection check, otherwise, false.

## bool isPolygonIntersection ( int polygon ) const

Returns a value indicating if the polygon with the given ID participates in the intersection check.
### Arguments

- *int* **polygon** - ID of the polygon.

### Return value

true if the polygon participates in the intersection check, otherwise, false.
## void setPolygonRender ( int polygon , bool render )

Sets the rendering state for the polygon with the given ID.
### Arguments

- *int* **polygon** - ID of the polygon.
- *bool* **render** - true to render the polygon, otherwise, false.

## bool isPolygonRender ( int polygon ) const

Returns a value indicating if the polygon with the given ID is rendered.
### Arguments

- *int* **polygon** - ID of the polygon.

### Return value

true if the polygon is rendered, otherwise, false.
## int getPolygonTextureWidth ( int polygon ) const

Returns the width of the polygon texture.
### Arguments

- *int* **polygon** - ID of the polygon.

### Return value

Width of the polygon texture.
## int getPolygonTextureHeight ( int polygon ) const

Returns the height of the polygon texture.
### Arguments

- *int* **polygon** - ID of the polygon.

### Return value

Height of the polygon texture.
