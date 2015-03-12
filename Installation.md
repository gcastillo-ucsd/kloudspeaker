# 1. Installation

1. Download latest installation package from http://www.kloudspeaker.com/download/latest.php

2. Unzip Kloudspeaker installation package (for example with command "`unzip kloudspeaker_[VER].zip`")

3. Copy extracted folder "`kloudspeaker`" into your web server root folder (or any other place of your choice)

4. Open installer at address "`http://your.host.name/kloudspeaker/backend/install/`". Installer will guide you through the configuration, for more information see [[Configuration|Configuration]].

5. Log in as admin and choose "Configuration" in app header to configure users and published folders

**NOTE!**

When setting up published folders, note that they should not be accessible via regular web access (= exposed to web server, where folder contents are accessible via browser). Using Kloudspeaker does not require web access to published folders as it can access the files through filesystem.

But since Kloudspeaker cannot prevent the web server from serving those files, there are two options how to prevent it:

1. Place all published folders outside www root. With this option, there is no way users can access the files with browser via Apache. Only PHP has to have read and write access to the folders.
2. Prevent access with web server access rules, for example htaccess rule "`deny from all`" in Apache.

In all cases, published folders should not be located under Kloudspeaker folders (not client or backend), as this makes upgrading difficult.

# 2. Upgrading

Upgrading Kloudspeaker requires following steps:

1. Log into Kloudspeaker as admin user, and leave the session open for the upgrade process
2. For backup, move or rename old installation directory "kloudspeaker" into different name or location
3. Download and unzip latest kloudspeaker release package
4. Copy folder "kloudspeaker" from the latest Kloudspeaker installation package
5. From backup, restore "configuration.php" into the new installation directory (as well as other customized files, such as "index.html")
6. Open updater in your browser at address "`http://your.host.name/kloudspeaker/backend/update/`" to check if further update actions are required.
7. Remove backup directory