# UnigineScript Cache Files

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


UnigineScript can be pre-compiled into cache file in order to achieve faster initialization and for distributing final builds without revealing full script sources.


## Cache File Creation


The cache file for *system* and *editor* scripts is generated automatically (or re-generated, if checksum of the source files doesn't match the one stored in the cache) every time you start the engine.  To generate the *world* script cache file, you need to pass the cache file name as the second argument to [`world_load`](../../code/console/index.md#world_load) command as follows:


```text
Unigine~# world_load world_name cache_name
```


In the result, the `*.cache` file is created in the specified directory (or inside the `data` directory by default, if the path is not specified).


> **Notice:** You need to run the `world_load` command for each world of your project to generate the required cache files.


After the world script cache file is created, you can delete the source code from the build and still [load your world](#world_cache) by using the `world_load` command with the cache file name as the second argument.


> **Notice:** You cannot use the `*.cache` file created with the debug version to load the world with the release version of the engine.


Cache files are not compatible between different versions of the engine, so make sure that you are using the same builds of the engine.


Notice that you can cache only the source code written in UnigineScript (your `*.usc` files). To protect assets, use the [Archiver](../../tools/archiver/index.md) tool to pack them into `ZIP` or [`UNG`](../../principles/filesystem/index_cpp.md#file_packages).


## How to Use Cache Files


The engine looks for the world, system and editor cache files inside the `data` directory first. After that they are looked for according to the `cache_name` variable, where `cache_name` is the path to the cache file stored outside the `data` directory.


### World Cache File


To use the world script cache file, simply pass its name (or the path to the file, if it is stored outside the `data` directory) to [`world_load`](../../code/console/index.md#world_load) command as the second argument. The [`world_reload`](../../code/console/index.md#world_reload) console command can receive the cache file name as an argument as well:


```text
Unigine~# world_reload cache_name
```
