# Cleaner


While working with a project, you create, copy, move, inherit, rename, and delete assets. As a result, an enormous amount of unnecessary files can be created.


**Cleaner** is a tool used to optimize your project and save disk space by deleting assets that won�t later be used in the final build. *Cleaner* also checks for corrupted references to assets.


> **Notice:** - *Cleaner* checks only the file types that are considered [assets](../../editor2/assets_workflow/asset_types.md) in terms of UNIGINE. For custom file types to be checked, add the extensions in the [Editor project settings](../../editor2/settings/hotkeys/index.md#user_extensions).
> - To learn how to use the tool, watch [this video tutorial](#video_tutorial).


## Tool Overview


*Cleaner* checks each asset that your project contains and displays irregularly used assets.


To open the *Cleaner* window, choose *Tools -> Cleaner* on the Menu Bar of UnigineEditor.


![](open_cleaner.png)


The *Cleaner* window will open:


![](cleaner_window.png)


### Unused Assets


This tab displays the assets that are **not used in any of the files** included in your project (worlds, layers, nodes, meshes, materials) and **not referenced from code** in any of your source files stored in your project `source/` folder, but still exist in the project.


![Unused Assets Tab](unused_assets.png)


*Cleaner* shows the file name and asset type for unused assets. As you click an unused asset in *Cleaner*, it is displayed in the Asset Browser and the *Parameters* window.
You can delete any or all of the displayed assets by using the *Cleaner* functionality.


The *Unused Assets* list also includes all assets that were referenced from the unused assets.


- **Delete Selected** � deletes only the selected assets from the list of unused assets. This option is also available by right-clicking the selected files in *Cleaner*.
- **Delete Listed** � deletes the whole list of currently displayed assets. > **Warning:** Use delete buttons carefully. Deleted assets cannot be restored.
- **Show Ignore List...** � displays the ignore list that already contains the default list of wildcards (e.g., *"*.jpg", "some_folder_*/", "dir*/*1*.world", "editor_[1-9]*.log"* etc. - [read more about wildcards](../../principles/filesystem/wildcards.md)) used to exclude files from the check by *Cleaner*. This list can be extended by the user. > **Warning:** If a filename in your project is generated in code (for example, a string concatenated from several words), add such cases to the Ignore List. Otherwise, such files will be deleted. ![](ignore_list.png) Upon clicking the **Check** button, all project files to be ignored by *Cleaner* are displayed in the bottom part of the *Ignore List* window.


### Lost Assets


This tab displays the assets referenced to by GUID but are not available in the project.


![Lost Assets Tab](lost_assets.png)


As you click a lost asset, the asset containing a reference to it, is displayed in the Asset Browser and the *Parameters* window. Fixing of lost assets is possible only manually.


The table in the *Lost Assets* tab has three columns:


- *Lost Asset* � shows the GUID of the lost asset.
- *Asset File* � shows the name of the file containing the reference to the lost asset.
- *Node Name* � shows the name of the node, if the file containing the reference includes the node that actually has a reference to the lost asset.


### Lost Runtimes


This tab displays the runtime files generated for the assets that are not available in the project, but referenced by a node/nodes in the scene.


![Lost Runtimes Tab](lost_runtimes.png)


The table in the *Lost Runtimes* tab has three columns:


- *Runtime Path* � shows the path to the lost runtime file.
- *Asset* � shows the name of the file containing the reference to the asset, for which the lost runtime file was generated.
- *Node Name* � shows the name of the node, if the file containing the reference includes the node that actually has a reference to the asset, for which the lost runtime file was generated.


Lost runtimes are managed using the buttons available on the tab. The buttons are the same as for the Unused Assets:


- **Delete Selected** � deletes only the selected runtimes from the list of unused runtimes. This option is also available by right-clicking the selected files in *Cleaner*.
- **Delete Listed** � deletes the whole list of currently displayed runtimes. > **Warning:** Use delete buttons carefully. Deleted files cannot be restored.


### Similar Assets


This tab displays groups containing images with a high degree of visual similarity. You may want to find and delete extra images to save more space in your project.


![Similar Assets Tab](similar_assets.png)


| Directory | Directory that contains the assets to be compared. |
|---|---|
| Similarity Threshold | The extent of visual similarity based on which similar images are grouped. |
| Preview Resolution | Resolution of the image preview that will be used as the basis for comparison. |
| Resolution of Compared Images | Resolution of other image previews that will be compared with the basis. |
| Similarity | The minimum percentage of similarity between all selected images. |


After you click the *Refresh* button, the comparison process will start. The result of this process will be displayed as the list of groups, each group containing images with a visual similarity exceeding the *Similarity Threshold* value. Files can be managed via the [context menu](../../editor2/interface/context/index.md) available by right-clicking on the file in the list.


### Console Info


Information on time spent to complete the *Cleaner* processes can be printed to the *[console](../../code/console/index.md)* and the *log file*: you just need to set the **`UNIGINE_EDITOR_TIME_TRACE`** environment variable.


![](cleaner_time_trace.png)


## Recommended Workflow


1. Click **Refresh** to check the project for lost and unused assets. You can narrow the search scope by specifying a directory in the **Directory** field: *Cleaner* will display and manage the lost and unused assets from the specified directory only. To see results after setting ![](set.png) (or resetting ![](reset.png)) the directory, click **Refresh** once again. After analyzing assets in your project, *Cleaner* shows the details.
2. Manage unused assets using the buttons available on the [Unused Assets tab](#unused_assets). > **Warning:** Use delete buttons carefully. Deleted assets cannot be restored.
3. Click **Refresh** to update the list. Deleting unused assets can reduce the number of lost assets.
4. Fix [Lost Assets](#lost_assets). Fixing of lost assets is possible only manually � by checking each asset displayed in the second or third column.
5. Manage [Lost Runtimes](#lost_runtimes) using the buttons available on the tab. The buttons are the same as for the Unused Assets. > **Warning:** Use delete buttons carefully. Deleted files cannot be restored.
6. Search for the [similar assets](#similar_assets) in your project and consider if one and the same asset can be used instead of several.


## Video Tutorial


Watch the video below to learn how to delete unused assets with the *Cleaner* tool.
