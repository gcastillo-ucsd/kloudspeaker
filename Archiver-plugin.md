Archiver plugin is built-in plugin that provides possibility to extract zip archives (later on also tar archives etc) and compress files, as well as download files/folders compressed.

## Configuration

Configure plugin by adding following into configuration.php:


        $CONFIGURATION = array(
		...,
		"plugins" => array(
			"Archiver" => array(
				"compressor" => "[COMPRESSOR]"
				"enable_download" => TRUE/FALSE,
				"enable_compress" => TRUE/FALSE
				"enable_extract" => TRUE/FALSE
			)
		)
	);


Value "COMPRESSOR" is the method used for compressing files, options are:

  * `ziparchive` Default PHP zip library (this is used if setting is not defined)
  * `native` Uses OS native tools to create the package (not available on all platforms)
  * `raw` PHP implementation of zip packaging

Values "`enable_download`", "`enable_compress`" and "`enable_extract`" control whether archiver actions "download", "compress" and "extract" are available.

By default, all actions are enabled, but with this option they can be disabled.