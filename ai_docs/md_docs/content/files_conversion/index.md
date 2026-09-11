# Art Assets Conversion


UNIGINE provides *automatic conversion* of art assets via [UnigineEditor](../../editor2/index.md): when you import a file of a type [supported by the UNIGINE asset system](../../editor2/assets_workflow/asset_types.md), all required files in the native formats are generated.


To learn more on automatic assets conversion, read the [Asset Types](../../editor2/assets_workflow/asset_types.md) and [Assets and Runtime Files](../../editor2/assets_workflow/assets_runtimes.md) articles.


> **Notice:** We recommend you to use automatic conversion, as it is the simplest way to get assets in native formats.


UNIGINE [Import System](../../principles/import_system/index_cpp.md) that allows importing art assets of external formats offers importing assets of the `.fbx`, `.obj`, `.dae` and `.3ds` formats out-of-the-box. The Import System is customizable: you implement a [custom import plugin](../../code/usage/custom_import_plugin/index.md) that imports art assets in specific formats (not supported by UNIGINE out-of-the-box). So, automatic conversion isn't limited only to the supported formats.
