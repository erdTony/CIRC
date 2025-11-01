# TN4121 Windows Initial Setup


## Baseline

* [ ] Chrome
  * [ ] Bing to `Chrome Download`,  Ignore Microsoft begging
  * [ ] Run downloaded `ChromeSetup.exe`
    * [ ] Sign in `ottoztony:L3r769`
  * [ ] Set as defalt browser

* [ ] ~~VNC~~ _Hold for now_
  * ~~Viewer `https://www.realvnc.com/en/connect/download/viewer/`, Select [Windows], [x64], Press [Download]~~
  * ~~Server `https://www.realvnc.com/en/connect/download/vnc/`, Select [Windows], [x64], Press [Download]~~
  * ~~Setup account: ottoztony@gmail.com:LakeLanc3r79~~

## Utilities

* [x] Paragon Partition Manager
* [x] qBittorrent
* [ ] Google Keep (add to Chrome toolbar)
* [x] Google Drive for Desktop
  * `https://www.google.com/drive/download/`, press [Download for Desktop]
  * When downloaded, run, press [Install]
  * When installed, press [Launch]
    * Press [Get Started], [Sign In]
    * Press [Add Folder], add `G:\GDrive`
    * Press [Next], [Got It]
    * Check `Pictures` and `Videos`, Press [Next]
    * Press [Next], [Open Drive]

* [ ] Gadwin PrintScreen
  * _Preferences_ as desired
  * Note _HotKeys_
    * Full = `PrtSc`
    * Window = Shift-`PrtSc`
    * Area = Ctrl-`PrtSc`
  * Image - uncheck `Capture Cursor` and `Shadow`
  * Actions
    * Uncheck `Preview`
    * Capture Folder - `H:\PrtSc`
    * File Template- `%comp-D%Y%m%d-T%H%M%S`

## Office

* [ ] LibreOffice

## Social

* _Hold for now_
* [ ] WhatsApp
* [ ] Skype
* [ ] Zoom

## Image & Video

* [ ] yEd Diagram Editor
  * `https://www.yworks.com/products/yed/download#download`, Press [Download]
  * Press [yEd for Windows], Accept, [Download], [OK]
  * When downloaded, Run
    * Press [Next], Accept, [Next]
    * Install to H:\Lang\yWorks\yEd
    * Press [Next]*4, ..., [Finish]
* [ ] InkScape
  * `https://inkscape.org/release/0.92.4/windows/64-bit/`, Press [MSI]
  * When downloaded, Run
    * Press [Next], Accept, [Next], [Typical], [Install], ..., [Finish]
* [ ] IrFan Image Viewer
  * `https://www.irfanview.com/64bit.htm`, Select 64-bit Download link
  * `https://www.fosshub.com/IrfanView.html?dwl=iview462_x64_setup.exe`
    * Click `IRFANVIEW Download`
      * When downloaded, run iview-...exe
      * Install for all to `H:\Lang\IrfanView\`
      * Press [Next]*4, [Done]
      * **TODO:** Associate JPG, PNG, etc in Windows Settings
    * Click `Plugins Win64`
      * When downloaded, Run
      * Confirm `H:\Lang\IrfanView\` folder, Press [Next]
* [ ] Vlan Video Player
  * `https://www.videolan.org/vlc/download-windows.html`, Press [Download VLC]
* [ ] Gimp
  * `https://www.gimp.org/downloads/`, Click [Windows], Press [Download via Torrent]
  * When torrent finished, Run, Press [Install], ..., ..., Press [Finish]
  * It is installed to `C:\Program Files\GIMP 2`

## Software Development

* [ ] Notepad++
  * From: `https://notepad-plus-plus.org/downloads/v8.5.8/`
  * `https://github.com/notepad-plus-plus/notepad-plus-plus/releases/download/v8.5.8/npp.8.5.8.Installer.x64.exe`
  * When downloaded (fast), Run
    * Press [Next], Accept, [Next]
    * Install to `H:\Lang\Notepad++`, [Next]
    * Defaults, [Next], [Install]
    * [Finish]
