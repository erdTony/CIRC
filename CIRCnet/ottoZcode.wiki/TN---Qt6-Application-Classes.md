## Tech Note 3381
# Qt6 Application Classes

## Class Hierarchy

* QObject
  * QCoreApplication
    * QGuiApplicatiom
      * QApplication
    * (QAndroidService)

## Classes

### QCoreApplication
  * Qt Core
  * : QObject
  * This class is used by non-GUI applications to provide their event loop. For non-GUI application that uses Qt, there should be exactly one QCoreApplication object.

### QGuiApplication
  * Qt Gui
  * : QCoreApplication
  * QGuiApplication contains the main event loop, where all events from the window system and other sources are processed and dispatched. It also handles the application's initialization and finalization, and provides session management. In addition, QGuiApplication handles most of the system-wide and application-wide settings. For any GUI application using Qt, there is precisely one QGuiApplication object no matter whether the application has 0, 1, 2 or more windows at any given time.

### QApplication
  * Qt Widgets
  * : QGuiApplication
  * QApplication specializes QGuiApplication with some functionality needed for QWidget-based applications. It handles widget specific initialization, finalization. For any GUI application using Qt, there is precisely one QApplication object, no matter whether the application has 0, 1, 2 or more windows at any given time.