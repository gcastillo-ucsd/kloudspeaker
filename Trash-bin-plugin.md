Trash bin plugin can provide two different functionality modes:

1. At minimum, plugin can add visual trash can into the file view, where files or folders can be drag&dropped for deletion. In this mode, files/folders are deleted permanently, the trash bin only allows easier and faster way to do it.

2. When configuring trash bin folder in configuration, the plugin will also intercept delete actions and store deleted files/folders into trash bin folder. Contents of the trash bin can then be viewed, and files/folders can be restored or deleted permanently.

**NOTE** Trash bin plugin is beta release, and does not yet have all functionality. For example, integration with plugins like Share or Quota is not yet added.

## Configuration

At minimum, plugin is only registered in the configuration

    $CONFIGURATION = array(
        ...
        "plugins" => array(
            "TrashBin" => array(),
            ...
        )
    );

Trash bin storage can be enabled by defining folder location:

    "TrashBin" => array(
        "folder" => "[TRASH_BIN_LOCATION]"
    )

The value `folder` should have absolute path to the folder where trashed items are stored. This folder should not be under published Kloudspeaker folders, or even web server root if possible.