* [ ] git & Glint
  * Reference: [Git-SCM](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  * Reference: [Git For Windows](https://gitforwindows.org/)
  * At [Git-SCM Windows Download](https://git-scm.com/download/win), Select 64-bit Setup
  * When downloaded, Run
    * Press [Next], Install to `C:\home\code\Lang\Git`
    * Check Desktop Icons, Bash Profile in Shell, Press [Next]*2
    * Select Use Notepad++, Press [Next]
    * Select Override, `main`, Press [Next]
    * Select Git from Command Line, Press [Next]
    * Select Bundled SSH, Press [Next]
    * Select OpenSSL, Press [Next]
    * Select Windows/Unix, Press [Next]
    * Select Windows Console, Press [Next]
    * Default to Default, Press [Next]
    * Select Credential Manager, Press [Next]
    * Default Enables twice, Press [Next], Press **[Install]**
    * Press [Finish] and view Release Notes
  * Reference: 
  * From `https://www.syntevo.com/smartgit/download/`, Select [Download for Windows x64]
  * When downloaded, Extract in place
    * Run Setup Application
    * Install to `C:\home\code\lang\SmartGit`, Press [Next]*2 [Install], ..., Press [Finish]
  * **ToDo:** Setup 2 part authentication
* Github Desktop
  * Reference: [Github Docs](https://docs.github.com/en/enterprise-cloud@latest/desktop/installing-and-authenticating-to-github-desktop/installing-github-desktop)
  * From: [Github Desktop](https://desktop.github.com/)
  * Press [[Download 64-bit Windows](https://central.github.com/deployments/desktop/desktop/latest/win32)] _Even though the link says 32 bit_
  * When downloaded, Run:
    * Press [Signin to Github]
    * Press [Open Github Desktop]
* GitHub CLI
  * Reference: `https://cli.github.com/`
  * From: `https://github.com/cli/cli/releases/tag/v2.37.0` or later
  * Download: `https://github.com/cli/cli/releases/download/v2.37.0/gh_2.37.0_windows_amd64.msi` or later
  * When downloaded, Run, Press [Next]
    * Install to: `H:\Lang\GitHubCLI`, Press [Next], [Install], ..., [Finish]
    * > `H:`, > `cd \Lang\GitHubCLI`, > `gh --version`, Expect v2.37.0 (2023-10-17) 
  * Add `H:\Lang\GitHubCLI` to `PATH`
  * > `gh auth login` and make it happy
* ~~CUDA Toolkit SDK~~ _Fails on FYH14X1 Laptop due to old graphics chip_
  * ~~From `https://developer.nvidia.com/cuda-downloads`, Press [Windows], [X86-64], [10], [local], [Download]
  * When downloaded, Run
  * Set Temporary folder to `H:\Temp\CUDA`
  * Agree, Select `Express`, Press [Next], ..., Press [Finish]~~

## Build Environment

* [ ] Visual Studio Code
  * Reference: [Visual StudioCode](https://code.visualstudio.com/docs/setup/windows)
  * `https://go.microsoft.com/fwlink/?LinkID=534107`, Automatic Download
  * Run `VSCodeUserSetup`... .exe
    * Accept, Press [Next]
    * Install to `H:\Lang\Microsoft VS Code`, Press [Next]
    * Default Start Menu, Press [Next]
    * Default Tasks, Press [Next], Press [Install], ..., Press [Finish]
  * Windows Device Driver Kit
    * From [Windows VDK](https://www.microsoft.com/en-us/download/details.aspx?id=11800), Press [Download]
      * `https://www.microsoft.com/en-us/download/details.aspx?id=11800`
* [ ] g++ & friends
  * Reference: https://www.freecodecamp.org/news/how-to-install-c-and-cpp-compiler-on-windows/
  * [ ] From `https://www.msys2.org/`, Download `msys2-x86_64-20230718.exe`
  * [ ] When downloaded, Run, Press [Next], 
    * Install to `H:\Lang\MSYS2`, Press [Next]
    * Default shortcut, Press [Next], ...
    * Press [Next], Check Run, [Finish]
    * **Warning:** This run didn't work; From Start Menu Search, Type MSYS, Select `MSYS2 MSYS` and Run as Administrator
  * From MSYS2 Terminal
    * $ `pacman -Syu`, ..., Enter `Y` twice
    * $
  * Add to PATH: `H:\Lang\Qt\Tools\mingw1120_64\bin`
* [ ] Qt6 with CMake
* [ ] See TN???? for OpenCV4 build on Windows


 
 