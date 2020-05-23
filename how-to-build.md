# How To Build This Project #

Install Windows 10 Pro x64 1909 in VM
After installing chocolatey (chocolatey.org):

(WIN+R) cmd (CTRL+SHIFT+ENTER)
$ choco install visualstudio2019professional (ENTER)
$ choco install git (ENTER)
$ choco install wget (ENTER)
$ choco install unzip (ENTER)
$ exit (ENTER)

(WIN+R) cmd (CTRL+SHIFT+ENTER)
$ cd \Users\Justin\Documents (ENTER)
$ wget https://gstreamer.freedesktop.org/data/pkg/windows/1.16.2/gstreamer-1.0-devel-mingw-x86_64-1.16.2.msi (ENTER)
$ wget https://gstreamer.freedesktop.org/data/pkg/windows/1.16.2/gstreamer-1.0-mingw-x86_64-1.16.2.msi (ENTER)
$ wget https://github.com/lucasg/Dependencies/releases/download/v1.10/Dependencies_x64_Release.zip (ENTER)
$ unzip Dependencies_x64_Release.zip -d dependencies (ENTER)
$ gstreamer-1.0-devel-mingw-x86_64-1.16.2.msi /quiet (ENTER)
$ gstreamer-1.0-mingw-x86_64-1.16.2.msi /quiet  (ENTER)
$ rem confirm we have gstreamer and it is the mingw build
$ dir c:\gstreamer\1.0\x86_64\libgstapp-1.0-0.dll /s/b (ENTER)
c:\gstreamer\1.0\x86_64\bin\libgstapp-1.0-0.dll
$ setx GST_SDK_PATH "C:\gstreamer\1.0\x86_64" (ENTER)
$ setx GST_PLUGIN_PATH c:\gstreamer\1.0\x86_64\lib\gstreamer-1.0 (ENTER)
$ setx GSTREAMER_1_0_ROOT_X86_64 c:\gstreamer\1.0\x86_64 (ENTER)
$ c:\Users\justin\AppData\Local\Temp\chocolatey\visualstudio2019professional\16.6.0.0\vs_Professional.exe --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NativeDesktop --add Microsoft.VisualStudio.Component.Windows10SDK.17763 --includeoptional --includerecommended --quiet (ENTER)
$ exit (ENTER)

(WIN+R) %comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2019\Professional\Common7\Tools\VsDevCmd.bat" (ENTER)
$ echo %GST_SDK_PATH% (ENTER)
C:\gstreamer\1.0\x86_64
$ cd \Users\Justin\Documents (ENTER)
$ git clone https://github.com/mrayy/mrayGStreamerUnity.git (ENTER)
$ cd \Users\justin\Documents\mrayGStreamerUnity\Plugin\VS (ENTER)
$ devenv GStreamerUnityPlugin.sln /build Release (ENTER)
$ set PATH=%PATH%;c:\gstreamer\1.0\x86_64\bin (ENTER)
$ rem confirm we have a mingw build of the mray gstreamer unity library
$ C:\Users\justin\Documents\mrayGStreamerUnity\Plugin\VS>\users\justin\Downloads\dependencies\Dependencies.exe -modules Release64\GStreamerUnityPlugin.dll | find "gstapp" (ENTER)
[Environment] libgstapp-1.0-0.dll : c:\gstreamer\1.0\x86_64\bin\libgstapp-1.0-0.dll
