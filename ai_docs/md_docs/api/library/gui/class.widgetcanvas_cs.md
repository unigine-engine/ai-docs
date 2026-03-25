# Unigine::WidgetCanvas Class (CS)

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

### Properties

## 🔒︎ int NumPolygons

The number of polygons drawn in the canvas widget.
## 🔒︎ int NumLines

The number of lines drawn in the canvas widget.
## 🔒︎ int NumTexts

The number of text strings drawn in the canvas widget.
## mat4 Transform

The transformation matrix applied to all primitives on the canvas widget.
## vec4 Color

The background color of the canvas widget.
## string Texture

The path to the texture used by default for new polygons added to the canvas widget.
### Members

---

## WidgetCanvas ( Gui gui )

Constructor. Creates a new canvas widget and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - GUI, to which the canvas will belong.

## WidgetCanvas ( )

Constructor. Creates a new canvas widget and adds it to the Engine GUI.
## void SetImage ( Image image )

Sets the image used as the default texture for new polygons added to the canvas widget.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Texture image.

## Image GetImage ( )

Returns the current default texture image used for new polygons added to the canvas widget.
### Return value

Texture image.
## int GetLine ( int num )

Returns the canvas element ID of the line by its number.
### Arguments

- *int* **num** - Number of the line in the array of lines drawn in the widget canvas.

### Return value

Canvas element ID of the line.
## void SetLineColor ( int line , vec4 color )

Updates the color of the specified line.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *vec4* **color** - Line color.

## vec4 GetLineColor ( int line )

Returns the current color of the specified line.
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

Line color.
## int GetLineIndex ( int line , int num )

Returns the index of the point of the line segment by its number.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - The number of the index of the point of the line segment.

### Return value

Index of the point of the line segment.
## int GetLineIntersection ( int x , int y , float distance )

Checks whether the specified point (e.g. the mouse cursor) intersects with lines drawn in the canvas widget.
### Arguments

- *int* **x** - X coordinate of the point.
- *int* **y** - Y coordinate of the point.
- *float* **distance** - Point radius acceptable for detecting intersection.

### Return value

Number of the first intersected line with the highest rendering order in the array of lines. If no intersections are found, -1 will be returned.
## void SetLineOrder ( int line , int order )

Updates the rendering order of the given line (the higher the value, the later the line will be rendered atop other elements).
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **order** - Rendering order.

## int GetLineOrder ( int line )

Returns the rendering order of the given line (the higher the value, the later the line is rendered atop other elements).
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

Rendering order.
## vec3 GetLinePoint ( int line , int num )

Returns the coordinates of the specified line segment point.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - Number of the line segment point in the array of line points.

### Return value

Segment point coordinates.
## void SetLineTransform ( int line , mat4 transform )

Updates the transformation matrix of the specified line.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *mat4* **transform** - Transformation matrix.

## mat4 GetLineTransform ( int line )

Returns the current transformation matrix of the specified line.
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

Transformation matrix.
## int GetNumLineIndices ( int line )

Returns the total number of indices set for the points that form line segments.
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

The number of indices set for the points that form line segments.
## int GetNumLinePoints ( int line )

Returns the number of the points that create line segments.
### Arguments

- *int* **line** - Canvas element ID of the line.

### Return value

Number of line segment points.
## int GetNumPolygonIndices ( int polygon )

Returns the total number of indices set for points of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

The number of indices set for points that form polygons.
## int GetNumPolygonPoints ( int polygon )

Returns the number of points that form the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Number of polygon points.
## int GetPolygon ( int num )

Returns the canvas element ID of the polygon by its index.
### Arguments

- *int* **num** - Number of the polygon in the array of polygons drawn in the widget canvas.

### Return value

Canvas element ID of the polygon.
## int GetPolygonBlendDestFunc ( int polygon )

Returns the blending mode of the destination color for the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Blending mode of the destination color (one of the BLEND_*).
## void SetPolygonBlendFunc ( int polygon , int src , int dest )

