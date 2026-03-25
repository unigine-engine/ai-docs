# Organizing Assets


You can rename your assets, move them between the folders and manage their hierarchy safely and easily using the *[Asset Browser](../../editor2/assets_workflow/index.md#asset_browser)*. You don't have to worry that your material will lose a texture when you change its name. The [Asset System](../../editor2/assets_workflow/index.md#asset_system) will track the changes and keep all links and dependencies between the resources.


## Managing Asset Browser Windows


To facilitate managing assets, you can create multiple Asset Browser windows via the menu bar: ***Windows -> Add Asset Browser*** and stack them anywhere. Each of the created windows is also listed in the *Windows* menu and can be hidden or removed, if required.


![](multiple_bro_windows.png)


Clicking on the lock sign ![](../interface/lock_sign.png) in the upper right corner of each Asset Browser window will prevent automatic switching of the [thumbnail view](../../editor2/assets_workflow/index.md#thumbnail_view) (the right side of the Asset Browser window) if an asset in another folder is selected.


## Creating and Moving Folders


Within your project, you can create as many folders as you need, including nested ones. Keeping the folder tree of your project well-structured will help to find necessary assets quickly and makes [migration of assets between projects](../../editor2/assets_workflow/assets_migration.md) easier.


> **Warning:** Do not create user folders with the following reserved names in the root of the `data/` or a mounted folder:
>
>
> - `.runtimes`
> - `.thumbnails`
> - `.cache_textures`
> - `.editor2`
> - `core`
> - `editor`
> - `editor2`
> - `scripts`
>
>
> If such a folder is created via Explorer, it won't be displayed in the Asset Browser. Inside subfolders of the data folder, no name restrictions are applied and such folders will be displayed by the Asset Browser properly.


To create a new folder right-click somewhere in the Asset Browser and choose **Create -> Create Folder**.


![](create_button.png)


To move a folder to another location within your project you can select it in the **[Hierarchy View](../../editor2/assets_workflow/index.md#hierarchy_view)** and simply drag it to the target folder.


![](folder_move.png)


To move several folders select them in the **[Thumbnail View](../../editor2/assets_workflow/index.md#thumbnail_view)** and drag to the target folder in the **[Hierarchy View](../../editor2/assets_workflow/index.md#hierarchy_view)**.


## Renaming an Asset


To rename an asset right-click the asset's icon or a thumbnail preview and choose **Rename** or select the asset and press **F2** on the keyboard, then type a new name and press **Enter**.


To rename multiple assets, you can use the *[Batch Rename](../../editor2/tools/batch_rename/index.md)* tool.


## Moving an Asset


To move an asset or a group of assets to another folder, select the asset(s) you want to move and then drag to the target folder.


![](dragndrop_asset.png)


Another way to move an asset is to right-click the asset's icon or a thumbnail preview and choose **Cut** or select the asset and press **Ctrl + X** on the keyboard. Then open the desired target folder, right-click and choose **Paste** (or press **Ctrl + V** on the keyboard).


## Copying an Asset


To copy an asset right-click the asset's icon or a thumbnail preview and choose **Copy** or select the asset and press **Ctrl + C** on the keyboard. Then open the desired target folder, right-click and choose **Paste** (or press **Ctrl + V** on the keyboard).


To duplicate an asset in the current folder, select the asset and press **Ctrl + D**.


## Replacing an Asset


To automatically replace one asset (or a group of similar ones) with another asset of the same type while keeping all references, right-click the asset's icon and choose **Replace Assets**. Then select the asset that will replace this one. All related changes are made everywhere in your project automatically, with most asset types supported, including meshes, textures, materials, properties, presets, landscape layer maps, etc.


![The Replace Assets option in the context menu](replace.png)


This option might be very useful, for example, when you want to replace certain textures in all materials with a new texture, or when building a prototype of your scene without having the final geometry yet by placing some simple blocks (proxies) to replace them with final models when they're ready.


## Deleting an Asset


To remove an asset right-click the asset's icon or a thumbnail preview and choose **Delete** or select the asset and press **Del** on the keyboard.


> **Notice:** When removing an asset in the Asset Browser, you also delete the file from the `data` folder on your computer.
