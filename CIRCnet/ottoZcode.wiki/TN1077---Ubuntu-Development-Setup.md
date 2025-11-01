# TN1077 Ubuntu Development Setup

This will guide setup of base line Linux software for a new installation.

* [ ] Snap - ensure `snapd` is available
  * $ `sudo apt upgrade`
  * $ `sudo apt update`
  * $ `sudo apt install snapd`

* [ ] gcc & friends
  * Reference: [Linuxize](https://linuxize.com/post/how-to-install-gcc-compiler-on-ubuntu-18-04/)
  * $ `sudo apt install build-essential`
  * _Note: New Qt6.5+ prerequisites._
  * $ `sudo apt install libxcb-cursor0` 
  * $ `sudo apt install freeglut3-dev` 

* [ ] git & SmartGit
  * Reference: [G4G](https://www.geeksforgeeks.org/how-to-install-configure-and-use-git-on-ubuntu/)
  * $ `sudo apt-get install git'
  * Reference: [idroot](https://idroot.us/install-smartgit-ubuntu-20-04/)
  * $ `sudo add-apt-repository ppa:eugenesan/ppa`
  * $ `sudo apt update`
  * $ `sudo apt install smartgit`

* [ ] Qt
  * For Qt Creator and Libraries
  * Download `qt-unified-linux-x64-4.?.?-online.run` from qt.io/download open source
  * $ `cd ~/Downloads`
  * $ `chmod 500 qt-`<tab>
  * $ `sudo ./qt-`<tab>
    * Enter email address and Lakewood password, Next>
    * Agree, enter company name or check no-company, Next>, Next>
    * Help or disable, Next>
    * _Installation_
      * to `opt\Qt` or alternative
      * First pass check Q6 6.? Development Environment
      * [Agree], Next>, [Install]

