Kloudspeaker can have plugins in client and backend.

Client plugin adds new functionality to the UI, and backend plugin adds new backend functionality like service interface, event handling etc. Some plugin packages have both, for example [[Comments plugin|Comments-plugin]].

# Installation

Installation package contains plugins which only needs to be configured, see "Built-in plugins" below. Each plugin instructions contains plugin specific instructions on how to configure them.

For syntax on how to register plugin in client or backend configuration, see [[Configuration|Configuration]].

Additional plugins, which are not included in installation package, are installed simply by unzipping the package into "backend/plugin" folder, and registering them in configuration according to instructions.

For installing plugins outside installation folder, see [[customization instructions|Customizing-resources#plugins]].

Whenever backend plugins are installed or updated, open the Kloudspeaker updater util to check if database update is required.

# Available plugins

## Commercial Plugins

Following plugins are released with Commercial Plugin license (for more information, see [license page](http://www.kloudspeaker.com/license.php)).

  * [[Quota|Quota-plugin]]
  * [[History|History-plugin]]

## Built-in Plugins
  * [[Event logging|Event-logging-plugin]]
  * [[Registration|Registration-plugin]]
  * [[File viewer/editor|FileViewerEditor-plugin]]
  * [[Lost password|Lost-password-plugin]]
  * [[Notificator|Notificator-plugin]]
  * [[Archiver|Archiver-plugin]]
  * [[Share|Share-plugin]]
  * [[Item collection|Item-collection-plugin]]
  * [[Comments|Comments-plugin]]