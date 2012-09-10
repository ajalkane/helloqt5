helloqt5
========
Qt5/QtQuick 2 modifications to QtCreator's Harmattan "Hello World" project 
to compile and run on Qt5.

Disclaimer
==========
The purpose of this project is to aid in porting harmattan applications
from qt4 to qt5. There is some effort in the project to make it compilable
both for qr4 and qt5 targets, but it is not complete.

Prerequisites for compilation
=============================
Development can be done with QtCreator, but final compilation for qt5 target
must be done on scratchbox. Here's one nice tutorial on setting up such an environment:
http://www.johanpaul.com/blog/2011/06/how-to-set-up-meego-harmattan-development-environment-in-linux/

In scratchbox set-up community repositories for qt5 packages (http://www.who.is.free.fr/wiki/doku.php?id=harmattan):

distro="harmattan"
target="MeeGo_1.2_Harmattan_Maemo.org_MeeGo_1.2_Harmattan_standard"
repo="home-rzr-${distro}-${target}"
url="http://repo.pub.meego.com/home:/rzr:/${distro}/${target}/"
echo "deb ${url} ./" |  tee "/etc/apt/sources.list.d/${repo}.list"

Install qt5 libraries:
apt-get update
apt-get install 'qt5.*'

Creating debian package 
=======================
PATH=/opt/qt5/bin:$PATH
make distclean # If you have compiled for another target
qmake
dpkg-buildpackage

If you get errors about missing 'xcb*" libraries, install them and run "dpkg-buildpackage" again.

The resulting debian package will appear one level above helloqt5 directory.

Running on device
=================
Install the community repository and qt5 libraries like in "Prerequisites for compilation" to device

Copy the compiled .deb to device and install it:
$ devel-su
# dpkg -i helloqt5*.deb
# exit

Run (as user or developer):
QML_IMPORT_PATH=/opt/qt5/imports LD_LIBRARY_PATH=/opt/qt5/lib /opt/helloqt5/bin/helloqt5

Known issues
============
 - Tilting the device does not change the orientation. This probably needs some changes to meego plugin and/or qt-components.
 - The homescreen icon is not yet usable



