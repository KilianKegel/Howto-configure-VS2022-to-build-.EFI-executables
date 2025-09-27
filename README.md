# HowTo-configure-VS2026-to-build-.EFI-executables
Step-by-step configuration to enable VS2026 to create UEFI .EFI executables

## CHECK LIST VS2026 target cross configuration  

![pic](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/PropertyPage.png)

<table>
  <tr>
    <td><b><h2>Configuration Properties</h2></b></td>
    <td><b><h2>toro-C-Library UEFI .EFI</h2></b></td>
    <td><b><h2>toro-C-Library Win64 .EXE</h2></b></td>
    <td><b><h2>Microsoft LIBCMT.lib Win64 .EXE</h2></b></td>
    </tr>
  <tr>
    <td colspan="4"><b>General</b></td>
  </tr>
  <tr>
  <td>Output Directory</td>
  <td><em>$(SolutionDir)$(Platform)\$(Configuration)\<br>or<br>$(ProjectDir)$(Platform)\$(ProjectName)\$(Configuration)\</em></td>
  <td><em>$(SolutionDir)$(Platform)\$(Configuration)\<br>or<br>$(ProjectDir)$(Platform)\$(ProjectName)\$(Configuration)\</em></td>
  <td><em>$(SolutionDir)$(Platform)\$(Configuration)\<br>or<br>$(ProjectDir)$(Platform)\$(ProjectName)\$(Configuration)\</em></td>
  </tr>

  <tr>
  <td>Intermediate Directory</td>
  <td><em>$(Platform)\$(Configuration)\</em></td>
  <td><em>$(Platform)\$(Configuration)\</em></td>
  <td><em>$(Platform)\$(Configuration)\</em></td>
  </tr>
  <tr>
    <td colspan="4"><b>Advanced</b></td>
  </tr>

  <tr>
  <td>Target File Extention</td>
  <td><em>.EFI</em></td>
  <td><em>.EXE</em></td>
  <td><em>.EXE</em></td>
  </tr>
  <tr>
  <td>Character Set</td>
  <td><em>Use Multi-Byte Character Set</em></td>
  <td><em>Use Multi-Byte Character Set</em></td>
  <td><em>Use Multi-Byte Character Set</em></td>
  </tr>
  
  <tr>
  <td>Whole Program Optimization</td>
  <td><em>No Whole Program Optimization</em></td>
  <td><em>No Whole Program Optimization</em></td>
  <td><em>No Whole Program Optimization</em></td>
  </tr>

  <tr>
    <td colspan="4"><b>C/C++\General</b></td>
  </tr>

  <tr>
  <td>SDL checks</td>
  <td><em>No (/sdl-)</em></td>
  <td><em>No (/sdl-)</em></td>
  <td><em>No (/sdl-)</em></td>
  </tr>


  <tr>
    <td colspan="4"><b>C/C++\Preprocessor</b></td>
  </tr>
  <tr>
    <td>Preprocessor Definitions</td>
    <td><em>_NO_CRT_STDIO_INLINE<br>_CRT_SECURE_NO_WARNINGS<BR><B>NOTE: Microsoft inline functions n/a in toro C Library</B></em></td>
    <td><em>_NO_CRT_STDIO_INLINE<br>_CRT_SECURE_NO_WARNINGS<BR><B>NOTE: Microsoft inline functions n/a in toro C Library</B></em></td>
    <td><em>_CRT_SECURE_NO_WARNINGS<BR><B>NOTE: <a href="https://www.open-std.org/JTC1/SC22/WG14/www/docs/n1570.pdf#PAGE=600">Bounds Checking Interface</a>  n/a in toro C Library</B></em></td>
  </tr>

  <tr>
    <td colspan="4"><b>C/C++\Code Generation</b></td>
  </tr>
  <tr>
    <td>Runtime Library</td>
    <td><em>Multi-threaded (/MT)</em></td>
    <td><em>Multi-threaded (/MT)</em></td>
    <td><em></em></td>
  </tr>
  <tr>
    <td>Struct Member Alignment</td>
    <td colspan="3">Default<br><B>NOTE: UEFI API access fails with any different setting</B></b></td>

    <td><em></em></td>
  </tr>
  <tr>
    <td>Security Check</td>
    <td><em>Disable Security Check (/GS-)</em></td>
    <td><em>Disable Security Check (/GS-)</em></td>
    <td><em></em></td>
  </tr>
  <tr>
    <td>Floating Point Model</td>
    <td><em>Strict (fp:strict)</em></td>
    <td><em>Strict (fp:strict)</em></td>
    <td><em></em></td>
  </tr>


  <tr>
    <td colspan="4"><b>Linker\General</b></td>
  </tr>
  <tr>
    <td>Output File</td>
    <td><em>$(OutDir)$(TargetName)$(TargetExt)</em></td>
    <td><em>$(OutDir)$(TargetName)$(TargetExt)</em></td>
    <td><em>$(OutDir)$(TargetName)$(TargetExt)</em></td>
  </tr>

  <tr>
    <td>Additional Library Directories</td>
    <td><em>$(SolutionDir)Lib</em></td>
    <td><em>$(SolutionDir)Lib</em></td>
    <td><em>$(SolutionDir)Lib</em></td>
  </tr>


  <tr>
    <td colspan="4"><b>Linker\Input</b></td>
  </tr>
  <tr>
    <td>Additional Dependencies</td>
    <td><em>toroC64.lib; <a href="https://github.com/KilianKegel/Visual-LIBWIN32-for-UEFI?tab=readme-ov-file#visual-libwin32-for-uefi">LibWin324UEFI.lib</a></em><br><b>NOTE:</b> uncheck <b>Inherit from parent or project defaults</b>, prevent from <b>%AdditionalDependancies</b></td>
    <td><em>toroC64.lib; kernel32.lib</em></td>
    <td><em>kernel32.lib; legacy_stdio_definitions.lib</em></td>
  </tr>
  <tr>
    <td>Ignore All Default Libraries</td>
    <td><em>Yes (/NODEFAULTLIB)</em></td>
    <td><em>Yes (/NODEFAULTLIB)</em></td>
    <td><em></em></td>
  </tr>

  <tr>
    <td colspan="4"><b>Linker\Manifest File</b></td>
  </tr>
  <tr>
    <td>Generate Manifest</td>
    <td><em>No (/MANIFEST:NO)</em></td>
    <td><em>No (/MANIFEST:NO)</em></td>
    <td><em></em></td>
  </tr>

  <tr>
    <td colspan="4"><b>Linker\System</b></td>
  </tr>
  <tr>
    <td>SubSystem</td>
    <td><em>EFI Application (/SUBSYSTEM:EFI_APPLICATION)</em></td>
    <td><em>Console (/SUBSYSTEM:CONSOLE)</em></td>
    <td><em>Console (/SUBSYSTEM:CONSOLE)</em></td>
  </tr>
  
  <tr>
    <td colspan="4"><b>Linker\Advanced</b></td>
  </tr>
  <tr>
    <td>Entry Point</td>
    <td><em>_cdeCRT0UefiShell</em></td>
    <td><em>_cdeCRT0WinNT</em></td>
    <td><em></em></td>
  </tr>
  <tr>
    <td>Randomized Base Address</td>
    <td><em>No (/DYNAMICBASE:NO)</em></td>
    <td><em></em></td>
    <td><em></em></td>
  </tr>
  <tr>
    <td>Data Execution Prevention (DEP)</td>
    <td><em>No (/NXCOMPAT:NO)</em></td>
    <td><em></em></td>
    <td><em></em></td>
  </tr>
