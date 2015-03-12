Kloudspeaker is based on [Mollify](https://github.com/sjarvela/mollify), is versions 2.6.x are fully compatible.

To migrate existing Mollify installation to Kloudspeaker, do following:

1. Update Mollify to latest version, at minimum 2.6.x
2. Download and extract latest Kloudspeaker installation package
3. Copy `configuration.php` from Mollify backend folder to Kloudspeaker backend folder, and add following option

    "server_hash_salt" => "MOLLIFY_SERVER_SALT"

4. Transfer any other customizations in `index.php` etc (rename any reference to "mollify" into "kloudspeaker")
5. Run Kloudspeaker updater