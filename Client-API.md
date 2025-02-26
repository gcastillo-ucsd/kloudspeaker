Kloudspeaker uses [AMD with require.js](http://requirejs.org/docs/whyamd.html), and publishes different services and interfaces via modules that can be imported into other modules like plugins.

For example, to get Kloudspeaker service in a module, it can be imported like this:

    define(['kloudspeaker/service'], function(service) {
        return function() {        
            // somewhere in code
            service.post('your/service', { your: data }).done(function() { ... });
        };
    });

# Core

## kloudspeaker/request

This module represents current page request, and it provides following functions:

* `getParam(name)`: function for resolving request parameter
* `getParams`: function for getting all request params
* `getBaseUrl`: function for resolving base url for the request (URL before params and view path)
* `getPageUrl`: function for resolving current page url (URL before params)

## kloudspeaker/service

Kloudspeaker REST API (backend services) can be used with service module. It provides function for all REST methods:

* `get(url)`: method GET
* `post(url, data)`: method POST with optional data
* `put(url, data)`: method PUT with optional data
* `del(url, data)`: method DELETE with optional data

All functions return a promise object, which will resolve with the result returned from backend service. If service call fails, the promise is rejected with the error object.

For example, success result can be handled like this:

    service.post("my/service", {
        foo: bar
    }).done(function(r) {
        // process result
    });

By default, all errors will trigger error dialog with system default error message. Any service caller can handle the error explicitly, and prevent default error message.

    service.post("my/service", {
        foo: bar
    }).done(function(r) {
        // process result
    }).fail(function(err) {
        this.handled = true; // prevent default error
        // handle error
    });

## kloudspeaker/session

Current session can be retrieved from session module with function "get". This function returns the active session object, or false if no session is active.

Session object has following attributes:

* `id`: session id
* `user`: session user (false if not logged in)
* `features`: object with feature keys for all enabled features
* `plugins`: backend plugins and their session data
* `version` (and `revision`): application version

User object has following data:

## kloudspeaker/events

Events module provides methods for listening and sending application events.

Events can be listened

    events.addEventHandler(fn, eventId);

where `fn` is handler function (called with one parameter, event) and `eventId` string for event identifier.

for example, to listen session start event

    events.addEventHandler(function(e) {
        // add event logic
    }, "session/start");

Events can be sent with

    events.dispatch(eventId, payload);

where `eventId` is string for event identifier and `payload` is event object. For example, session start event payload object is the session object.

## kloudspeaker/filesystem

Kloudspeaker filesystem operations can be done using filesystem module. It provides following functions:

* `getDownloadUrl(item)`: get download url for provided item
* `getUploadUrl(folder)`: get upload url for provided folder
* `itemDetails(item)`: get item details for provided item
* `folderInfo(folder)`: get folder info for provided folder
* `findFolder`
* `hasPermission(item, name, required)`
* `items(parent, files)`
* `createEmptyFile(parent, name)`
* `copy(item|items, to)`
* `copyHere(item, name)`
* `canCopyTo(item, to)`
* `move(item|items, to)`
* `canMoveTo(item, to)`
* `rename(item, name)`
* `del(item|items)`
* `createFolder(parent, name)`

# UI

## kloudspeaker/ui/texts

Texts module provides methods for getting localized strings.

    texts.get(id, params)

where id is text key (string) and params (optional) possible parameters in the text.

For example

    var t = texts.get('someTextKey');

or

    var t = texts.get('someTextKeyWithParams', ['firstParam', 'secondParam']);


Texts are defined in localization files, and are loaded based on language defined.

## Templates (deprecated)

Kloudspeaker uses JQuery Templates engine (no longer maintained, documentation http://web.archive.org/web/20121014080309/http://api.jquery.com/jquery.tmpl/) for creating UI.

Templates are declared in HTML:

	<script id="my-tmpl" type="text/x-jquery-tmpl">
		<div class="my-element">
			${message}
		</div>
	</script>

Template element can be created using `kloudspeaker.dom.template`, for example:

	var $e = kloudspeaker.dom.template("my-tmpl", data, opt);

The result object is jQuery DOM object that can be used like any other jQuery DOM object, for example append to existing DOM object.