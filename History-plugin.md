History plugin enables file versioning.

When user uploads or copies file that already exists, the older file is versioned.

![File view with History plugin](http://www.kloudspeaker.com/images/screenshots/history_quota.png)

Versioned files are shown in the file listing, where they can be viewed, removed or restored.

![File history](http://www.kloudspeaker.com/images/screenshots/history.png)

# Installation & Configuration

History plugin requires Kloudspeaker version 2.6 or later.

History plugin is installed with following steps:

1. Extract plugin zip package into "backend/plugin" folder (for installing plugin outside installation folder, see [[customization instructions|Customizing-resources#plugins]])
2. Add plugin configuration into "configuration.php" (see configuration options below)
3. Run Kloudspeaker updater

Example minimum configuration:

	$CONFIGURATION = array(
		...
		"plugins" => array(
			"History" => array(
				"folder" => "/data/kloudspeaker/history"
			),
			...
		)
	);

History plugin has following options:
* `folder`: Server filesystem path to the folder where versions are managed (use absolute path). **Required**
* `max_versions`: The maximum number of versions stored for each file. When number is exceeded, older versions are removed. By default, there is no restriction on number of versions.
* `exclude_folders`: List of root folder IDs that are excluded from version handling, by default all folders are included
* `store_current_on_restore`: Whether current file is versioned when older version is restored, by default TRUE
* `version_on_copy`: Whether copy action over existing file will version the current file, by default TRUE

**NOTE!** Folder used for version storage *should not* be

  * exposed via web server (ie. use location outside web root), only PHP needs read/write access to it
  * accessed/modified by other than plugin itself, as any modifications to the internal version data files may corrupt versioning. This includes a) publishing the folder in Kloudspeaker itself and b) modifying the files directly with FTP or server filesystem etc.

Example full configuration:

	$CONFIGURATION = array(
		...
		"plugins" => array(
			"History" => array(
				"folder" => "/data/kloudspeaker/history",
				"max_versions" => 3,
				"exclude_folders" => array("2")
			),
			...
		)
	);

# License

Plugin is released with [Commercial Plugin license](http://www.kloudspeaker.com/license.php).

License costs 150 EUR, and can be downloaded from [Download page](http://www.kloudspeaker.com/downloads.php).