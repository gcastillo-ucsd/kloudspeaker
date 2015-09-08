Share plugin is built-in plugin that provides possibility to share any file or folder.

## Configuration

Configure plugin by adding following into configuration.php (or merge into existing plugins array):

        $CONFIGURATION = array(
		...,
		"plugins" => array(
			"Share" => array()
		)
	);

*NOTE* After configuration is done, share plugin requires installation via Kloudspeaker update util.

## Usage

When share plugin has been registered, there will be a new option in file/folder popup called "Share".

This will open a list for all shares made for the file or folder, where you can also get the link for the share.

## File list columns

Share plugin provides share count column with column id `share-info`. For example:

	require(['kloudspeaker/app'], function(app) {
		app.init({
			...
			"list-view-columns": {
				"share-info": {},
				...
			}
		});
	});

Column will show how many shares current user has, or if someone else has shared the item. Clicking the icon also opens the share editor.