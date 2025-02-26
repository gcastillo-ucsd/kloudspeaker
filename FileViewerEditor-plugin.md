File viewer and editor plugin is built-in plugin that provides file view, preview and edit. Different file types are handled by viewers or editors, which can be added separately.

# Configuration

Plugin is registered with name "`FileViewerEditor`".

File viewer has following settings:
* "viewers"
* "previewers"
* "editors"

Each list viewer/previewer/editor and file extensions they handle, in format of `[NAME] => [FILE_TYPE_LIST]`.

For example:

	$CONFIGURATION = array(
		...,
		"plugins" => array(
			"FileViewerEditor" => array(
				"viewers" => array(
					"Image" => array("gif", "png", "jpg"),
					"TextFile" => array("txt", "php", "html")
				),
				"previewers" => array(
					"Image" => array("gif", "png", "jpg")
				),
				"editors" => array(
					"TextFile" => array("txt")
				)
			)
		)
	);

# Viewers

## Built-in viewers

### Image

Provides image viewer for gif, png and jpg files.

Configuration:

    "Image" => array("gif", "png", "jpg")

### ViewerJS

Provides file viewer for PDF and ODF, uses [ViewerJS library](http://viewerjs.org/).

**NOTE!** Viewer is published with AGP-3.0 license, see license text in viewer folder.

### Google

Provides file viewer for PDF, DOC and TIFF.

**NOTE!** All sites using this service must agree to the [https://docs.google.com/viewer/TOS?hl=en Google Viewer Terms of Service]

Configuration:

    "Google" => array("pdf", "tiff", "doc")


Using Google Viewer requires that files can be accessed from internet (as the Google service needs to download the file). When Kloudspeaker is used in a closed network (ie. intranet), this viewer cannot be used.

### Quicktime

Provides video viewer for mov and mp4 video files.

Configuration:

    "Quicktime" => array("mov", "mp4")


## Additional viewers

File viewer plugins are installed by unzipping installation package to "`backend/plugin/FileViewerEditor/viewers`".

Additional viewers can be found from [Downloads](http://www.kloudspeaker.com/downloads.php)

### TextFile

Provides text file viewer with syntax hilighting. Viewer uses [http://alexgorbatchev.com/wiki/SyntaxHighlighter SyntaxHighlighter] from Alex Gorbatchev. See `ReadMe.txt` in the package.

Configuration:

    "TextFile" => array("txt", "js", "css", "xml", "html", "xhtml", "py", "c", "cpp", "as3", "sh", "java", "sql", "php")


### JPlayer

Provides music player for mp3 and ogg files, and uses [http://www.happyworm.com/jquery/jplayer/ JPlayer] by Happyworm. See `ReadMe.txt` in the package.

Configuration:

    "JPlayer" => array("mp3")


### FlowPlayer

Provides video player for mp4, flv and f4v files, and uses [http://flowplayer.org/ FlowPlayer] by Flowplayer Ltd. See `ReadMe.txt` in the package.

Configuration:

    "FlowPlayer" => array("f4v")


# Previewers

## Built-in previewers

### Image

Provides image previewer for gif, png and jpg files.

Configuration:

    "Image" => array("gif", "png", "jpg")


## Additional previewers

File previewer plugins are installed by unzipping installation package to "`backend/plugin/FileViewer/previewers`".

Additional previewers can be found from [Downloads](http://www.kloudspeaker.com/downloads.php)

# Editors

## Built-in editors

### TextFile

Provides text file editing.

Configuration:

    "TextFile" => array("txt")


## Additional editors

File editor plugins are installed by unzipping installation package to "`backend/plugin/FileViewerEditor/editors`".

Additional editors can be found from [Downloads](http://www.kloudspeaker.com/downloads.php)

### CKEditor

Provides HTML file editing, and uses [http://ckeditor.com/ CKEditor] by CKSource. CKEditor is released under GPL, LGPL and MPL open source licenses, for more info see [http://ckeditor.com/license].

Configuration:

    "CKEditor" => array("html")