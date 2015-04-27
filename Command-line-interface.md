Kloudspeaker has command line interface script, which allows controlling Kloudspeaker from server scripts.

System and plugins can register commands that can be run, optionally as specified user.

For example:

    php kloudspeaker/backend/cmd.php upload --user=2 --src=/tmp/downloads/000948.pdf --target=2:/documents

This command would execute command named `upload`, and it would be run as user with id 2.

## Available commands

### `upload`

Performs file upload just as it would from UI. This will trigger same events and handlers as they would in UI, for example event logging, quota checking etc.

Requires attributes `src` for local file to be uploaded and `target` for Kloudspeaker location where file is uploaded

### `copy`

Performs file copy, differs from command `upload` so that file is added in the background without triggering events or action handlers.

Requires attributes `src` for local file to be uploaded and `target` for Kloudspeaker location where file is uploaded