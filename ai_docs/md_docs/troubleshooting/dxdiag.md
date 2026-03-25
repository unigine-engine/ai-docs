# How to Make a DirectX Diagnostic (DxDiag) Report


***DxDiag (DirectX Diagnostic)*** is a tool that comes with the Windows operating system. It shows technical information about the software on your computer. Our Support team uses this to help fix technical issues, it helps us:


- Identify the version of DirectX installed on your system.
- Verify that your graphics and audio drivers are properly installed.
- Review hardware information (GPU, CPU, memory, etc.).
- Detect errors that might affect application stability or startup.


## Step by Step Instructions


Use the following steps to generate a **DxDiag** report:


1. On Windows right-click your **Start** button and choose **Run** (or press and hold your **Windows** key on your keyboard, then press R.
2. In the **Run** window that opens type **dxdiag**, then press **Enter** or click **Ok**. ![](run_window.png) > **Notice:** If a pop-up window asks you about digital driver signing; click **Yes** to proceed.
3. **DxDiag** will automatically begin collecting system information. Wait until the progress bar at the bottom of the window disappears before continuing. ![](dxdiag_window.png)
4. Click **Save all information**.
5. It will ask you to create a new text file to save the logged information. Leave the name as `DxDiag.txt`, but take note of where the file is to be saved, then click **Save**.
6. After saving the file click **Exit**.


Please attach the `DxDiag.txt` file on your desktop to your Support Ticket or forum post. **Please do not ZIP or RAR your files.**


## Investigate DXDiag Report Yourself


If your application or Editor crashes (or doesn't start), open the **DxDiag** report and scroll down to the very bottom. Thr last 10 or so application crashes will often be listed in this file. Reading these error messages often provides valuable insights into what caused the crash. You can try Googling the error message to get more information.
