Comments plugin is built-in plugin that provides possibility to comment any file or folder.

## Configuration

### Backend

Configure plugin by adding following into `configuration.php` (or merge into existing plugins array):

	$CONFIGURATION = array(
		...,
		"plugins" => array(
			"Comment" => array()
		)
	);

### Client

Add following into client settings:

	kloudspeaker.App.init({
		...
		}, [
			new kloudspeaker.plugin.CommentPlugin()
		]
	});


*NOTE* After configuration is done, comments plugin requires installation via Kloudspeaker update util.

## File list columns

Comments plugin provides comments count column with column id `comment-count`. For example:

	kloudspeaker.App.init({
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