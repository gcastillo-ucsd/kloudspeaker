Kloudspeaker is based on [Mollify](https://github.com/sjarvela/mollify), and versions starting from 2.6.7 are fully compatible.

To migrate existing Mollify installation to Kloudspeaker, do following:

1. Update Mollify to latest version, at minimum 2.6.7 (as this is the starting version for Kloudspeaker)

2. Download and extract latest Kloudspeaker installation package

3. Copy `configuration.php` from Mollify `backend` folder to Kloudspeaker `backend` folder, and add following option

    `"server_hash_salt" => "MOLLIFY_SERVER_SALT"`

4. Transfer any other customizations in `index.php` etc (rename any reference to "`mollify`" into "`kloudspeaker`")

5. Run Kloudspeaker updater