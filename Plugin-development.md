It is possible to create custom plugins for Kloudspeaker in client and backend.

Client plugins can add content and functionality in the UI, and backend plugins can create new services and extend existing functionality.

Both can be registered separately, but it is also possible to create a backend plugin package that contains also client plugin, which allows making individual packages containing all functionality from UI to backend.

## Client plugins

Define custom module to be loaded as explained in https://github.com/sjarvela/kloudspeaker/wiki/Client-modules.

During the module initialization, register plugin like this:

    define(['kloudspeaker/plugins'], function(plugins) {
        plugins.register({
            id: "custom-plugin",
            initialize: function() {
                ...
            }
        });
    });

Other plugin options:
* `initialize`: function invoked when system is initialized
* `backendPluginId`: plugin identifier used in backend plugin (needs to be defined only if not same as client)
* `resources`: resources plugin requires to be loaded (relevant only when plugin has backend)
* `configViewHandler`: object registered to handle config view related actions and content
* `fileViewHandler`: object registered to handle file view related actions and content
* `itemContextHandler`: object registered to handle item context content
* `itemCollectionHandler`: object registered to handle item collection actions


## Backend plugins

Backend plugins are registered in configuration.php

	<?php
		$CONFIGURATION = array(
			"plugins" => array(
				"CustomPlugin" => array()
			)
		)
	?>

By default, Kloudspeaker expects plugins to be found under folder "backend/plugin".

In this example, plugin "CustomPlugin" is expected to be found at "backend/plugin/CustomPlugin". Under this folder, there should be a class "CustomPlugin.plugin.class.php" (extending class "PluginBase") that is loaded automatically.

	<?php
	class CustomPlugin extends PluginBase {
		public function setup() {
			// plugin setup
		}

		public function __toString() {
			return "CustomPlugin";
		}
	}
	?>

For other options in backend plugins, see backend plugin API.

**Note!** It is recommended to create custom plugins in separate location by using [customization folder](https://github.com/sjarvela/kloudspeaker/wiki/Customizing-resources#plugins). This makes Kloudspeaker updates easier, when custom plugins are not overwritten.

## Packages with client and backend plugins

It is possible to create packages that contain both, client and backend plugins.

By overwriting backend plugin class PluginBase function getClientModuleId, it can define the client module.

For example

	<?php
	class CustomPlugin extends PluginBase {
		public function setup() {
			// plugin setup
		}

		public function getClientModuleId() {
			return "custom/plugin";
		}

		public function __toString() {
			return "CustomPlugin";
		}
	}
	?>

This tells Kloudspeaker that plugin package contains client module, and it will be exposed with package name "custom/plugin", and is mapped into folder "client" under the plugin folder.

When application is started, it automatically loads main module from this package, ie. "client/main.js". This module should do any plugin initialization etc.

For an example how to package client module in backend plugin, see [Trash bin plugin](https://github.com/sjarvela/kloudspeaker/tree/master/backend/plugin/TrashBin).

Using module definition, it is now possible to publish any additional modules and/or files, and refer to them using the package name. For example:

	define(['kloudspeaker/plugins', 'custom/plugin/some/module'], function(plugins, someModule) {
		//use someModule
	});

This will load a module called "some/module" from the plugin package "custom/plugin" automatically, and it will be resolved into "CustomPlugin/client/some/module.js".