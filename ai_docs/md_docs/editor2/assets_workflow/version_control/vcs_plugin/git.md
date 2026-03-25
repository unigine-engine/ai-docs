# Git


The **VCSIntegration Plugin** provides Git integration. It tracks changes made to assets in UnigineEditor and updates their statues in the repository automatically via the Git client.


> **Notice:** Within this article, we will use ***TortoiseGit*** as the client for Git. The plugin supports integration with **TortoiseGit 2.10** and later.


## Setting Up Environment


For *VCSIntegration Plugin* to operate with Git correctly, you should prepare the environment:


1. Make sure ***[git](https://git-scm.com/download/win)*** and ***[git-lfs](https://git-lfs.com/)*** are installed on your computer. If the plugin can't locate a Git executable (`git.exe` is unavailable), it will provide you with the error message. The same will be displayed in the console. In this case, install the client and proceed with setting up the environment.
2. Add the path to the `git.exe` file to the **PATH** environment variable. You can do that as follows:

  1. Type *Advanced System Settings* in the search bar next to the **Start** button and click on the matching option. ![](advanced_settings.png)
  2. In the window that opens, click **Environment Variables...** ![](environment_variables.png)
  3. Select the system variable **PATH** from the list and click **Edit...** ![](path_edit.png)
  4. In the window that opens, click **New**, add the path, and click **OK**. By default, it will be `C:\Program Files\Git\cmd`. ![](git_env_variable.png)


Now you can [configure your project to use the VCSIntegration plugin](../../../../editor2/assets_workflow/version_control/vcs_plugin/index.md#configuration) and allow tracking changes.


## Plugin Operation


### Adding New Asset


The user imports a new asset `pedestal.fbx` to the `data` directory. The new FBX asset, its metadata, and all runtime files with their metafiles will be displayed in the *Git Commit*. All files will have the **Added** status.


[![](git_added.png)](git_added.png)


### Renaming Asset


The user renames an asset from `cube.png` to `sphere.png`. The texture asset and its metadata with the new name will show up as **Renamed** in *Git Commit*. The previous names of the files will be displayed in the parentheses right after the new names.


The status of the runtime file metadata will be set as **Modified**.


[![](git_rename.png)](git_rename.png)


### Moving Asset


The user moves a non-native asset `helicopter_simple.fbx` from one directory to another. The asset and its metadata added to the new directory will be displayed in Git Commit with the **Renamed** status. The previous paths to the files will be displayed in the parentheses right after the new paths.


[![](git_moved.png)](git_moved.png)


### Deleting Asset


The user deletes a non-native asset `helicopter_simple.fbx`. The asset, its metadata, and all runtime files with their metadata will have the **Deleted** status within *Git Commit*.


[![](git_delete.png)](git_delete.png)


### Changing Asset Import Parameters


When an asset is re-imported with new parameters, its runtime files and metadata will have the **Modified** status in *Git Commit*. The asset itself remains unchanged.


[![](git_modified.png)](git_modified.png)
