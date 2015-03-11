In case of errors, first check most common errors below.

If none of those help with your problem, do following steps before reporting new issue:

1. Check for configuration file errors

    Modify script "`backend/check.php`" and enable the script as instructed in the file. Open url in your browser: `http://yourhost/backend/check.php`. If the script tells that file is OK, continue with other steps. Otherwise correct the problem as instructed, and try again.

2. Enable server side logging by adding following settings in `configuration.php`:


		$CONFIGURATION = array(
			...,
			"debug" => TRUE
		);

	This enables detailed logging in the backend, and it will be written in PHP error log file. If you don't know where this file is, ask your service provider.

	In case that service provider does not allow access to the log file, custom log file can be set up with following:

		$CONFIGURATION = array(
			...,
			"debug" => TRUE,
			"debug_log" => "/kloudspeaker/debug.log", // CHANGE THIS
		);

	The debug log file path must be located in a folder where PHP has read and write permissions. Using absolute path is recommended.

3. Recreate the error situation

4. Get the log

	Get the debug log from PHP error log, or from custom log file (if defined).

	Optionally, log can be retrieved with browser: `http://yourhost/backend/r.php/debug`. This option applies only to admin users, and the log is emptied every time this url is opened.

5. Copy the debug info and attach into error report

**NOTE!** Once the logs are reported, remember to disable server side debug logging option as it generates lots of log entries.



# Most Common Errors

## Error "Cannot modify header information" or "Got malformed JSON response"

Error "Cannot modify header information, headers already sent" means PHP output is started prematurely before the Kloudspeaker session is initialized.

Error "Got malformed JSON response" means response is received to the client, but it's format is not valid.

Usually these are due to following content in `configuration.php` file:

* there are extra characters outside php tags: spaces, line feeds, tabs etc. There must be nothing before or after "`<?php`" and "`?>`"
* the file has been saved in UTF-8 without BOM information

## Error "`Cannot resolve host`"

Some features, like sharing file links, requires the public URL to access the resources. If possible, Kloudspeaker will try to resolve this, but in some cases this information is not available.

In this case, you need to define this manually with setting "host public address", see option [[host public address|Backend-configuration-options#host-public-address-host_public_address]]

## Error "`Parse error: syntax error, unexpected '{'`"

Error "`Parse error: syntax error, unexpected '{'`" occurs when PHP version is lower than the minimum required.

## Error "Localization file missing" with IIS

With IIS server, JSON file downloads may require configuration:

* make sure "Application Development Features" are enabled
* make sure JSON file type has mime type configured (application/json)

## Some operations, like rename or editing descriptions, don't work

Kloudspeaker uses REST HTTP protocol for the requests, which means all HTTP methods (ie. GET, PUT, POST and DELETE) must be supported by the web server. If these are not supported, many operations will fail (error in the server log indicate protocol error or missing resource).

To fix this, Kloudspeaker can be set to operate on [[limited HTTP methods mode|Backend-configuration-options#limited-http-methods-enable_limited_http_methods]].

## Filenames have corrupted chars, or file upload/download does not work with special chars

Kloudspeaker operates on UTF-8, so all the data handled must be in UTF-8. First make sure your Kloudspeaker web page is set to display UTF-8 content, with following tag in head section: 

    <meta http-equiv="content-type" content="text/html; charset=UTF-8">

If this is correct, then most likely your filesystem does not operate on UTF-8 (usually Windows). In this case you need to configure charset conversion:

1. If you are using MySQL, make sure the charset used is UTF-8. See [[Configuration|Configuration]].

2. Setup conversion as instructed in [[configuration|Backend-configuration-options#convert-filesystem-filenames-convert_filenames]]

## Godaddy hosting and error "No input file specified"

1. Enter the Godaddy Hosting Control Center

2. Choose settings-file extensions management-default extensions

3. In the table that is presented edit ".php" Runs under "PHP 5.2.x" (instead of "PHP 5.2.x FastCGI")

## Zero byte download with WebDAV

1. Add "`include 'Sabre/DAV/UUIDUtil.php';`" in `Sabre.includes.php` 
2. Ensure write access in both "`temp`" and "`data`" folder

## Downloaded files are corrupted

Make sure `configuration.php` does not have any characters outside `<?php` - `?>` tags, including spaces or line feeds. These characters are interpreted as output, and will corrupt file downloads.

See troubleshooting step 1 to check your `configuration.php`.