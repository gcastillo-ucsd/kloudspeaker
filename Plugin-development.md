It is possible to create custom plugins for Kloudspeaker in client and backend.

Client plugins can add content and functionality in the UI, and backend plugins can create new services and extend existing functionality.

Both can be registered separately, but it is also possible to create a backend plugin package that contains also client plugin, which allows making individual packages containing all functionality from UI to backend.

## Client plugins

Client plugins are registered in index.html

    <script type="text/javascript">
        $(document).ready(function() {
            kloudspeaker.App.init({
                ...
            },
            [
                new CustomPlugin()
            ]
        });
    </script>

The plugin itself is expected to be a javascript object with at least variable `id` defining unique identifier for the plugin.

    var CustomPlugin = function() {
        var that = this;

        return {
            id: "custom-plugin"
        }
    };

or with simple plugins just use plain javascript objects

    <script type="text/javascript">
        $(document).ready(function() {
            kloudspeaker.App.init({
                ...
            },
            [
                {
                    id: "custom-plugin",
                    ...
                }
            ]
        });
    </script>

At minimum, registered plugin object has to be define plugin id.

Other plugin options:
* `initialize`: function invoked when system is initialized
* `backendPluginId`: plugin identifier used in backend plugin (needs to be defined only if not same as client)
* `resources`: resources plugin requires to be loaded
* `configViewHandler`: object registered to handle config view related actions and content
* `fileViewHandler`: object registered to handle file view related actions and content
* `itemContextHandler`: object registered to handle item context content
* `itemCollectionHandler`: object registered to handle item collection actions

For example:
    var CustomPlugin = function() {
        var that = this;

        this.initialize = function() {
            // do plugin initialization
        };

        return {
            id: "custom-plugin",
            backendPluginId: "CustomPlugin",
            initialize: that.initialize,
            resources: {
                css: true,
                texts: true
            },
            fileViewHandler: {
                onInit: function(fileview) {},
                onActivate: function($mainviewElement, mainviewHandle) {},
                onDeactivate: function($mainviewElement, mainviewHandle) {}
            }
        }
    };

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

By overwriting backend plugin class PluginBase function getClientPlugin, it can define the javascript file that is automatically loaded when client is initialized.

For example

	<?php
	class CustomPlugin extends PluginBase {
		public function setup() {
			// plugin setup
		}

		public function getClientPlugin() {
			return "client/plugin.js";
		}

		public function __toString() {
			return "CustomPlugin";
		}
	}
	?>

This tells Kloudspeaker that plugin package contains folder "client" containing "plugin.js" which is loaded automatically.

In this file, there should be client plugin registration like this:

    ! function($, kloudspeaker) {
        "use strict"; // jshint ;_;

        var CustomPlugin = function() {
            return {
                id: "custom-plugin",
                ...
            };
        }

        kloudspeaker.plugins.register(new CustomPlugin());
    }(window.jQuery, window.kloudspeaker);