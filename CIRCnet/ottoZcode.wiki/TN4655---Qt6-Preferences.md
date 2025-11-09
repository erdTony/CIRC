# TN4655 - Qt6 Preferences

## For ottoztony (Tony Otto)

* /Edit/Preferences
  * Environment
    * Keyboard
      * [ ] Remove: `Alt+R`, `Ctrl+Q` _(EXIT)_
      * [ ] Change: FollowSymbolUnderCursorInNextSplit and JumpToFileUnderCursorInNextSplit from `Ctrl+E, F2` to `Ctrl+F2`
      * [ ] Change: QtCreator/GoToNextSplit to `Ctrl+F1`
      * [ ] Set: Project Explorer/Build Project as `Ctrl+B`
      * [ ] Set: Project Explorer/Build Project Only (no dependencies) as `Alt+B`
      * [ ] Set: Project Explorer/BuildFile as `Ctrl+Alt+B`
      * [ ] Set: Project Explorer/Rebuild Session to `Ctrl+Shift+B`, Removing conflicts
      * [ ] Set: DeleteLine to `Ctrl+Del`
      * [ ] Set: CopyLineDown to `Ctrl+Down`, Removing ViewLineDown
      * [ ] Set: Run QMake to `Ctrl+Q`
  * Text Editor
    * Font & Colors
      * Font
        * [ ] Family: Source Code Pro
        * [ ] Font Size: 12
        * [ ] _Laptop_: Maybe Zoom >100%
        * Color Scheme
          * [ ] Scheme: Default Classic _Trying_
          * [Copy...] to Default Classic Tony
            * Select `Parentheses`, Foreground, Set 'Brick Red' `#AA0000`, OK
              * Check Bold
              * Press Background Unset
            * Select `Selection`, Foreground, Set 'Full White' `#FFFFFF`, OK
              * Press Background, Set 'Dark Blue' `#00007F`, OK
    * Behavior
      * Uncheck: Enable built-in camel case navigation (`Alt+n`)
    * Display
      * Check: Display Line Numbers
  * C++
    * File Naming
      * [ ] Check: Use `#pragma once`
      * [ ] Uncheck: Lower Case File Names
    * Quick Fixes
      * Uncheck: In cpp file twice
      * Getter name: `<name>`
      * Setter name: `<name>`
      * Setter parameter name: `new_<name>`
      * Reset name: `reset_<name>`
      * Signal name: `changed_<name>`
      * Member variable name: `p_<name>`
  * Build & Run
    * General tab
      * Projects Directory
        * [ ] Directory: `/home/code/repo`
      * Build and Run
        * [x] Check: Save all files before build
    * Default Build Properties tab
        * [ ] Default Build Directory: Replace leading `../` with `/tmp/QtBuild/`
        * `/QtTemp/%{JS: Util.asciify("build-%{Project:Name}-%{Kit:FileSystemName}-%{BuildConfig:Name}")}`
    * Application Output tab
      * [x] Check: Clear old output on a new rum
      * [x] Check: Merge stderr and stdout
    * Compile Output tab 
      * [x] Check: Open Compile Output when building

### Qt Creator Plugins

* /Help/About Plugins...
  * Navigate to `Utility`
    * Check `ToDo`
  * Then, /Edit/Preferences...
    * Select `ToDo`
      * Add keywords if you like (such as MUSTDO Error #AA0000)
      * Select Whole Active Project if you like
  * Search for QML
    * Disable (uncheck) all related to QML, unless, of course, you need QML. Makes it much faster startup and normal operation in Creator.
  * Press `OK`
  * Restart Qt Creator

