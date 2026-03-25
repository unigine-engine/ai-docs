# Unigine::Plugins::PDFRender::Manager Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


## Manager Class

---

## PDFFile load ( string path )

Loads a PDF file from the specified path.
### Arguments

- *string* **path** - Path to the PDF file to load.

### Return value

The loaded PDF file.
## void unload ( PDFFile * file )

Unloads the specified PDF file.
### Arguments

- *[PDFFile](../../../../api/library/plugins/pdfrender/class.pdffile_usc.md) ** **file** - The PDF file to unload.
