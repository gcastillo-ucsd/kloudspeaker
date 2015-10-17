Using module "`kloudspeaker/ui/views`" it is possible to register full application views.

    views.registerView("myview", function(rqParts, urlParams) { ... });

This will register view handler for view id "`myview`". When browser opens URL "`http://yoursite/kloudspeaker?v=myview`", this function is called.

Param rqParts is array with view id parts, for example if view opened is "`?v=myview/subview`", the array is `["myview", "subview"]`.

Param `urlParams` contains all parameters in the request.

The function can return
* `false` if no view should be opened
* object with `model` (and optionally `view`) for UI composition

For example:

    views.registerView("myview", function(rqParts, urlParams) {
        return {
            model: 'my-package/myview'
        };
    });

For options `model` and `view`, see Composition.

Example for full view can be found at [Registration plugin](https://github.com/sjarvela/kloudspeaker/blob/master/backend/plugin/Registration/client/main.js)
