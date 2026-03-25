# VCSIntegration Plugin


> **Notice:** **VCSIntegration Plugin** is available for Windows only.


**VCSIntegration Plugin** is designed to let the version control system (*Subversion, Git*) track all file changes performed in UnigineEditor. The plugin tracks all actions (with some exceptions) and processes them.


**VCSIntegration Plugin** is available for projects under version control. It has no interface and starts automatically after the Asset System is initialized and all assets are imported.


Similar to other plugins, this plugin can be loaded and unloaded via the *Editor Plugin Manager* window. When the plugin is loaded and running, it receives data about every event in the Asset System (asset or directory adding, deleting, renaming, moving, or asset editing).


> **Notice:** The plugin only manages the `/data` directory. This means that the plugin can't track changes to directories or assets outside of that directory.


For every event, a VCSIntegration executable (`svn.exe` or `git.exe`) is called and the corresponding process with the required arguments is started.


> **Notice:** For correct operation of the plugin with projects under the different version control systems, you should set up the environment. Please refer to the corresponding articles for details:
>
>
> - [Git](../../../../editor2/assets_workflow/version_control/vcs_plugin/git.md)
> - [Subversion](../../../../editor2/assets_workflow/version_control/vcs_plugin/svn.md)


## Plugin Limitations


The plugin does not provide fully-fledged integration with *Subversion* and *Git*, and it can't solve all issues. Its aim is to facilitate tracking of major content changes done by multiple developers working on the same project in the Editor and saving these changes to the repository. Therefore, be aware of the following constraints:


- The plugin only manages the `/data` directory. This means that the plugin can't track changes to directories or assets outside of that directory.
- The ***Cleaner*** tool allows deleting lost runtime files (*[Lost Runtimes](../../../../editor2/cleaner/index.md#lost_runtimes)*), but this can't be handled by *VCSIntegration Plugin*. Files deleted using this feature will have the **missing** status.
- Editor plugins run after Asset System is initialized and all assets are imported. Therefore, if project files have been added or removed before the Editor is launched, *VCSIntegration Plugin* can't track these changes upon initialization, and they will have the **non-versioned/missing** status in SVN/Git Commit.
- The plugin doesn't track changes in the mounted directories (referenced by a *mount point*).
- The plugin doesn't solve and doesn't simplify conflict solving. It only helps SVN or Git to correctly determine the file status.
- When the plugin is running, the Editor may slow down. This is caused by processing of all file interactions by SVN/Git, which is time-consuming. The more files are affected by changes, the longer the processing is. This is especially obvious when adding or removing files, in other cases processing is rather quick.


## Configuring Project for Plugin Support


To allow *VCSIntegration Plugin* to track changes on the assets via UnigineEditor, you should configure your project as follows:


1. Find your project in the UNIGINE SDK Browser and select **Other Actions -> Configure**. ![](../../../../sdk/projects/other_actions.png)
2. In the *Configure* form that opens, click the **Plugins** button and choose ***VCSIntegration Plugin*** from the list.
3. Click **Add** and then click **Configure Project**.
4. Ensure the version control system (*SVN, Git*) manages your project. Otherwise, an error message will appear when launching UnigineEditor. ![](vcs_init_failed.png)


When you run UnigineEditor, the *VCSIntegration Plugin* will automatically receive data about events in the Asset System and process them.


> **Notice:** When creating a new project, you can add the *VCSIntegration Plugin* the same way via the *Create New Project* form.


## General Plugin Workflow


From the user's point of view, the plugin operation has almost no effect on the Editor behavior - you won't observe any changes. You can delete, add, rename, edit, move, and create files and directories just the same way as you have done before, only with *VCSIntegration Plugin* tracking and processing all the changes.


The **workflow** basically is as follows:


1. Before you start, update and clean up your repository.
2. Start the Editor and work as usual (add, remove and change files and directories as you always did).
3. When finished, save the project and close the Editor. We recommend closing the Editor, as an update may be required before the commit.
4. Apply your changes to the repository. If conflicts arise, resolve them as you have done before. However, be aware that all changes made without the Editor running (via File Explorer) will have an invalid status.


## Disabling VCSIntegration Plugin


*VCSIntegration Plugin* can be disabled the same way as other plugins in the Editor:


1. Select *Windows -> Editor Plugin Manager* in the Menu Bar.
2. Find *VCSIntegration Plugin* in the list and click **Unload**. ![](vcs_plugin_manager.png)


After that, the plugin will be disabled until the Editor is restarted or the **Load** button is clicked.


To *completely disable* the plugin, you need to reconfigure the project just as you did [before](#configuration):


1. Find your project in the UNIGINE SDK Browser and select **Other Actions -> Configure**.
2. In the *Configure* form that opens, click the **Plugins** button and disable the ***VCSIntegration Plugin***.
3. Click **Add** and then click **Configure Project**.
