Folder quota plugin allows setting maximum space for a folder.

For a user, quota is visible in the file view header. When any action (upload, copy, move etc) would exceed the quota available, it is rejected.

![File list view with Quota plugin](http://www.kloudspeaker.com/images/screenshots/history_quota.png)

Quota is set by admin in root folder level:

![Quota admin](http://www.kloudspeaker.com/images/screenshots/quota_admin.png)

# Installation & Configuration

Quota plugin requires Kloudspeaker version 2.6 or later.

Quota plugin is installed with following steps:

1. Extract plugin zip package into "backend/plugin" folder (for installing plugin outside installation folder, see [[customization instructions|Customizing-resources#plugins]])
2. Add plugin configuration into "configuration.php" (see configuration options below)
3. Run Kloudspeaker updater

Example minimum configuration:

	$CONFIGURATION = array(
		...
		"plugins" => array(
			"Quota" => array(),
			...
		)
	);

Quota plugin does not require any configuration, but has following options:

  * `registration_user_folder_quota`: Automatic quota set for user folders when user registers with Registration plugin (value in Mb)

Example full configuration:

	$CONFIGURATION = array(
		...
		"plugins" => array(
			"Quota" => array(
				"registration_user_folder_quota" => 1000	
			),
			...
		)
	);

# License

Plugin is released with Commercial Plugin license (http://www.kloudspeaker.com/license.php).

License costs 150 EUR, and download link will be provided after successful license payment.