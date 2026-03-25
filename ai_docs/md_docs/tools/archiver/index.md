# Archiver


Archiver is a tool for handling `UNG` files: it allows performing encryption, decryption, compression and decompression of project files, creating archives and unpacking them, and provides the statistics on UNG archives.


On Windows, using the archive instead of a big amount of project files will take significantly less time on initialization, as [Windows Defender](../../troubleshooting/antivirus/index.md#exclusion) will treat it as a single file.


For convenience, *Archiver*'s packing and compression functionality has been implemented in *[Build Tool](../../editor2/projects/build_project.md#pack_data_files)* to allow you packing the final build into a UNG archive. However, setting a password, unpacking UNG archives and checking the archive statistics and content is only possible using *Archiver*.


The contents of `UNG` archives are completely transparent to the engine: archived files are accessed using their standard paths, as if they were not packed. However, it's important to note that:


- A `UNG` archive cannot contain another `UNG` archive.
- A mount point cannot be packed into an archive, although it can reference one.
- **[Data Streaming](../../principles/data_streaming/index.md) is not supported for compressed files within archives.** An archive may contain both compressed and uncompressed files. Although compressed files in archives benefit from faster read speeds, they cannot be streamed. Therefore, by deafult, files that may be streamed remain uncompressed when the archive is created.
- Compression of binary formats (e.g. `.texture`, `.mesh` or `.lmap`) **is not recommended**, since these formats are already compressed internally and require streaming for efficient runtime loading.
- For files whose extensions are marked for compression, the **LZ4** compression algorithm is applied. The list of compressible extensions is specified at the time of archive creation.


For more information, refer to the article: **[File System](../../principles/filesystem/index_cpp.md#file_packages)**.


To invoke Archiver, run `<UnigineSDK>/bin/ung_x64.exe` (in Windows) or `<UnigineSDK>/bin/ung_x64` (in Linux) from a command-line console.


## Command Line Options


Archiver recognizes the following command-line options:


- **-p *<PASSWORD>*** - set a password. It should be the same password as passed on engine initialization on the API side. For more information refer to the article **[Protecting Your Data with a Password](../../code/data_protection_cpp.md)**. > **Notice:** You can skip password setting if it is not required. The engine supports loading UNG archives without password protection even if the password was specified on its initialization.
- **-x *<FILE>*** - exclude the specified files from packing into the archive.
- **-o *<ARCHIVE>*** - name the output archive.
- **-e *<ARCHIVE>*** - extract files from the archive.
- **-i *<ARCHIVE>*** - list all files from the archive along with their respective sizes.
- **-s *<ARCHIVE>*** - output detail information about the archive.
- **-c *<EXTENSIONS>*** - enable compression for the specified extensions. If no extensions are provided, compression will be enabled by deafult for the following extensions: `json`, `xml`, `txt`, `node`, `world`, `prop`, `track`, `mat`, `basemat`. > **Notice:** If you specify your own extensions, the default ones **will not be used**, only the extensions you explicitly list will be applied.


## Statisctics Overview


When you request statistics for an archive using the **-s *<ARCHIVE>***, the output includes both general and extension-specific statistics:


![](archive_stats.png)

*Result of runningung_x64 -s data.ung: all included file extensions are listed along with their sizes before and after the compression.*


**General Statistics:**


- ***Num files*** - Displays total number of files in archive.
- ***Size*** - Displays the original size of the archive and the compressed size.
- ***Compression diff*** - Indicates the amount of space saved by compression.
- ***Compression rate*** - Displays the compression ratio as a percentage, representing how much smaller the compressed archive is compared to the original.


**Per-Extension Statistics Table:**


- ***Extension***: The file extension (e.g. texture, json, xml).
- ***Size***: The total size occupied by files of this extension, showing the original and compressed sizes.
- ***Diff***: The total amount of space saved for this extension.
- ***Rate total***: The overall compression rate for all files with this extension.
- ***Rate average***: The average compression rate across all files of this type.
- ***Rate median***: The median compression rate, showing the most common compression outcome.
- ***Rate min***: The minimum compression rate observed for this extension.
- ***Rate max***: The maximum compression rate observed for this extension.


## Usage Examples


- The following creates an archive named `files.ung` that contains files `file.txt` and `file.tga`: ```bash ung_x64 -o files.ung file.txt file.tga ``` You can specify the name of the folder, and all files in it will be archived recursively.
- The following extracts all files from the archive created above: ```bash ung_x64 -e files.ung ```
- The following prints statistics related to the archive: ```bash ung_x64 -i files.ung ```
- The following creates an archive named `files.ung` that contains files `file.txt` and `file.tga` protected with the password "**12345**": ```bash ung_x64 -p 12345 -o files.ung file.txt file.tga ```
