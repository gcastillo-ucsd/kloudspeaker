Lost password plugin is built-in plugin that provides possibility to users retrieve their lost password.

## Configuration

Configure plugin by adding following into configuration.php:

	$CONFIGURATION = array(
		...,
		"plugins" => array(
			"LostPassword" => array()
		)
	);

Lost password plugin does not have any parameters.

Lost password plugin requires [[mail notification enabled|Mail]].