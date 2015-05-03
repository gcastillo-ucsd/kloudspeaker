Kloudspeaker registers a global object `kloudspeaker`, which provides various services.

## Request

Current page request can be retrieved from `kloudspeaker.request`. It provides following functions:

* `getParam(name)`: function for resolving request parameter
* `getParams`: function for getting all request params
* `getBaseUrl`: function for resolving base url for the request (URL before params and view path)
* `getPageUrl`: function for resolving current page url (URL before params)

## Service

Kloudspeaker REST API (backend services) can be used with `kloudspeaker.service`. It provides function for all REST methods:

* `get(url)`: method GET
* `post(url, data)`: method POST with optional data
* `put(url, data)`: method PUT with optional data
* `del(url, data)`: method DELETE with optional data

All functions return a promise object, which will resolve with the result returned from backend service. If service call fails, the promise is rejected with the error object.

For example, success result can be handled like this:

    kloudspeaker.service.post("my/service", {
        foo: bar
    }).done(function(r) {
        // process result
    });

By default, all errors will trigger error dialog with system default error message. Any service caller can handle the error explicitly, and prevent default error message.

    kloudspeaker.service.post("my/service", {
        foo: bar
    }).done(function(r) {
        // process result
    }).fail(function(err) {
        this.handled = true; // prevent default error
        // handle error
    });

## Session

Current session can be retrieved from `kloudspeaker.session`. It has following attributes:

* `id`: session id
* `user`: session user (false if not logged in)
* `features`: object with feature keys for all enabled features
* `plugins`: backend plugins and their session data
* `version` (and `revision`): application version

User object has following data:

## Events

Kloudspeaker events can be listened

    kloudspeaker.events.addEventHandler(fn, eventId);

where `fn` is handler function (called with one parameter, event) and `eventId` string for event identifier.

for example, to listen session start event

    kloudspeaker.events.addEventHandler(function(e) {
        // add event logic
    }, "session/start");

Events can be sent with

    kloudspeaker.events.dispatch(eventId, payload);

where `eventId` is string for event identifier and `payload` is event object. For example, session start event payload object is the session object.