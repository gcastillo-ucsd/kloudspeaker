Mollify external interface is utility script for controlling Mollify outside, for example when integrating it into existing site.


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
  * `addItemPermission($id, $permission, $userId)`: add item permission for a user. Permission is "no" (none), "ro" (read-only) or "rw" (read-write)

## Example

Following example shows how to make user logged in (only need to resolve Kloudspeaker user id):

    <?php 
        set_include_path("backend/".PATH_SEPARATOR.get_include_path()); 
        require_once("external/KloudspeakerExternalInterface.class.php"); 
        $ks = KloudspeakerExternalInterface(); 
        $ksUserId = GET_KLOUDSPEAKER_USER_ID(); 
        $ks->authenticate($mollifyUserId); 
    ?>
