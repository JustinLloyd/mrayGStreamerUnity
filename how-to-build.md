# How To Build This Project #

Install Windows 10 Pro x64 1909 in VM

Install Chocolatey (chocolatey.org) to make software installation easier

After installing chocolatey:

## Install utilities from chocolatey ##
1. Open an admin prompt

        (WIN+R) cmd (CTRL+SHIFT+ENTER)

2. Install utilities from chocolatey.org

        $ choco install visualstudio2019professional (ENTER)
        $ choco install git (ENTER)
        $ choco install wget (ENTER)
        $ choco install unzip (ENTER)

3. Close the admin prompt

        $ exit (ENTER)

## Install gstreamer & dependencies walker ##
1. Open an admin prompt

        (WIN+R) cmd (CTRL+SHIFT+ENTER)
2. Install gstreamer

        $ cd %USERPROFILE%\Downloads (ENTER)
        $ wget https://gstreamer.freedesktop.org/data/pkg/windows/1.16.2/gstreamer-1.0-devel-mingw-x86_64-1.16.2.msi (ENTER)
        $ wget https://gstreamer.freedesktop.org/data/pkg/windows/1.16.2/gstreamer-1.0-mingw-x86_64-1.16.2.msi (ENTER)
        $ gstreamer-1.0-devel-mingw-x86_64-1.16.2.msi /quiet (ENTER)
        $ gstreamer-1.0-mingw-x86_64-1.16.2.msi /quiet  (ENTER)
3. Optional - install dependency checker software

        $ wget https://github.com/lucasg/Dependencies/releases/download/v1.10/Dependencies_x64_Release.zip (ENTER)
        $ unzip Dependencies_x64_Release.zip -d dependencies (ENTER)

4. Confirm we have gstreamer and it is the mingw build    

        $ rem confirm we have gstreamer and it is the mingw build
        $ dir c:\gstreamer\1.0\x86_64\libgstapp-1.0-0.dll /s/b (ENTER)
        $ rem we expect to see the following string in the command window
        $ rem c:\gstreamer\1.0\x86_64\bin\libgstapp-1.0-0.dll
5. Set environment variables necessary for gstreamer usage

        $ setx GST_SDK_PATH "C:\gstreamer\1.0\x86_64" (ENTER)
        $ setx GST_PLUGIN_PATH c:\gstreamer\1.0\x86_64\lib\gstreamer-1.0 (ENTER)
        $ setx GSTREAMER_1_0_ROOT_X86_64 c:\gstreamer\1.0\x86_64 (ENTER)

6. Install additional packages for Visual Studio 2019

        $ c:\Users\justin\AppData\Local\Temp\chocolatey\visualstudio2019professional\16.6.0.0\vs_Professional.exe --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NativeDesktop --add Microsoft.VisualStudio.Component.Windows10SDK.17763 --includeoptional --includerecommended --quiet (ENTER)
7. Close the admin prompt

        $ exit (ENTER)

## Build the project ##
1. Open a Visual Studio Command Prompt

        (WIN+R) %comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2019\Professional\Common7\Tools\VsDevCmd.bat" (ENTER)
2. Verify the gstreamer environment variables are correctly set

        $ echo %GST_SDK_PATH% (ENTER)
        $ rem we should see the following text in the command prompt
        $ rem C:\gstreamer\1.0\x86_64
3. Clone the mrayStreamUnity git repo from github

        $ cd \Users\Justin\Documents (ENTER)
        $ git clone https://github.com/mrayy/mrayGStreamerUnity.git (ENTER)
        $ cd \Users\justin\Documents\mrayGStreamerUnity\Plugin\VS (ENTER)
4. Build the project

        $ devenv GStreamerUnityPlugin.sln /build Release (ENTER)
5. Optional - confirm we have a mingw build of the mrayGstreamerUnity project by using Dependencies application    

        $ set PATH=%PATH%;c:\gstreamer\1.0\x86_64\bin (ENTER)
        $ rem confirm we have a mingw build of the mray gstreamer unity library
        $ C:\Users\justin\Documents\mrayGStreamerUnity\Plugin\VS>\users\justin\Downloads\dependencies\Dependencies.exe -modules Release64\GStreamerUnityPlugin.dll | find "gstapp" (ENTER)
        $ rem we should see the following text in the command prompt
        $ rem [Environment] libgstapp-1.0-0.dll : c:\gstreamer\1.0\x86_64\bin\libgstapp-1.0-0.dll

