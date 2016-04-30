Kloudspeaker has HTML5 uploader (based on [JQuery-File-Upload](https://github.com/blueimp/jQuery-File-Upload)) which supports all HTML5 uploading features if browser has the capabilities.

Uploader settings are defined in Kloudspeaker app init:


	kloudspeaker.App.init({
		… ,
		"html5-uploader": {
			...
		}
	});


For more options, see [JQuery-File-Upload options](https://github.com/blueimp/jQuery-File-Upload/wiki/Options)

## Server max upload limit

To control server max upload limit, change following settings in PHP ini:

    ; Maximum allowed size for single uploaded file
    upload_max_filesize = 40M
    
    ; Maximum allowed total size of post request, must be greater than or equal to upload_max_filesize
    post_max_size = 40M

These settings control regular uploads, but using HTML5 uploader options, these restrictions can be avoided by using alternative upload methods.

## Avoiding server max upload size restrictions

To avoid server side max upload size restrictions, following HTML5 options are available

### Chunked upload

Chunked uploading uploads smaller pieces at once, where each piece is smaller than the max size allowed. 

Following setting enables chunked upload (value in bytes):

	"html5-uploader": {
		maxChunkSize: 100000
	}


### Stream upload

Stream uploading uses HTTP PUT method for sending file contents as a stream.

Following client setting that enables stream upload:

	"html5-uploader": {
		multipart: false
	}

Note that setting "`maxChunkSize`" should not be defined (or should be "`false`"), as it applies to non-multipart uploads as well.