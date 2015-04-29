WebDAV plugin is separately downloaded plugin that allows accessing Kloudspeaker content via WebDAV protocol, see [Downloads](http://www.kloudspeaker.com/downloads.php).

WebDAV plugin is based on SabreDAV framework from Rooftop Solutions (http://code.google.com/p/sabredav/), which is released under New BSD License (http://www.opensource.org/licenses/bsd-license.php).

## Installation

Copy folder "dav" under Kloudspeaker backend folder, and continue with configuration.

## Configuration

### WebDAV client URL

Default URL for accessing files via WebDAV client is "`http[s]://[host_ip]/[kloudspeaker_backend_path]/dav/`".

In the installation package, there is a rewrite rule in file ".htaccess" which applies only to Apache web servers.

If this does not apply your server, or it is disabled, the url becomes "`http[s]://[host_ip]/[kloudspeaker_backend_path]/dav/index.php/`" (Note that the url always ends with "/").

Modify "index.php" and update variable `$BASE_URI` according to your configuration. The value is the access url without protocol or host ip.

For example, if Kloudspeaker backend is located at "http://host/kloudspeaker/backend", the base uri should be "`/kloudspeaker/backend/dav/`" (assuming rewrite applies, "/kloudspeaker/backend/dav/index.php/" if not).
	
If htaccess rules are not available, you can also use Apache alias. For example following alias in Apache configuration will do the same:

	alias  /kloudspeaker/backend/dav  /kloudspeaker/backend/dav/index.php

### Script location

If dav folder needs to be located somewhere else than under Kloudspeaker backend, modify "index.php" and update variables `$KLOUDSPEAKER_BACKEND_ROOT` and `$BASE_URI` (see previous chapter) accordingly.

### Authentication

Currently only basic auth is possible.

### Locking

By default, dav is set up with locking support. Some clients don't require this (see http://code.google.com/p/sabredav/), and can be disabled by setting "$ENABLE_LOCKING = FALSE;" in index.php

### Temporary file filter

By default, dav is set up to filter temporary files, because many clients create garbage files on your WebDAV share (see http://code.google.com/p/sabredav/wiki/TemporaryFileFilter). This can be disabled by setting "$ENABLE_TEMPORARY_FILE_FILTER = FALSE;" in index.php