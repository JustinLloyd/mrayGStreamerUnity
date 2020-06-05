# How To Build This Project #

Install Windows 10 Pro x64 1909 in VM

Install Chocolatey (chocolatey.org) to make software installation easier

After installing chocolatey:

## Install utilities from chocolatey ##
1. Open an admin prompt  
<kbd>WIN</kbd>+<kbd>R</kbd><code>cmd</code><kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>ENTER</kbd>  
2. Install utilities from chocolatey.org  
<code>$ choco install visualstudio2019professional</code><kbd>ENTER</kbd>  
<code>$ choco install git</code><kbd>ENTER</kbd>  
<code>$ choco install wget</code><kbd>ENTER</kbd>  
<code>$ choco install unzip</code><kbd>ENTER</kbd>  
3. Close the admin prompt  
<code>$ exit</code><kbd>ENTER</kbd>  


## Install gstreamer & dependencies walker ##
1. Open an admin prompt  
<kbd>WIN</kbd>+<kbd>R</kbd><code>cmd</code><kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>ENTER</kbd>
2. Install gstreamer  
<code>$ cd %USERPROFILE%\Downloads (ENTER)
<code>$ wget https://gstreamer.freedesktop.org/data/pkg/windows/1.16.2/gstreamer-1.0-devel-mingw-x86_64-1.16.2.msi (ENTER)
<code>$ wget https://gstreamer.freedesktop.org/data/pkg/windows/1.16.2/gstreamer-1.0-mingw-x86_64-1.16.2.msi (ENTER)
<code>$ gstreamer-1.0-devel-mingw-x86_64-1.16.2.msi /quiet (ENTER)
<code>$ gstreamer-1.0-mingw-x86_64-1.16.2.msi /quiet  (ENTER)
3. Optional - install dependency checker software  
<code>$ wget https://github.com/lucasg/Dependencies/releases/download/v1.10/Dependencies_x64_Release.zip (ENTER)
<code>$ unzip Dependencies_x64_Release.zip -d dependencies (ENTER)

4. Confirm we have gstreamer and it is the mingw build  
<code>$ rem confirm we have gstreamer and it is the mingw build</code><kbd>ENTER</kbd>  
<code>$ dir c:\gstreamer\1.0\x86_64\libgstapp-1.0-0.dll /s/b</code><kbd>ENTER</kbd>  
<code>$ rem we expect to see the following string in the command window</code><kbd>ENTER</kbd>  
<code>$ rem c:\gstreamer\1.0\x86_64\bin\libgstapp-1.0-0.dll</code><kbd>ENTER</kbd>  
5. Set environment variables necessary for gstreamer usage  
<code>$ setx GST_SDK_PATH "C:\gstreamer\1.0\x86_64"</code><kbd>ENTER</kbd>  
<code>$ setx GST_PLUGIN_PATH c:\gstreamer\1.0\x86_64\lib\gstreamer-1.0</code><kbd>ENTER</kbd>  
<code>$ setx GSTREAMER_1_0_ROOT_X86_64 c:\gstreamer\1.0\x86_64</code><kbd>ENTER</kbd>  
6. Install additional packages for Visual Studio 2019  
<code>$ c:\Users\justin\AppData\Local\Temp\chocolatey\visualstudio2019professional\16.6.0.0\vs_Professional.exe --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NativeDesktop --add Microsoft.VisualStudio.Component.Windows10SDK.17763 --includeoptional --includerecommended --quiet</code><kbd>ENTER</kbd>  
7. Close the admin prompt  
<code>$ exit</code><kbd>ENTER</kbd>  

## Build the project ##
1. Open a Visual Studio Command Prompt  
<kbd>WIN</kbd>+<kbd>R</kbd><code>%comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2019\Professional\Common7\Tools\VsDevCmd.bat"</code><kbd>ENTER</kbd>  

2. Verify the gstreamer environment variables are correctly set  
<code>$ echo %GST_SDK_PATH%</code><kbd>ENTER</kbd>  
<code>$ rem we should see the following text in the command prompt</code><kbd>ENTER</kbd>  
<code>$ rem C:\gstreamer\1.0\x86_64</code><kbd>ENTER</kbd>  
3. Clone the mrayStreamUnity git repo from github  
<code>$ cd %USERPROFILE%\Documents</code><kbd>ENTER</kbd>  
<code>$ git clone https://github.com/mrayy/mrayGStreamerUnity.git</code><kbd>ENTER</kbd>  
<code>$ cd \Users\justin\Documents\mrayGStreamerUnity\Plugin\VS</code><kbd>ENTER</kbd>  
4. Build the project  
<code>$ devenv GStreamerUnityPlugin.sln /build Release</code><kbd>ENTER</kbd>  
        
5. Optional - confirm we have a mingw build of the mrayGstreamerUnity project by using Dependencies application  
<code>$ set PATH=%PATH%;c:\gstreamer\1.0\x86_64\bin</code><kbd>ENTER</kbd>  
<code>$ %USERPROFILE%\Downloads\dependencies\Dependencies.exe -modules Release64\GStreamerUnityPlugin.dll | find "gstapp"</code><kbd>ENTER</kbd>  
<code>$ rem we should see the following text in the command prompt</code><kbd>ENTER</kbd>  
<code>$ rem [Environment] libgstapp-1.0-0.dll : c:\gstreamer\1.0\x86_64\bin\libgstapp-1.0-0.dll</code><kbd>ENTER</kbd>  

