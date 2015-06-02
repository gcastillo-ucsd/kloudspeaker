Kloudspeaker has command line interface script, which allows controlling Kloudspeaker from server scripts.

System and plugins can register commands that can be run, optionally as specified user.

For example:

    php kloudspeaker/backend/cmd.php upload --user=2 --src=/tmp/downloads/000948.pdf --target=3:/documents

This command would execute command named `upload`, and it would be run as user with id 2. The file would be uploaded into folder with ID 3 and subfolder "documents".

## Available commands

### `upload`

Performs file upload just as it would from UI. This will trigger same events and handlers as they would in UI, for example event logging, quota checking etc.

Requires attributes `src` for local file to be uploaded and `target` for Kloudspeaker location where file is uploaded

### `copy`

Performs file copy, differs from command `upload` so that file is added in the background without triggering events or action handlers.

Requires attributes `src` for local file to be uploaded and `target` for Kloudspeaker location where file is uploaded

## Custom commands

Plugins can register own commands like this:

	class MyPlugin extends PluginBase {
		public function setup() {
			$this->env->commands()->register("my-plugin:some-command", $this);
		}
	}

In register call:
* First parameter is command name, use unique names that don't collide (prefix with plugin name etc)
* Second parameter is command handler


Possible command handler options are:
* Object reference. With this option, it is assumed that the object has function "execute" which will be called.
* Function name as string. With this option, global function with given name is executed.

In all cases, the execute is called with two parameters:
1. Command name (string)
2. Invocation options (array of name/value pairs from the command line)