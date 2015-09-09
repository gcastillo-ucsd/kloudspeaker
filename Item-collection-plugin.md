Item collection plugin is built-in plugin that provides possibility to store dropbox contents and share them via public link.

## Configuration

Configure plugin by adding following into configuration.php:


        $CONFIGURATION = array(
		...,
		"plugins" => array(
			"ItemCollection" => array()
		)
	);


*NOTE* After configuration is done, share plugin requires installation via Kloudspeaker update util.

## Usage

When share plugin has been registered in both, client and server, there will be a new option in dropbox and item selection dropdown: "Store". This will store all the items selected, and it will be accessible in the left side panel under "Stored".

In the stored collections list, user can share the collection (if [[Share plugin|Share-plugin]] is configured) and get the public link which will download the contents in zip package.

## Requirements

Item collection plugins requires
  * zip feature enabled
  * share plugin registered (for sharing collections)