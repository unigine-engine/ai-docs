# Function Node


![](../img/function.png)

### Description

This node is used to write your own custom functions, you can have multiple functions inside a single node and even call one function from another.


When to use the Function node:


- to implement large functions via code;
- to copy some functions from external sources;
- if you are a programmer you got used to write code and feel uncomfortable with node-based workflow;


Please keep in mind that some functionality might be unavailable as graph nodes yet, but via code you have access to everything in UNIGINE's graphics API. See the `SDK/data/core/materials/shaders/render/common.h` for the list of common shader functions which can be used in the Function node to implement you custom functionality.


For example, there is no dedicated node that can get a random color but our Shader API offers a ***randColor(float seed)*** function, which can be used in a Function node as follows (see the image above):


```text
void getRandColor(float a, out float4 c)
{
    c = randColor(a);
}
```


## Usage Example

| [**View Fullscreen**](https://matgraph.unigine.com/DocsFunction_2.21/fullView) |
|---|
