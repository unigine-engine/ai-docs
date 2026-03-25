# Upgrade Script


UNIGINE upgrade script is a one-touch solution to upgrade data of a UNIGINE-based project to be consistent with updated engine builds.


The script recursively scans the project folders inside the `data` folder to upgrade the files located there. If the script fails to upgrade some files, it will generate an error log (`errors.log` file).


> **Notice:** The same upgrade script is run when upgrading projects via [UNIGINE SDK Browser](../../sdk/projects/index_cpp.md#upgrade_project).


## Usage


The script is located in `utils/upgrade` directory of UNIGINE SDK.


> **Notice:** You need to properly set the [development environment](../../code/environment/index.md) to get the script working.


To invoke the upgrade script, run `upgrade.usc` at the command prompt by using *[USC Interpreter](../../tools/usc/index.md)*:


```bash
usc_x* upgrade.usc DIRS OPTIONS
```


- If the content to be upgraded is stored only in the project's `data` folder, specify the path to this folder: ```bash usc_x* upgrade.usc PATH_TO_DATA OPTIONS ``` You can also specify only a particular folder inside the `data` folder, if necessary.
- If the content to be upgraded is stored [outside the `data` folder](../../principles/filesystem/index_cpp.md#mount_points), you can specify the corresponding folders for the upgrade script: ```bash usc_x* upgrade.usc DIR_0 DIR_1 OPTIONS ```


> **Notice:** If you need to upgrade several projects, you should run the upgrade script for each of them separately.


## Command Line Options


The upgrade script recognizes the following command line options:


- **--log** - a path to the log file. If the option isn't specified, the log will be printed to the command prompt only.


If no options are set, the script will start upgrading with the default values.


## Examples


- To upgrade content of a UNIGINE-based project located in `D:\my_project` directory, type at the command prompt: ```bash usc_x64 upgrade.usc D:\my_project\data ```
- To run content upgrading of a UNIGINE-based project and save the log data into a file, run the upgrade script as follows: ```bash usc_x64 upgrade.usc  D:\my_project\data --log D:\my_project\log.html ```
