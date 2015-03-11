Kloudspeaker allows storing customized versions of resources outside Kloudspeaker folders, which makes updates easier.

To avoid losing customizations when updating Kloudspeaker version, set up a customizations folder in the kloudspeaker root, instead of inside any of the folders in the Kloudspeaker package.

Suggested folder structure is:
  * Kloudspeaker app root/
    * custom (CREATE THIS)
    * backend/
    * js/
    * localization/
    * css/
    * templates/
    * index.html

Under folder "custom", create all custom plugins, stylesheets and localizations.

Customization folder location and URL are defined in [[configuration|Backend-configuration-options#customizations-folder-customizations_folder]].

For example:

	$CONFIGURATION = array(
		...
		"customizations_folder" => "/htdocs/kloudspeaker/custom/",
		"customizations_folder_url" => "http://myhost/kloudspeaker/custom/",
	)

The option '`customizations_folder_url`' defines the URL where this folder is accessible, and is needed for serving plugin resources from the customization folder.

# Client resources

Using [[client resource map|Client-resource-map]], different resources can be mapped into custom location. These include any client loaded resources:
  * plugin texts
  * plugin javascripts
  * plugin css
  * templates

Copy original file into the custom location, and add resource map entry to load your version instead.
 
For example, following loads custom "mainview.html" from folder "custom" :

	kloudspeaker.App.init({
		"resource-map" : {
			"templates/mainview.html" : "custom/templates/mainview.html"
		},
		...
	});


For example, following loads custom localizations file for Registration plugin:

	kloudspeaker.App.init({
		"resource-map" : {
			"backend/plugin/Registration/localization/texts_en.json": "custom/localization/texts_registration_en.json"
		},
		...
	});


# Plugins

Plugins can be also located in the customizations folder. This allows, for example, creating custom version of built-in plugin, or placing separately downloaded plugins outside the installation plugin folder, which makes upgrades easier as new version package does not remove or overwrite these plugins.

Plugins located in customization folder are marked with setting `"custom" => TRUE`, for example:

	"plugins" => array(
		"Comment" => array(
			"custom" => TRUE
		),
	)

All plugins must be located inside folder "plugin" under the customization folder.

For example, with previous example, it is expected that plugin "Comments" is found under `[customization_folder_location]/plugin/Comment`.

# Backend texts

When a backend feature needs text resources, these are stored in a text file. With a customizations location defined, Kloudspeaker will look for any text resource from that location first.

Customizations location is defined in configuration.php with following setting:

	$CONFIGURATION = array(
		"customizations_folder" => "/Applications/MAMP/htdocs/kloudspeaker/custom/backend/",
		...
	);


Now any text resources are first searched from this folder.

For example customizing LostPassword plugin texts:

1. Copy "`backend/plugin/LostPassword/PluginLostPasswordMessages.txt`" into customizations folder defined in `configuration.php`
2. Make your own modifications