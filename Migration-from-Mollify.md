Kloudspeaker is based on [Mollify](https://github.com/sjarvela/mollify), and versions 2.6.7 from both applications are fully compatible.

To migrate existing Mollify installation to Kloudspeaker, do following:

1. Update Mollify to latest version (2.6.7) according to the Mollify update instructions

2. Download and extract latest Kloudspeaker installation package

3. Copy `configuration.php` from Mollify `backend` folder to Kloudspeaker `backend` folder, and add following option

    `"server_hash_salt" => "MOLLIFY_SERVER_SALT"`

4. In case you were running Mollify version prior to 2.2, see chapter "Legacy passwords" below

5. Transfer any other customizations in `index.php` etc (rename any reference to "`mollify`" into "`kloudspeaker`")

6. Run Kloudspeaker updater

## Legacy passwords

Starting from Mollify version 2.2, passwords were created more secure way using hash and salt. However, upgrade could not create these new passwords, but instead they were updated on-the-fly whenever "old" passwords were encountered.

In Kloudspeaker there is no support for legacy passwords, and if migration is done from Mollify version prior to 2.2, legacy support must be added manually.

First, add legacy password detection by modifying "backend/include/auth/AuthenticatorPW.class.php", and add lines according to [Mollify version](https://github.com/sjarvela/mollify/blob/master/backend/include/auth/AuthenticatorPW.class.php) had lines 19-28.

Second, add configuration method for getting legacy password by editing "backend/include/configuration/ConfigurationDao.class.php", and add method according to [Mollify version] (https://github.com/sjarvela/mollify/blob/master/backend/include/configuration/ConfigurationDao.class.php#L108) lines 108-110.