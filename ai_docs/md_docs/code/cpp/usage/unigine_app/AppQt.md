# Unigine Integration into Qt Application


This article describes the sample located in the `<UnigineSDK>/source/apps/main_qt` folder. The sample demonstrates how to create a Qt Widget and embed Unigine into it.


> **Notice:** Qt version **6.5.3** is supported.


In this sample, the Qt application controls the main loop: the engine *[iterate()](../../../../api/library/engine/class.engine_cpp.md#iterate_void)* function is called when a request to repaint all or part of a Qt widget has been received (see the *AppQt::timerEvent()* function defined in the `<UnigineSDK>/source/source/apps/main_qt/AppQt/AppQt.cpp` file).
