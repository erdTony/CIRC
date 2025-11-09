# TN5654 - Ubuntu Office Setup **BROKEN**

## Prerequsites

* [ ] glibc2
  * $ `sudo apt update`
  * $ `sudo apt install glibc-source`
* [ ] Java Runtime 8
  * $ `sudo apt install default-jre`
  * $ and/or? `sudo apt install openjdk-8-jre`
* [ ] Remove old or developer snapshot releases of OpenOffice


* Apache OpenOffice
  * Reference: [Linux Hint](https://linuxhint.com/openoffice_installation_ubuntu/) 
    * and: [Apache](https://www.openoffice.org/product/linux.html)
    * and: [Liberian Geek](https://www.liberiangeek.net/2013/08/apache-openoffice-4-0-releasedheres-how-to-install-it-in-ubuntu/)
  * [ ] $ `sudo apt-get remove --purge libreoffice* libexttextcat-data* && sudo apt-get autoremove`
  * [Download](http://www.openoffice.org/download/) and subscribe
    * $ `cd ~/Downloads` (or your download location)
    * $ `wget http://sourceforge.net/projects/openofficeorg.mirror/files/4.1.14/binaries/en-US/Apache_OpenOffice_4.1.14_Linux_x86-64_install-deb_en-US.tar.gz`
    * $ `tar xzf Apache_OpenOffice_4.1.14_Linux_x86-64_install-deb_en-US.tar.gz`
    * $ `cd en-US/DEBS`
    * $ `sudo dpkg -i *.deb`
    * $ `cd desktop-integration/`
    * $ `sudo dpkg -i openoffice4.1-debian-menus*.deb`
    * **Launch:** $ `openoffice4`



