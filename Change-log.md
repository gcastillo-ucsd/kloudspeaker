### 2.6.13

Released 2015/6/26
* Share plugin rewrite complete, example on how to use modules to publish config views, full views, dialog views, file column bubble etc
* Trash bin expiration feature and small improvements
* More mime type icons
* New option for mail notificator: mail sender name
* Small improvements and fixes in AMD support etc

### 2.6.12

Released 2015/6/7

Technical release, improves support for AMD design (modular structure) and includes rewritten plugins as modules:
* Share plugin rewritten on most parts, no need to be registered in index.html
* Event logging plugin rewritten, no need to be registered in index.html
* Dropbox rewritten as module, no need to be registered in index.html
* Better support for registering custom full views (example in share plugin)
* Better support for registering custom config views from modules (example in event logging plugin)
* Support for bound UI widget: config list

### 2.6.11

Released 2015/5/23

Technical release, adds support for AMD design (modular structure) and view binding with Durandal/Knockout. See development pages:
* https://github.com/sjarvela/kloudspeaker/wiki/Client-modules
* https://github.com/sjarvela/kloudspeaker/wiki/Plugin-development
* https://github.com/sjarvela/kloudspeaker/wiki/Creating-UI

API changes:
* Registration plugin is rewritten with client module, and is no longer required to be registered in index.html

### 2.6.10 (+ History 1.3 & Quota 1.3)

Released 2015/5/10

* Trash bin support for Quota
* Quota recalculate command changed into command line interface action
* New development API: support for UI binding
* Fixes and improvements

### 2.6.9 (+ History 1.2)

Released 2015/4/27

* Added new feature: https://github.com/sjarvela/kloudspeaker/issues/9
* Added new feature: https://github.com/sjarvela/kloudspeaker/issues/20
* Added new feature: https://github.com/sjarvela/kloudspeaker/issues/21
* Fixed: https://github.com/sjarvela/kloudspeaker/issues/14
* Added new beta plugin [TrashBin](https://github.com/sjarvela/kloudspeaker/wiki/Trash-bin-plugin)
* Added initial support for [command line interface](https://github.com/sjarvela/kloudspeaker/wiki/Command-line-interface)

### 2.6.8 (+ History 1.1 & Quota 1.2)

Released 2015/4/11

* Added new feature: https://github.com/sjarvela/kloudspeaker/issues/5, see [configuration instruction](https://github.com/sjarvela/kloudspeaker/wiki/Backend-configuration-options#ignored-filesystem-items-ignored_items)
* Added enhancement: https://github.com/sjarvela/mollify/issues/15 (with History 1.1)
* Fixed issue: https://github.com/sjarvela/kloudspeaker/issues/8 (with Quota 1.2)
* Fixed issue: https://github.com/sjarvela/mollify/issues/2
* Fixed issue: https://github.com/sjarvela/mollify/issues/9

### Quota plugin 1.1

Released 2015/3/30

* Added quota refresh action for users

### 2.6.7.1

Released 2015/3/29

* Fixed project rename related issues

### 2.6.7

Released 2015/3/20

* First Kloudspeaker release

Kloudspeaker is based on Mollify, and its change log can be found at https://code.google.com/p/mollify/wiki/ChangeLog