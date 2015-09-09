Comments plugin is built-in plugin that provides possibility to comment any file or folder.

## Configuration

Configure plugin by adding following into `configuration.php` (or merge into existing plugins array):

	$CONFIGURATION = array(
		...,
		"plugins" => array(
			"Comment" => array()
		)
	);

*NOTE* After configuration is done, comments plugin requires installation via Kloudspeaker update util.

## File list columns

Comments plugin provides comments count column with column id `comment-count`. For example:

	app.init({
		...
		"list-view-columns": {
			"name": {},
			"comment-count": {},
			"type": {},
			"size": {}
		}, [
			new kloudspeaker.plugin.CommentPlugin()
		]
	});

For more info, see [[file list column customization|Client-configuration-options#file-list-column-customization]].