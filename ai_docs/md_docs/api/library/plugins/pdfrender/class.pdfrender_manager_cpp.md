# Unigine::Plugins::PDFRender::Manager Class (CPP)

**Header:** #include <plugins/Unigine/PDFRender/UniginePDFRender.h>

> **Notice:** This class is a singleton.


## Manager Class

---

## PDFFile * load ( const char * path )

Loads a PDF file from the specified path.
### Arguments

- *const char ** **path** - Path to the PDF file to load.

### Return value

The loaded PDF file.
## void unload ( PDFFile * file )

Unloads the specified PDF file.
### Arguments

- *[PDFFile](../../../../api/library/plugins/pdfrender/class.pdffile_cpp.md) ** **file** - The PDF file to unload.
