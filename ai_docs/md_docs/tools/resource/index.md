# Resource


**Resource** is a tool for compiling binary resources (`*.resource` files, zipped and encoded to base64), which then will be embedded during compilation of the binary executable.


To invoke the *Resource* tool, run `resource_*` from a command-line (the `x64` postfix) and specify all the required resources.


### See Also


- [Resource](../../api/library/common/class.resource_cpp.md) class


## Command Line Options


The Resource tool recognizes the following command-line options:


- **-o *NAME*** - name of the output file. ```bash D:\UnigineSDK\bin>resource_x64 icon1.ico -o icon ``` As a result, the `icon` file will be created.


## Usage


- If you run the *Resource* tool without the **-o** option, the `*.resource` file named after the source file will be created. For example: ```bash D:\UnigineSDK\bin>resource_x64 icon1.ico ``` The `icon1.resource` file is created.
- If you specify several resources to be compiled without the **-o** option, several `*.resource` files named after the source files will be created. For example: ```bash D:\UnigineSDK\bin>resource_x64 icon1.ico splash.png ``` Two files `icon1.resource` and `splash.resource` are created.
- If you specify the **-o** option, all specified resources will be added to one file. For example: ```bash D:\UnigineSDK\bin>resource_x64 icon1.ico splash.png -o images.resource ```


> **Notice:** To load data from a `*.resource` file, use methods of the [Resource](../../api/library/common/class.resource_cpp.md) class.


## Encrypting Password


To encrypt a password by using the *Resource* tool, perform the following:


1. Create a text file named `password` that contains your password. For example, you can create such file via the command prompt: ```bash D:\UnigineSDK\bin>echo MyPassword > password ``` If the file already exists, its content will be overwritten with the given one (in this case, *MyPassword*).
2. Run `<UnigineSDK>/bin/resource_*` (with the `x64` postfix) for the password file. For example: ```bash D:\UnigineSDK\bin>resource_x64 password ```


As a result, the `password.resource` file that contains the encrypted password will be created.


To rebuild the engine with the password, copy this file to `<UnigineSDK>/source/engine` directory. Note that the password should be the same as the one that is entered when creating a UNG archive.