</table>

## OPTIONAL IMPROVEMENT, SIMPLIFICATION 

Define environment value **MYUSBSHARE** to tell your **exchange drive**

![](https://github.com/KilianKegel/Howto-setup-a-UEFI-Development-PC/blob/master/envedit.png)
<table>
  <tr>
    <td><b><h2>Configuration Properties</h2></b></td>
    <td><b><h2>toro-C-Library UEFI .EFI</h2></b></td>
    <td><b><h2>toro-C-Library Win64 .EXE</h2></b></td>
    <td><b><h2>MSFT LIBCMT.lib Win64 .EXE</h2></b></td>
  </tr>
  <tr>
    <td colspan="4"><b>Build Events\Post-Build Event</b></td>
  </tr>
  <tr>
    <td>Command Line</td>
    <td colspan="3"><b>IF DEFINED MYUSBSHARE copy /y "$(OutDir)$(TargetName)$(TargetExt)" $(MYUSBSHARE) & copy /y "$(OutDir)$(TargetName)$(TargetExt)" $(ProjectDir)</b></td>
  </tr>
  <tr>
    <td>Description<</td>
    <td colspan="3"><b>copy /y "$(OutDir)$(TargetName)$(TargetExt)" $(MYUSBSHARE)</b></td>
  </tr>
  <tr>
    <td>Use In Build</td>
    <td colspan="3"><b>YES</b></td>
  </tr>


</table>

1. Get and install Visual Studio:<br>
  https://github.com/KilianKegel/HowTo-setup-an-UEFI-Development-PC#install-visual-studio-2022
2. Follow the screenshots below:<br><br>
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_1.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_2.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_3.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_4.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_5.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_6.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_7.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_8.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_9.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_10.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_11.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_12.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_13.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_14.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_15.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_16.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_17.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_18.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_19.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_20.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_21.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_22.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_23.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_24.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_25.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_26.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_27.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_28.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_29.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_30.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_31.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_34.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_35.png)
![](https://github.com/KilianKegel/Howto-configure-VS2022-to-build-.EFI-executables/blob/main/images/HOWTOCONFIGVS2022_36.png)
