Notificator plugin is built-in plugin that provides mail notifications when certain events happen.

## Configuration

Configure plugin by adding following into configuration.php:


	$CONFIGURATION = array(
		...,
		"plugins" => array(
			"Notificator" => array()
		)
	);

Notificator plugin does not have any parameters.

Notificator requires mail [[notifications enabled|Mail]]

## Installation

Notificator plugin requires database, so run Kloudspeaker updater after adding configuration.

## Variables

Following variables are available in the title and message for all event types:

  * %user_id% User id
  * %user_name% User name
  * %user_email% User email
  * %event_time% Time of the event
  * %event_type% Type of the event, for example "filesystem/rename"
  * %event_main_type% Main type of the event, for example "filesystem"
  * %event_sub_type% Sub type of the event, for example "rename"

For filesystem events, following variables are available:
  * %item_id% Id of the file or folder
  * %item_name% Name of the file or folder
  * %item_path% Mollify path of the file or folder
  * %item_internal_path% Internal path of the file or folder (for local filesystem this the actual location in the filesystem)
  * %root_name% Name of the published folder

Following applies only to rename, copy and move events:
  * %to_item_id% Id of the target file or folder
  * %to_item_name% Name of the target file or folder
  * %to_item_path% Mollify path of the target file or folder
  * %to_item_internal_path% Internal path of the target file or folder (for local filesystem this the actual location in the filesystem)
  * %to_root_name% Name of the target published folder

For session events (login, logout and failed login):
  * %ip% IP address
  * %user% (only for failed login) user name

For registration creation and registration confirmation events:
  * %registration_id% ID of the registration
  * %registration_approve_link% Link for admin approval

For registration creation event also (in addition to previous):
  * %registration_key% Registration key