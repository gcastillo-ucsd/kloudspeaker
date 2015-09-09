Item details plugin is built-in plugin that provides details section in the file or folder popup.

## Configuration

Register plugin by adding following into configuration.php (or merge into existing plugins array):


	$CONFIGURATION = array(
		...
		"plugins" => array(
			...
			"ItemDetails" => array()
		)
	);


## Item details configuration

Details shown for files or folders can be configured by the type, with following format:


	require(['kloudspeaker/app'], function(app) {
		app.init({
			...
			plugins : {
				itemdetails : {
					filetypes: {
						[TYPE] : {
							[DATA_KEY] : [CONFIGURATION],
							...
						},
						...
					}
				}
			}
		});
	});


The type can be:
 * file extension, like "`png`" or "`pdf`"
 * "`[folder]`" for folders
 * "`[file]`" for files
 * "`*`" for default configuration

Data key is the id of the data displayed. Mollify provides following built-in data keys:
 * "`last-modified`" : Time of the last modification
 * "`size`" : Size of the file
 * "`image-size`" : Size of the image (in pixels), requires server lib GD (see http://www.php.net/manual/en/image.requirements.php)
 * "`exif`" : Image exif data (only jpg and tiff supported, see example below on how to register exif renderer)

Some plugins may provide more data keys.

Configuration can override following:
 * "`title`": Title text
 * "`title-key`" : Localization key of the title text

For example:

        require(['kloudspeaker/app'], function(app) {
            app.init({
                ...,
                plugins: {
                    "itemdetails": {
                        filetypes: {
                            "pdf": {
                                "size": {}
                            },
                            "jpg,tiff": {
                                "metadata-created": {},
                                "last-modified": {},
                                "size": {},
                                "exif": {},
                            },
                            "*": {
                                "metadata-created": {},
                                "last-modified": {},
                                "size": {}
                            }
                        }
                    }
                }
            });
        });


This configuration will show created info, last modification stamp and size for all files, except for pdf files only size. Image files (jpf and tiff) will also display EXIF data.