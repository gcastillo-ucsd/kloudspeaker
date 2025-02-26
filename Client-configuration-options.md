Following settings are available in client configuration:


	<script type="text/javascript">
		require(['kloudspeaker/app'], function(app) {
			app.init({
				"service-path": "backend/",				// service path
				"service-param": false,					// service param
				"languages": {},						// languages
				"default-view": "/files/",
				"view-url": true,						// reflect view in url
				"app-element-id": "kloudspeaker",		// application element ID
				"html5-uploader": {},					// uploader

				"file-view": {							// file view options
					"drop-type": ...,					// customize drag&drop operation
					"create-empty-file-action": false,	// create empty file
					"default-view-mode": "list",		// default view mode
					"default-sort": null,
					"icon-view-thumbnails": false,		// show icon thumbnails in icon view mode
					"list-view-columns": {
						...								// file list column setup
					},
					"list-view-hierarchy": false,		// show hierarchy in list view
					...
				},
				"modules": {
					// modules configuration
				},
				plugins: {
					// plugin configuration
				}
			});
		});
	</script>

## General

### Service path (`service-path`)

Location of the backend script relative to the index.html file.

### Service param (`service-param`)

By default, REST API service is part of the request path, for example "http://host/kloudspeaker/backend/r.php/request/path/", where "request/path" would be the service requested.

Some servers don't support this format, and PHP application does not receive the service path at all. In this cases, enabling `service-param`, these requests are transformed into using URL parameter "http://host/kloudspeaker/backend/r.php?sp=request/path/"

### Default view (`default-view`)

The view opened after login, if url does not specify the view. By default, files view is opened.

### Languages (`languages`)

See [[languages|Languages]]

### Application element ID (`app-element-id`)

By default, Kloudspeaker expects to find div element with ID "kloudspeaker" from the HTML page. With this setting, the element ID can be customized.

### Reflect view in URL (`view-url`)

Kloudspeaker can reflect the current view in the browser url (if browser supports history pushState). By default this is enabled.

### Uploader (`html5-uploader`)

See [[uploader|Uploader]]

## File view options

### Drag&drop operation (`drop-type`)

By default, drag&drop has following logic:
  * if dragging single item, and it is from same root folder than the target folder, item is moved
  * if dragging single item, and it is from different root folder than the target folder, item is copied
  * if dragging multiple items, items are copied

With this setting it is possible to customize the drag&drop operation.

Setting can have single constant value that is applied always, for example:

	"file-view": {
		"drop-type": "copy"
	}

Setting can also have different values for dragging&dropping single or multiple items:

	"file-view": {
		"drop-type": {
			single: "move",
			multi: "copy"
		}
	}

Also, value can be a function where custom logic can be defined, for example:

	"file-view": {
		"drop-type": function(to, i) {
			// "to" is the target folder
			// "i" is dragged item/items
	
			if (window.isArray(i)) {
				//dragging multiple items
				return "copy";
			}
			// dragging single item
			var copy = (to.root_id != i.root_id);
			return copy ? "copy" : "move";
		}
	}

In this example multiple items are always copied, and single item copied when dragged from different root folder.

Possible return values from this function can be "`copy`" or "`move`".

### Default sort (`default-sort`)

The sort criteria used by default in list view. For example:

	"default-sort": {
		col: 'modified',
		asc: false
	}

The value "col" is the id of the column, and "asc" specifies the sort order (if not given, will be in ascending order). By default, list is ordered with column "name" in ascending order.

### Create empty file (`create-empty-file-action`)

Action "create empty file" is not shown by default. With this setting, it can be enabled in folder action menu.

### Icon view thumbnails (`icon-view-thumbnails`)

With this option, icon view can display supported images (gif, png, jpg, jpeg) with thumbnail. Requires thumbnail feature enabled in backend [https://github.com/sjarvela/kloudspeaker/wiki/Backend-configuration-options#enable-thumbnails-enable_thumbnails]

### Default view mode (`default-view-mode`)

View mode selected when Kloudspeaker is launched, options are "`list`" (default), "`small-icon`" and "`large-icon`".

### List view hierarchy (`list-view-hierarchy`)

List view can show folder hierarchy, which allows expanding folders in the list. By default this is disabled.

### File list column customization

File list columns can be customized with setting 'list-view-columns'.

The setting accepts following format:

		app.init({
			"file-view": {
				"list-view-columns": [
					{ /* column 1 settings */ },
					"column-2-id",
					...
				]
			}
		});

Option takes a list of columns in the order they are displayed. Each value in the list can be either string (column ID) or object with column settings.

Column ID identifies the data shown, which can be either built-in predefined column or plugin provided.

For example:

		app.init({
			"file-view": {
				"list-view-columns": [
					"name",
					{
						id: 'size',
						width: 250
					},
					"type"
				]
			}
		});

This example shows three columns in following order: "name", "size" and "type". For column "size", also width is set.

Kloudspeaker provides following columns:

* 'name': File or folder name
* 'type': File or folder type description
* 'size': File size
* 'file-modified': Last modification time
* 'item-description': Item description

Following plugins provide more column data:

  * [[Comments|Comments-plugin#file-list-columns]]

Column settings accepts following settings:

* 'title': Text key (in localization file) shown in the column title. If not provided, default title used
* 'sortable': Is column sortable
* 'width': Column width in pixels
* 'min-width': Column minimum width in pixels

Example configuration:

		app.init({
			"list-view-columns": {
				"name": {width: 250},
				"type": {title:"myOwnColumnTitleKey"},
				"size": {}
			}
		});

### Actions customizations

File list actions can be customized with following syntax:

	app.init({
		"file-view": {	
			actions: {
				onClick: function(item, ctx) {
					return "open_menu";
				},
				onDblClick: function(item, ctx) {
					if (item.is_file) return "open_popup";
					return "go_into_folder";
				},
				onRightClick: function(item, ctx) {
					...
				}
			}
		},
		...

The object "actions" has can define following actions:
  * onClick (for regular click in file list)
  * onDblClick (for double click in file list)
  * onRightClick (for right click in file list)

These action functions are called with following parameters:
  * `item`: the file or folder
  * `ctx`: context with following properties
    * `viewtype`: file list type "list" or "icon"
    * `target`: action target, in list view the column
    * `element`: jQuery object for the element representing the file or folder
    * `viewport`: jQuery object for the viewport (used when displaying UI popups etc)
    * `container`: jQuery object for the container (used when displaying UI popups etc)
    * `folder`: folder that is currently displayed
    * `folder_permission`: current user permission for the item

Possible return value for the action functions:
  * `"open_popup"`: opens the popup
  * `"open_menu"`: opens the action menu
  * `"go_into_folder"`: goes into the folder (if item is folder)
  * `false` or no return value: default action
  * `true`: default action is skipped (used for custom actions)

The options with string value are shortcuts for most common options, but by returning `true` you can define your own action handler.

## Modules configuration

With modules configuration, it is possible to define additional kloudspeaker modules that are loaded once the application is started.

Also, if loading custom modules, it is possible to define the location of the modules (if loading async).

Example configuration:

            "modules": {
                load: ['my-package/module1', 'my-package/module2'],
                paths: {
                    'my-package': '/kloudspeaker/my-modules'
                }
            }

This configuration defines that two modules, "module1" and "module2", are loaded when application starts. These modules are loaded from package "my-package", which are set to be found from "/kloudspeaker/my-modules".