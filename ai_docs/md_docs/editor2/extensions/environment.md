# Setting Up Environment to Develop Editor Plugins


This article describes the process of configuring development environment required to develop plugins for UnigineEditor depending on your operating system.


> **Warning:** This feature is an experimental one and is not recommended for production use.


UnigineEditor is an application written entirely in C++ relying a lot on the Qt6 framework infrastructure. So, in order to extend its functionality not only C++ programming skills are required, but you should also be familiar with the Qt6 framework, CMake build system.


> **Notice:** *Qt Framework* version **6.5.3** is required to develop plugins for UnigineEditor.


## Windows Environment


The following actions are to be performed to prepare your environment on Windows:


1. Download an online installer for the **Qt open-source 6.5.3** from the official web-site **[for Windows](https://www.qt.io/download-qt-installer-oss)** operating system.
2. Run the installer and click **Next** in the window that opens.
3. To start the installation process you will need to enter you Qt account credentials (if you already have an account), or you can **Sign-up** for a new account right in the installer by filling the fields offered, accepting the service terms and clicking **Next**. [![](qt_install_register.png)](qt_install_register.png)
4. If you create a new account, you'll have to confirm your email before proceeding to the next step, so check your inbox for the new email verification message from the *Qt Company* and click verification link provided.
5. After clicking the link you will be redirected to your Qt account at **https://login.qt.io/login** and prompted to fill other required fields and click **Confirm**.
6. As you confirm you may return to your offline installer and click **Next**, the welcome message shall be displayed, click **Next** again and the installation process shall continue.
7. Read and confirm that you accept Qt Open Source Obligations and click **Next** to continue the installation process.
8. At the next stage specify installation directory, select the *Desktop Development* package, check *Custom Installation*, and click **Next** to proceed to the components selection stage. [![](qt_install_select_custom.png)](qt_install_select_custom.png)
9. Select Components to be installed. [![](qt_install_customize.png)](qt_install_customize.png) > **Notice:** Be sure to check the **MSVC2019 64bit** compiler option. The *Sources* component is optional, so tick it only if you need to browse through the Qt source code. In case you don't see the **Qt 6.5.3** version, choose the ***Show -> Archive*** option from the dropdown in the top-right corner. ![](archive_option.png)
10. Read and confirm that you accept the License agreement and click **Next** to continue the installation process. [![](qt_install_license.png)](qt_install_license.png)
11. After successful installation of the Qt Framework 6.5.3 you should add a new environment variable named `UNIGINE_QT653ROOT` and set its value so that it points to the folder, where the **MSVC2019 64bit** compiler kit is located. On Windows the path should be as follows: `<YOUR_QT_INSTALLATION FOLDER>\6.5.3\msvc2019_64`. In our case, for example, `"C:\Qt\Qt6.5.3\6.5.3\msvc2019_64"` > **Notice:** If you're using CMake, it's enough to have a path to **Qt6.5.3** installation directory in the **PATH** variable.

  1. Open **Control Panel → System** and select **Advanced System Settings**
  2. Follow the instructions given in the picture below. [![](add_variable_win.png)](add_variable_win.png)
  3. Click **OK** and close the **Control Panel**.
12. Restart your IDE, so that the information on environmental variables is updated.
13. Now you are ready to start developing your first plugin for UnigineEditor!


## Linux Environment


The following actions are to be performed to prepare your environment on Linux:


1. Download an online installer for the **Qt open-source 6.5.3** from the official web-site **[for Linux](https://www.qt.io/download-qt-installer-oss)** operating system.
2. Run the installer and click **Next** in the window that opens.
3. To start the installation process you will need to enter you Qt account credentials (if you already have an account), or you can **Sign-up** for a new account right in the installer by filling the fields offered, accepting the service terms and clicking **Next**. [![](qt_install_register_linux.png)](qt_install_register_linux.png)
4. If you create a new account, you'll have to confirm your email before proceeding to the next step, so check your inbox for the new email verification message from the *Qt Company* and click verification link provided.
5. After clicking the link you will be redirected to your Qt account at **https://login.qt.io/login** and prompted to fill other required fields and click **Confirm**.
6. As you confirm you may return to your offline installer and click **Next**, the welcome message shall be displayed, click **Next** again and the installation process shall continue.
7. Read and confirm that you accept Qt Open Source Obligations and click **Next** to continue the installation process.
8. At the next stage specify installation directory, select the *Desktop Development* package, check *Custom Installation*, and click **Next** to proceed to the components selection stage. [![](qt_install_select_custom_linux.png)](qt_install_select_custom_linux.png)
9. Select Components to be installed. [![](select_components_linux.png)](select_components_linux.png) > **Notice:** Be sure to check the **Desktop** option (*GCC 64bit* compiler). The *Sources* component is optional, so tick it only if you need to browse through the Qt source code. In case you don't see the **Qt 6.5.3** version, choose the ***Show -> Archive*** option from the dropdown in the top-right corner. ![](archive_option_linux.png)
10. Read and confirm that you accept the License agreement and click **Next** to continue the installation process. [![](qt_install_license_linux.png)](qt_install_license_linux.png)
11. After successful installation of the Qt Framework 6.5.3 you should add a new environment variable named `UNIGINE_QT653ROOT` and set its value so that it points to the folder, where the **GCC 64bit** compiler kit is located. > **Notice:** If you're using CMake, it's enough adding a path to **Qt6.5.3** installation directory to **$PATH**. On Linux the path should be as follows: `<YOUR_QT_INSTALLATION FOLDER>/6.5.3/gcc_64`. > **Notice:** Adding the environment variable to a user's bash profile alone will not export it automatically, the variable will be exported the next time the user logs in. To immediately apply all changes to bash_profile, use the source command. > > > ```bash > source ~/.bash_profile > ```

  1. Open the current user's profile into a text Editor ```bash vi ~/.bash_profile ```
  2. Add the export command for your environment variable. ```bash export UNIGINE_QT653ROOT=<YOUR_QT_INSTALLATION FOLDER>/6.5.3/gcc_64 ```
  3. Save your changes.
12. Now you are ready to start developing your first plugin for UnigineEditor!
