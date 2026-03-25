# PDFRender Plugin


The **PDFRender** plugin allows you to import and display PDF files directly within your UNIGINE scenes. The loaded PDF is rendered into an *[Image](../../../api/library/common/class.image_cpp.md)* object with specified parameters, which can then be used in various scenarios - e.g., on shared boards during VR meetings or presentations.


![](pdfrender.png)

*PDFRenderplugin (Widget PDF Sim Sample).*


### See Also


- *[PDFRender Plugin](../../../api/library/plugins/pdfrender/index.md)* classes
- Samples in **C++ SIM Samples** set: Samples in **C# SIM Samples** set:

  -
  -

  -
  -


## Launching PDFRender


To use the plugin, specify the `extern_plugin` command line option on the start-up:


```bash
main_x64d -extern_plugin "PDFRender"
```