Updates the blending coefficients for specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **src** - Blending mode for the source screen buffer color (one of the *[BLEND_*](../../../api/library/gui/class.gui_cs.md#BLEND_NONE)* variables).
- *int* **dest** - Blending mode for the destination polygon color (one of the *[BLEND_*](../../../api/library/gui/class.gui_cs.md#BLEND_NONE)* variables).

## int GetPolygonBlendSrcFunc ( int polygon )

Returns the blending mode of the source screen buffer color for the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Blending mode of the source screen buffer color (one of the BLEND_*).
## void SetPolygonColor ( int polygon , vec4 color )

Updates the color of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *vec4* **color** - Polygon color.

## vec4 GetPolygonColor ( int polygon )

Returns the current color of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Polygon color.
## void SetPolygonImage ( int polygon , Image image )

Sets an image for a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to set.

## Image GetPolygonImage ( int polygon )

Returns the current image set for a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Current image set for the specified polygon.
## int GetPolygonIndex ( int polygon , int num )

Returns the index of the point of the polygon by its number.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - The number of the index of the point of the polygon.

### Return value

Index of the point of the polygon.
## int GetPolygonIntersection ( int x , int y )

Checks whether the specified point (e.g. the mouse cursor) intersects with widget polygons.
### Arguments

- *int* **x** - X coordinate of the point.
- *int* **y** - Y coordinate of the point.

### Return value

Number of the first intersected polygon with the highest rendering order in the array of polygons. If no intersections are found, -1 will be returned.
## void SetPolygonOrder ( int polygon , int order )

Updates the rendering order of the given polygon (the higher the value, the later the polygon will be rendered atop other elements).
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **order** - Rendering order.

## int GetPolygonOrder ( int polygon )

Returns the rendering order of the given polygon (the higher the value, the later the polygon is rendered atop other elements).
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Rendering order.
## int AddPolygonPoint ( int polygon , vec3 point )

Adds a new point to the polygon in the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *vec3* **point** - Polygon point coordinates.

### Return value

Number of the added polygon point.
## int AddPolygonPoint ( int polygon )

Adds a new point to the polygon in the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Number of the added polygon point.
## int AddPolygonPoint ( int polygon , vec3 point , vec2 texcoord )

Adds a new point to the polygon in the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *vec3* **point** - Polygon point coordinates.
- *vec2* **texcoord** - Texture coordinates for the point.

### Return value

Number of the added polygon point.
## void SetPolygonPoint ( int polygon , int num , vec3 point )

Sets the coordinates of the specified polygon point.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Number of the polygon point in the array of polygon points.
- *vec3* **point** - Polygon point coordinates.

## vec3 GetPolygonPoint ( int polygon , int num )

Returns the coordinates of the specified polygon point.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Number of the polygon point in the array of polygon points.

### Return value

Polygon point coordinates.
## void SetPolygonTexCoord ( int polygon , vec2 texcoord )

Updates the texture coordinates for the last added point of the polygon. Before calling this function, the point should be added with addPolygonPoint().
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *vec2* **texcoord** - Texture coordinates for the point.

## void SetPolygonTexCoord ( int polygon , int num , vec2 texcoord )

Sets the texture coordinates of the specified point of the polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Number of the polygon point in the array of polygon points.
- *vec2* **texcoord** - Texture coordinates of the point.

## vec2 GetPolygonTexCoord ( int polygon , int num )

Returns the texture coordinates of the specified point of the polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Number of the polygon point in the array of polygon points.

### Return value

Texture coordinates of the point.
## void SetPolygonTexture ( int polygon , string name )

Sets a texture from a file for the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *string* **name** - Path to the texture.

## string GetPolygonTexture ( int polygon )

Returns the current texture set for a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Path to the texture.
## void SetPolygonTransform ( int polygon , mat4 transform )

Updates the transformation matrix of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *mat4* **transform** - Transformation matrix.

## mat4 GetPolygonTransform ( int polygon )

Returns the current transformation matrix of the specified polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Transformation matrix.
## void SetPolygonTwoSided ( int polygon , int two_sided )

Sets polygon two sided option.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **two_sided** - 1 to make the polygon 2-sided; otherwise, 0.

## int GetPolygonTwoSided ( int polygon )

Gets polygon two sided option.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

Returns two sided option.
## void SetPolygonWrapRepeat ( int polygon , int repeat )

Sets texture tiling for a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **repeat** - Positive number to enable texture tiling; 0 to disable it.

## int GetPolygonWrapRepeat ( int polygon )

Returns a value indicating if texture tiling is enabled for the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

1 if texture tiling is enabled; 0 if disabled.
## int GetText ( int num )

Returns the canvas element ID of the text string by its number.
### Arguments

- *int* **num** - Number of the text element.

### Return value

Canvas element ID of the text string.
## void SetTextAlign ( int text , int align )

Updates the alignment of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *int* **align** - Text alignment. One or a combination of the *[Gui.ALIGN_*](../../../api/library/gui/class.gui_cs.md#ALIGN_BOTTOM)* values (TOP, BOTTOM, LEFT, RIGHT, CENTER).

## int GetTextAlign ( int text )

Returns the current alignment of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text alignment. One or a combination of the *[Gui.ALIGN_*](../../../api/library/gui/class.gui_cs.md#ALIGN_BOTTOM)* values (TOP, BOTTOM, LEFT, RIGHT, CENTER).
## void SetTextColor ( int text , vec4 color )

Updates the color of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *vec4* **color** - Font color.

## vec4 GetTextColor ( int text )

Returns the current color of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Font color.
## int GetTextHeight ( int text )

Returns the height of the given text element on the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text height in pixels.
## int GetTextIntersection ( int x , int y )

Checks whether the specified point (e.g. the mouse cursor) intersects with a bounding box of widget text.
### Arguments

- *int* **x** - X coordinate of the point.
- *int* **y** - Y coordinate of the point.

### Return value

ID of the intersected text lines array; otherwise, -1 is returned if no intersections are found.
## void SetTextOrder ( int text , int order )

Updates the rendering order of the given text element (the higher the value, the later the text will be rendered atop other elements).
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *int* **order** - Rendering order.

## int GetTextOrder ( int text )

Returns the rendering order of the given text element (the higher the value, the later the text is rendered atop other elements).
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Rendering order.
## void SetTextOutline ( int text , int outline )

Sets a value indicating if the text should be rendered casting a shadow. Positive or negative values set the distance in pixels to offset the outline. The default is 0 (no outlining).
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *int* **outline** - Outline offset:

  - Positive values set offset in the bottom-right corner direction.
  - Negative values set offset in the top-left corner direction (the outline will overlap widget text).
  - **0** is not to use outlining.

## int GetTextOutline ( int text )

Returns a value indicating if the text is rendered casting a shadow. Positive or negative values determine the distance in pixels used to offset the outline.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Positive value if the outline is offset in the bottom-right corner direction. Negative value if the outline is offset in the top-left corner direction. 0 if font is not outlined.
## void SetTextPosition ( int text , vec2 position )

Updates the position of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *vec2* **position** - Text position.

## vec2 GetTextPosition ( int text )

Returns the current position of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text position coordinates.
## void SetTextSize ( int text , int size )

Updates the font size of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *int* **size** - Font size.

## int GetTextSize ( int text )

Returns the current font size of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Font size.
## void SetTextText ( int text , string str )

Updates the text to be drawn in the given text element on the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *string* **str** - Text string.

## string GetTextText ( int text )

Returns the current text drawn in the given text element on the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text string.
## void SetTextTransform ( int text , mat4 transform )

Updates the transformation matrix of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.
- *mat4* **transform** - Transformation matrix.

## mat4 GetTextTransform ( int text )

Returns the current transformation matrix of the specified text.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Transformation matrix.
## int GetTextWidth ( int text )

Returns the width of the given text element on the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.

### Return value

Text width in pixels.
## int AddLine ( int order = 0 )

Adds a new line to the canvas widget. By default, it is rendered in white color.
### Arguments

- *int* **order** - Rendering order (the higher the value, the later the line will be rendered atop other elements).

### Return value

Canvas element ID for the added line.
## int AddLineIndex ( int line , int index )

Adds an index for the point of the line segment in the canvas widget. Notice that before adding indices, you should add all points that form the line.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **index** - Index of the point of the line segment.

### Return value

The number of the added index in the array of line indices.
## int AddLinePoint ( int line , vec3 point )

Adds a new segment to the line in the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *vec3* **point** - Segment point coordinates.

### Return value

Number of the added line segment point.
## int AddLinePoint ( int line , vec2 point )

Adds a new segment to the line in the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *vec2* **point** - Segment point coordinates.

### Return value

Number of the added line segment point.
## void SetLinePoint ( int line , int num , vec3 point )

Sets a line segment in the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - Index of the point in the array of line points.
- *vec3* **point** - Line point coordinates.

## void SetLinePoint ( int line , int num , vec2 point )

Sets a line segment in the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - Index of the point in the array of line points.
- *vec2* **point** - Line point coordinates.

## int AddPolygon ( int polygon = 0 )

Adds a new polygon to the canvas widget. By default, it is rendered in white color. Texture tiling mode is disabled.
### Arguments

- *int* **polygon** - Rendering order (the higher the value, the later the polygon will be rendered atop other elements).

### Return value

Canvas element ID for the added polygon.
## int AddPolygonIndex ( int polygon , int index )

Adds an index for the point of the polygon in the canvas widget. Notice that before adding indices, you should add all points that form the polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **index** - Index of the point of the polygon.

### Return value

The number of the added index in the array of polygon indices.
## int AddText ( int order = 0 )

Adds a new text string to the canvas widget. By default, it is rendered in white color. If a font size is not set for the canvas widget, a default one is used. No shadow is cast from a text (no outlining). Text width and height on the canvas widget are equal to 0.
### Arguments

- *int* **order** - Rendering order (the higher the value, the later the text will be rendered atop other elements).

### Return value

Canvas element ID of the added text string.
## void Clear ( )

Clears the canvas widget: deletes all drawn lines, polygons and text.
## void ClearLineIndices ( int line )

Clears the array of indices set for points that form the given line.
### Arguments

- *int* **line** - Canvas element ID of the line.

## void ClearLinePoints ( int line )

Deletes all points that make up a given line.
### Arguments

- *int* **line** - Canvas element ID of the line.

## void ClearPolygonIndices ( int polygon )

Clears the array of indices set for points that form the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

## void ClearPolygonPoints ( int polygon )

Deletes all points that make up a given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

## void RemoveLine ( int line )

Removes the line from the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.

## void RemoveLineIndex ( int line , int num )

Removes the index with the given number from the array of the line indices.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - The number of the index in the array of the line indices.

## void RemoveLinePoint ( int line , int num )

Removes the segment of the line from the canvas widget.
### Arguments

- *int* **line** - Canvas element ID of the line.
- *int* **num** - Number of the point in the array of the line points.

## void RemovePolygon ( int polygon )

Removes the polygon from the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

## void RemovePolygonIndex ( int polygon , int num )

Removes the index with the given number from the array of the polygon indices.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - The number of the index in the array of the polygon indices.

## void RemovePolygonPoint ( int polygon , int num )

Removes the point of the polygon from the canvas widget.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *int* **num** - Polygon point coordinates.

## void RemoveText ( int text )

Removes the text from the canvas widget.
### Arguments

- *int* **text** - Canvas element ID of the text string.

## void SetPolygonGPUTexture ( int polygon , Texture texture )

Sets a GPU texture for the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - GPU texture

## Texture GetPolygonGPUTexture ( int polygon )

Returns the current GPU texture for the given polygon.
### Arguments

- *int* **polygon** - Canvas element ID of the polygon.

### Return value

GPU texture
## void SetTextFont ( int text , string path )

Sets a new font to be used for the text with the given ID.
### Arguments

- *int* **text** - ID of the text.
- *string* **path** - Path to the font file (`.ttf`) to be used.

## void SetTextPixelPerfect ( int text , bool pixel_perfect )

Sets the text with the given ID as pixel perfect.
### Arguments

- *int* **text** - ID of the text.
- *bool* **pixel_perfect** - true to make the text pixel perfect, otherwise, false.

## bool GetTextPixelPerfect ( int text )

Returns a value indicating if the text with the given ID is pixel perfect.
### Arguments

- *int* **text** - ID of the text.

### Return value

true if the text is pixel perfect, otherwise, false.
## void SetPolygonIntersection ( int polygon , bool intersection )

Specifies whether the polygon with the given ID will participate in the intersection check.
### Arguments

- *int* **polygon** - ID of the polygon.
- *bool* **intersection** - true to make the polygon participate in the intersection check, otherwise, false.

## bool IsPolygonIntersection ( int polygon )

Returns a value indicating if the polygon with the given ID participates in the intersection check.
### Arguments

- *int* **polygon** - ID of the polygon.

### Return value

true if the polygon participates in the intersection check, otherwise, false.
## void SetPolygonRender ( int polygon , bool render )

Sets the rendering state for the polygon with the given ID.
### Arguments

- *int* **polygon** - ID of the polygon.
- *bool* **render** - true to render the polygon, otherwise, false.

## bool IsPolygonRender ( int polygon )

Returns a value indicating if the polygon with the given ID is rendered.
### Arguments

- *int* **polygon** - ID of the polygon.

### Return value

true if the polygon is rendered, otherwise, false.
## int GetPolygonTextureWidth ( int polygon )

Returns the width of the polygon texture.
### Arguments

- *int* **polygon** - ID of the polygon.

### Return value

Width of the polygon texture.
## int GetPolygonTextureHeight ( int polygon )

Returns the height of the polygon texture.
### Arguments

- *int* **polygon** - ID of the polygon.

### Return value

Height of the polygon texture.
