# Upgrading Assets


According to the standard workflow, content of the project is [migrated](../../upgrade/migration_content/index.md) to the newest version automatically via UNIGINE *[SDK Browser](../../sdk/index.md)* or manually using the upgrade script.


However, you can add non-migrated assets to the upgraded project via UnigineEditor, as it allows upgrading assets to the current version of UNIGINE SDK. An outdated asset is upgraded in the following cases:


- When importing an asset via the *Asset Browser*.
- When importing a package with an asset.
- When copying an asset to the project's `data` folder. If UnigineEditor is launched, the asset will be upgraded on the fly. > **Notice:** If UnigineEditor is not running, the asset will be upgraded on the next launch.


To toggle upgrading on and off and specify the migration folder, go to the *[Editor](../../editor2/settings/hotkeys/index.md)* section of the *Settings* window:


![](upgrade_enabled.png)


The *Migration Directory* is a temporary folder for the outdated assets: they are copied into this folder and processed by the upgrade script. Then the upgraded assets replace the original ones.


### Upgrading Mounted Assets


The only way to upgrade the mounted assets (i.e. referenced by a [mount point](../../principles/filesystem/index_cpp.md#mount_points)) via UnigineEditor is to add the mount point to the project when the editor is off. In this case, the assets will be upgraded on the next launch. However, we recommend you to upgrade assets inside mount points [manually by using the `upgrade.usc` script](../../upgrade/migration_content/index.md#manual_upgrade).


> **Notice:** If a folder contains an outdated asset, UnigineEditor won't allow you to create a mount point.
