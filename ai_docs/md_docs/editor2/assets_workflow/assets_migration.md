# Copying Assets From Other Projects


Assets used in one UNIGINE project, both simple and composite (e.g. a material requiring a texture, or a node that requires several materials linked to plenty of textures), can be easily copied to another project using Packages.


**Package** is a collection of files and data for UNIGINE projects stored in a single `*.upackage` file. A Package compresses data while preserving the original directory structure. Packages can be used to conveniently transfer content between your projects or exchange data with other users, be it a single model or a scene with a set of objects driven by logic implemented via [C# components](../../principles/component_system/index.md).


**To copy your assets from one project to another**:


1. Open your source project in UnigineEditor and [export all necessary assets as a package file](../../editor2/managing_packages/index.md#export).
2. Open your target project that requires those assets in UnigineEditor and [import your package](../../editor2/managing_packages/index.md#import).


### See Also


Video tutorial [How To Transfer Assets to Another Project](../../videotutorials/how_to/how_to_basics/transfer_assets.md)
