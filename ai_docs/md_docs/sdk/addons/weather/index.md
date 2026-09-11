# Weather Add-on


![](index.png)


> **Warning:** This add-on is no longer developed: no new features or fixes are planned for it. It runs on Windows with DirectX 12 only and is compatible only with projects that use [double-precision coordinates](../../../sdk/projects/index_cpp.md#precision).


The *Weather* add-on provides a set of ready-to-use sample weather effects:


- Raindrops, streaks and splashes
- Windshield wiper effect
- Lightning strikes
- Snowfall effect with wet flakes landing on the camera lens
- 3 types of screen frost effect with adjustable intensity
- Volume fog


![](index.gif)


## Opening the World


To open the world containing weather effects:


- Download the *Weather* add-on from [Add-On Store](https://store.unigine.com/).
- Add the downloaded add-on (UPACKAGE file) to your project by dragging it into the project `data/` folder in the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)*. In the *Import Package* window that opens, click the *Import Package* button and wait until the add-on contents are imported.
- In UnigineEditor, click *File -> Open World* (**Ctrl + O**) or open the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)* window. The `weather_samples.world` file is available in the `data/` directory.


> **Notice:** Node references to weather effects are located in the `data/UnigineWeather/fx/` directory.


The add-on requires the *UnigineWeather* plugin, which can be added using the following command-line option on the application start-up:


```bash
-extern_plugin UnigineWeather
```


> **Notice:** The plugin can be run on Windows only.
