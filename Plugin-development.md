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
            plugins: {
                new CustomPlugin()
            }
        });
    </script>

The plugin itself is expected to be a javascript object with at least variable `id` defining unique identifier for the plugin.

    var CustomPlugin = function() {
        var that = this;

        return {
            id: "custom-plugin"
        }
    };

For other options in JavaScript plugins, see JS plugin API.

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