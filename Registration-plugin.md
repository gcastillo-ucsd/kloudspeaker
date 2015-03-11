Registration plugin is built-in plugin that provides functionality for user self registration and confirmation.

# Configuration

## Backend

Registration has following settings:
  * `require_approval` (by default TRUE)
  * `permission`
  * `groups`
  * `folders`
  * `user_folder`

Option `require_approval` controls whether registrations require approval before processing. If approval is required, confirmed registration will not create user automatically. Instead, confirmed registrations are listed in admin view, where admin user can approve them. Using notificator plugin admins can get email notifications for confirmable registrations.

Option "`permissions`" controls user default permissions. String value is considered filesystem access permission, but with array syntax it is possible to define all permissions, see [Permissions] for possible values. If not given, no default permissions are added, and system defaults are applied for the created users.

Option `groups` is a list of user group ids for the created user. If not set, user is not assigned to any groups.

Option `folders` is a list of folder ids for the created user. If not set, user is not assigned to any folders.

Option `user_folder` is for creating user folders automatically after registration (leave out if no folders need to be created).

For example:

	$CONFIGURATION = array(
		...,
		"plugins" => array(
			"Registration" => array(
				"require_approval" => TRUE,
				"permissions" => "rwd",
				"folders" => array("1", "3"),
				"user_folder" => array("path" => "/foo/users", "folder_name" => "User Folder", "add_to_users" => array("1", "2"))
			)
		)
	);

Registration plugin requires installation via Kloudspeaker update util.

To enable mail notifications, add following settings:

	$CONFIGURATION = array(
		...,
		"enable_mail_notification" => TRUE,
		"mail_notification_from" => "admin@your.host"
	);


The setting "mail_notification_from" defines the address which the mail is sent from.


## Client

Register client plugin with following client settings:

	<script type="text/javascript">
		kloudspeaker.App.init({
			...
			}, [
				new kloudspeaker.plugin.RegistrationPlugin()
			]
		});
	</script>

# Folders

In backend configuration, it is possible to list only folder ids that are added to the new user.

	$CONFIGURATION = array(
		...,
		"plugins" => array(
			"Registration" => array(
				"folders" => array("1", "3"),
			)
		)
	);

To give folder properties, use following syntax:

	$CONFIGURATION = array(
		...,
		"plugins" => array(
			"Registration" => array(
				"folders" => array(
					"1" => array(
						"name" => "Folder name",
						"permissions" => "rw"
					)
				)
			)
		)
	);

Property "`name`" (optional) can set a name different than the default.

Property "`permissions`" can set assigned folder permissions for the new user. If only single string value given, it is assumed to be filesystem item access permission (see [Permissions]).

To give other permissions (see [Permissions]), use array syntax:

	$CONFIGURATION = array(
		...,
		"plugins" => array(
			"Registration" => array(
				"folders" => array(
					"1" => array(
						"name" => "Folder name",
						"permissions" => array(
							"filesystem_item_access" => "rw",
							"edit_description" => "1"
						)
					)
				)
			)
		)
	);

# User Folder

For user folders definition in backend configuration, the parameters are:
  *  "`path`" is the place where user folders are created, use a folder that is not published.
  *  "`folder_name`" is a name for the folder. Leave it out if you want to name it after the user.
  *  "`add_to_users`" is a list of user ids that also see this folder. Useful for listing admins who need to control these folders.
  *  "`permissions`" is the list of permissions assigned to the created folder. By default, user will get read/write/delete permission, but with this option all permissions can be defined in the same way as explained in chapter Folders.

# Registration process

Once registration plugin is installed, login page will display registration link. Optionally, registration page can be opened diractly with url "`http://[PATH_TO_MOLLIFY]/?v=registration/new`".

Users can fill out the form presented, and they will receive a notification mail after completing the form. Mail provides a link for confirming the registration.

Optionally confirmation can be done at "`http://[PATH_TO_MOLLIFY]/?v=registration/confirm&email=[EMAIL]`", where `[EMAIL]` is the email address (in url encoded format) given in registration. This opens a form where the registration key is required.