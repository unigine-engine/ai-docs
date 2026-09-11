# Subversion


**Subversion (SVN)** is one of the most frequently used version control systems for content-heavy UNIGINE-based projects. **VCSIntegration Plugin** provides Subversion integration, which allows tracking changes in the project and processing them.


All tracked actions go to ***SVN Commit*** via the SVN client, where they are assigned the corresponding status. It helps users avoid manual work.


> **Notice:** Within this article, we will use ***TortoiseSVN*** as the client for Subversion.


## Setting Up Environment


For VCSIntegration Plugin to operate with Subversion correctly, you should prepare the environment:


1. Make sure the *Subversion* *client* (in our case, *[TortoiseSVN](https://tortoisesvn.net/downloads.html)*) is installed with the command-line tools. If the plugin can't locate a Subversion executable (`svn.exe` is unavailable), it will provide you with the error message. The same will be displayed in the console. In this case, modify the configuration of your SVN client. For TortoiseSVN, follow the instructions: When completed, proceed with setting up the environment.

  1. Run the SVN installer and click **Modify**.
  2. Click on the *command line client tools* icon and follow the installation instructions. ![](svn_setup.png)
2. Add the path to the `svn.exe` file to the **PATH** environment variable. You can do that as follows:

  1. Type *Advanced System Settings* in the search bar next to the **Start** button and click on the matching option. ![](advanced_settings.png)
  2. In the window that opens, click **Environment Variables...** ![](environment_variables.png)
  3. Select the system variable **PATH** from the list and click **Edit...** ![](path_edit.png)
  4. In the window that opens, click **New**, add the path, and click **OK**. For TortoiseSVN, it will be `C:\Program Files\TortoiseSVN\bin` by default.


## Limitations


In addition to [general plugin limitations](../../../../editor2/assets_workflow/version_control/vcs_plugin/index.md#limitations), there are also specific constraints for tracking changes in projects managed by SVN:


- The plugin doesn't process Unicode characters like: *"لا أدري不知道боль"*. Therefore, only use English characters, numbers or space in file and directory names. Using other characters in the file and folder names may cause changing the recursive status to **non-versioned**. However, this restriction doesn't apply to the file content.
- The plugin doesn't use the TortoiseSVN *Ignore list* - such files still are tracked. Thus be aware that if such files and the directories containing them are changed, they will be added to the *SVN Commit* list. For example, when a texture is imported to a directory added to the *Ignore list*, the plugin will process it and mark it with the **added** status instead of ignoring that texture and mark it with the **non-versioned** status. Make sure to exclude such files from the commit!


## Plugin Operation


### Adding New Asset


The user imports a new asset `humanoid_run_forward.fbx` to the directory. The new FBX asset, its metadata, and all runtime files with their metafiles will be displayed in the *SVN Commit*. All files will have the **added** status.


[![](svn_added.png)](svn_added.png)


### Renaming Asset


The user renames an asset from `PNG.png` to `ddd.png`. The texture asset and its metadata with the old name will show up as **deleted** in *SVN Commit*, the same files with the new name will be displayed as **added(+)**.


[![](svn_rename.png)](svn_rename.png)


### Moving Asset


The user moves a non-native asset `import_materials.fbx` from one directory to another. The asset and its metadata will be displayed in *SVN Commit*: the files from the old directory will have the **deleted** status, and those added to the new directory will be marked as **added(+)**.


[![](svn_replace.png)](svn_replace.png)


### Deleting Asset


The user deletes a non-native asset `humanoid_run_forward.fbx`. The asset, its metadata, and all runtime files with their metadata will have the **deleted** status within *SVN Commit*.


[![](svn_delete.png)](svn_delete.png)


### Changing Asset Import Parameters


When an asset is re-imported with new parameters, its runtime files and metadata will have the **modified** status in *SVN Commit*. The asset itself remains unchanged.


[![](svn_modified.png)](svn_modified.png)
