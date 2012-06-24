helloqt5
========

Qt5/QtQuick 2 modifications to QtCreator's Harmattan project.

Has modifications so that compiles both on Qt5 and Qt4 projects.

Currently you need to yourself modify the qml files to import
correct modules. For Qt5 the imports are:

import QtQuick 2.0
import com.nokia.meego 2.0
