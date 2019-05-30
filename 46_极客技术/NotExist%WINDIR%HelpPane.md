### 绿化和卸载
```
@echo off
:CheckAdmin
if not exist %WINDIR%\HelpPane.exe goto Main
title 检查是否以管理员身份运行
setlocal EnableDELAYEDEXPANSION
set UAC=0
for /f "usebackq delims==" %%i in (`tasklist /fi "WINDOWTITLE eq 管理员:  检查是否以管理员身份运行"`) do (
set "cmdline=%%i"
set "cmdline=!cmdline:~0,7!"
if "!cmdline!" == "cmd.exe" set UAC=1
)
if "%UAC%" == "1" goto Main
echo.
echo 你没有以管理员身份运行当前批处理程序，这样可能会出错，是否要继续？
echo.
set /p xj=Y: 继续 N: 退出 
if "%xj%"=="Y" goto Main
if "%xj%"=="y" goto Main
goto End
:Main
PUSHD %~DP0 &TITLE 绿化和卸载
mode con cols=36 lines=20
color 2F
:Menu
Cls
@ echo.
@ echo.
@ echo.           百度云不限速版
@ echo.
@ echo.           版本号 v9.9.9.9
@ echo.
@ echo.      ╔══════════╗
@ echo.      ║                    ║
@ echo.      ║   绿化 → 请输入1  ║
@ echo.      ║                    ║
@ echo.      ╠══════════╣
@ echo.      ║                    ║
@ echo.      ║   卸载 → 请输入2  ║
@ echo.      ║                    ║
@ echo.      ╠══════════╣
@ echo.      ║                    ║
@ echo.      ║   退出 → 请输入0  ║
@ echo.      ║                    ║
@ echo.      ╚══════════╝
@ echo.
@ echo.
set /p xj=输入数字后按回车键:
if /i "%xj%"=="1" Goto Install
if /i "%xj%"=="2" Goto Uninstall
if /i "%xj%"=="0" Goto End
@ echo.
echo      选择无效，请重新输入
ping -n 2 127.1>nul 
goto menu
:Install
@ echo.
ECHO 　　　正在安装中..请稍等..
taskkill /f /im BaiduYunGuanjia.exe>NUL 2>NUL
taskkill /f /im 百度云不限速.exe>NUL 2>NUL
del /f AppSettingApp.dat  >NUL 2>NUL
rd/s/q "%tmp%\bdyunguanjiaskinres" 2>NUL
rd/s/q "%AppData%\BaiduYunGuanjia" 2>NUL
rd/s/q "%AppData%\Baidu\BaiduYunGuanjia"2>NUL
regsvr32 /s npYunWebDetect.dll
reg delete "HKCU\Software\Baidu\BaiduYunGuanjia" /f >NUL 2>NUL
reg delete "HKCR\CLSID\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKCU\SOFTWARE\Classes\CLSID\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKLM\SOFTWARE\Classes\CLSID\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKLM\SOFTWARE\Wow6432Node\Classes\CLSID\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKLM\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
mshta VBScript:Execute("Set a=CreateObject(""WScript.Shell""):Set b=a.CreateShortcut(a.SpecialFolders(""Desktop"") & ""\百度云不限速.lnk""):b.TargetPath=""%~dp0百度云不限速.exe"":b.WorkingDirectory=""%~dp0"":b.Save:close")
if exist "%WinDir%\SysWOW64" regsvr32 /s YunShellExt64.dll
if not exist "%WinDir%\SysWOW64" regsvr32 /s YunShellExt.dll
goto Install2
:Uninstall
@ echo.
echo 　　　正在卸载中..请稍等.
taskkill /f /im BaiduYunGuanjia.exe>NUL 2>NUL
taskkill /f /im 百度云不限速.exe>NUL 2>NUL
del /f AppSettingApp.dat  >NUL 2>NUL
rd/s/q "%tmp%\bdyunguanjiaskinres" 2>NUL
rd/s/q "%AppData%\BaiduYunGuanjia" 2>NUL
rd/s/q "%AppData%\Baidu\BaiduYunGuanjia"2>NUL
regsvr32 /s /u YunShellExt.dll
regsvr32 /s /u npYunWebDetect.dll
if exist "%WinDir%\SysWOW64" regsvr32 /s /u YunShellExt64.dll
reg delete "HKCU\Software\Baidu\BaiduYunGuanjia" /f >NUL 2>NUL
reg delete "HKCR\CLSID\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKCU\SOFTWARE\Classes\CLSID\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKLM\SOFTWARE\Classes\CLSID\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKLM\SOFTWARE\Wow6432Node\Classes\CLSID\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
reg delete "HKLM\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\{679F137C-3162-45da-BE3C-2F9C3D093F64}" /f>NUL 2>NUL
del /f /q "%userprofile%"\Desktop\百度云不限速.lnk
del /f /q "%userprofile%"\桌面\百度云不限速.lnk
goto Uninstall2

:Install2
ECHO 　　　安装完成..
ping -n 2 127.8>nul
goto menu
:Uninstall2
ECHO 　　　卸载完成..
ping -n 2 127.8>nul
goto menu
:End