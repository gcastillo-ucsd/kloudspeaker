Kloudspeaker external interface is utility script for controlling Kloudspeaker outside, for example when integrating it into existing site.


## Functions

  * `isAuthenticated()`: check if user is authenticated
  * `authenticate($userId)`: authenticate user with given id
  * `getUserId()`: get authenticated user id
  * `getUsername()`: get authenticated user name
  * `getAllUsers()`: get list of all users configured
  * `getUser($id)`: get user with given id
  * `addUser($name, $pw, $email, $userType, $expiration)`: add new Mollify user, user type and expiration are optional
  * `removeUser($id)`: remove user with given id
  * `addFolder($name, $path)`: add new published folder. Return value is id of the published folder.
  * `addUserFolder($userId, $folderId, $name)`: assign published folder (with id) for a user (with id). Name is optional (default name used if not given)
  * `setUserDefaultFilesystemPermission($userId, $permission)`: Set user default filesystem permission
  * `setUserFolderFilesystemPermission($userId, $folderId, $permission)`: Set user folder permission
  * `addFilesystemItemAccessPermission($itemId, $permission, $userId)`: add item filesystem permission for a user.

Permission options are: "no" (none), "ro" (read-only) or "rw" (read-write)

## Examples

Following example shows how to make user logged in (only need to resolve Kloudspeaker user id):

    <?php 
        set_include_path("backend/".PATH_SEPARATOR.get_include_path()); 
        require_once("external/KloudspeakerExternalInterface.class.php"); 
        $ks = KloudspeakerExternalInterface(); 
        $ks->authenticate(GET_KLOUDSPEAKER_USER_ID_SOMEHOW()); 
    ?>

Following example shows how to add new user and assign a folder with read/write permissions:

    <?php 
        set_include_path("backend/".PATH_SEPARATOR.get_include_path()); 
        require_once("external/KloudspeakerExternalInterface.class.php"); 
        $ks = KloudspeakerExternalInterface(); 
        $userId = $ks->addUser("New User", "password", "email");
        $folderId = GET_KLOUDSPEAKER_FOLDER_ID_SOMEHOW();
        $ks->addUserFolder($userId, $folderId);
        $ks->setUserFolderFilesystemPermission($userId, $folderId, "rw"); 
    ?>